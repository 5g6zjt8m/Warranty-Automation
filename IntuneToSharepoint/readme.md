# Intune to Sharepoint
[Previous page](README.md) | [Next page](/IntuneToSharepoint/Flow/readme.md)

There are two Power Automate flows. One is titled **Android Warranty: Intune to Sharepoint** and the other is titled **Android Warranty: Expiration Warning Notifications**. 
 
This page covers the first flow, pulling the data from Intune and getting it into a Sharepoint List. 
 
Logically, this is how the flow is laid out. 

- Pull Android devices from Intune, including the selected properties. 
- Add a new property to each item in that array, reformatting a date nicely. 
- Parse the new array so that the new property is selectable in the future. 
- Pull everything from the Sharepoint list containing the Android devices. (first run, nothing is there) 
- Create an array of only serial numbers from Sharepoint. 
- Create an array of only serial numbers from Intune. 
- Time to compare. Filter out devices that only exist in Intune by comparing serial numbers. 
- Add devices that only exist in Intune to the Sharepoint list. 
- Time to compare again. Filter out devices that only exist in the Sharepoint list by comparing serial numbers. 
- Remove devices that only exist in the Sharepoint list from the Sharepoint list. 
- Loop through all serial numbers in original Intune array with the added property. Pull those serial numbers from the Sharepoint list, and update all of the properties in those list items except for warranty info. 

![Top level flow](/IntuneToSharepoint/Flow/Screenshots/IS0toplevel.png)
 
## Pulling data from Intune into Power Automate 
Great article: https://uem4all.com/2020/04/04/mem-powerautomate-graph/ 
 
The article describes the process much better than I can, including registering an application in Azure and setting up the connector with Intune. 
 
Essentially, the problem to solve was getting some sort of authentication layer between Intune and Power Automate setup so that calls could be made using the MSGraph API. This took quite a bit of experimenting, but the video linked in the article above is great.
 
## Processing the data 
#### From Intune: 
Once the device information has been pulled into Power Automate using the MSGraph API, it is stored in an array. I needed to get the last check in date formatted properly, so I wrote the following expression: 
 
``addProperty(item(), 'LastCheckIn', formatDateTime(item()?['lastSyncDateTime'], 'd')) ``
 
This adds a new property to each item using a more readable date format. I then needed to parse the array so that this new property would be selectable in future actions. 
 
I also create a separate array of just serial numbers from the Intune call. 
 
#### From Sharepoint: 
I pull all of the items in the Sharepoint list and create an array of just the serial numbers. I needed a specific property from this array that I could compare against the Intune array, and every single device will always have a serial number. 
 
#### Comparing two arrays: 
I used the filtering action as it is the most efficient way to loop through items in arrays. One side of the comparison figures out which items exist in Intune, but not Sharepoint (implies new devices have been added to Intune).
 
The other side of the comparison figures out which devices exist in Sharepoint, but not in Intune (implies they have been deleted from Intune/decommissioned). 
 
For each serial number in the Intune (whole) array, if the Sharepoint (serial number) array does not contain this serial number, the item gets included in the result. 
 
For each item in the filtered array that only includes devices not in Sharepoint, create a new item in the Sharepoint list using the properties of the item. Set the warranty renewal property to "Yes". 
 
Onto the other side.  
For each serial number in the Sharepoint (whole) array, if the Intune (serial number) array does not contain this serial number, the item gets included in the result. 
 
Parse this new array. For each item in the parsed filtered array that only includes devices not in Intune, remove it from the Sharepoint list. 
 
## Updating the list 
It is necessary to update the list daily so that check in dates and location changes stay current. This uses a loop within a loop. 
 
For each item in the full Intune list with added property, filter the Sharepoint list for an item that shares the serial number property. If it doesn't, the filter fails and moves on to the next item. For each Sharepoint item that is pulled in doing this, update the contents of that list item using the new data from the Intune array. 
 
## Future proofing 
I added a parallel branch that will send out an email when the year is 2026. This alerts someone to update the certificate that is used for the registered app.

[Previous page](README.md) | [Next page](/IntuneToSharepoint/Flow/readme.md)