# Expiration Warning Notifications

[Previous Page](/IntuneToSharepoint/Flow/readme.md) | [Next page](/ExpirationWarningNotifications/Flow/readme.md)

There are two Power Automate flows. One is titled **Android Warranty: Intune to Sharepoint** and the other is titled **Android Warranty: Expiration Warning Notifications**. 
 
This page covers the second flow, organizing the data and sending alerts. 
 
Logically, this is how the flow is laid out: 
#### (Left Branch) 
- Pull all items from Sharepoint that have an expiration date, are marked to be renewed, and have a check in date. 
- Add a new property to each item in that Sharepoint array, telling how many days away from expiry the device is. 
- Add a new property to each item in that new array, telling how many days it has been since the last check in. 
- Parse that new array so the properties are available to select. 
- Filter the array, grabbing all devices that are less than or equal to 30 days away from expiring (including negative numbers) 
- Initialize separate variables for close to expiring, already expired, and lacking a recent check in date. 
- Filter full array for devices that are more than 0 days away from expiring. 
- If that array is not empty, organize those items into an HTML table and write that table to the close to expiring variable. 
- Filter full array for devices that are less than 0 days away from expiring (already expired). 
- If that array is not empty, organize those items into an HTML table and write that table to the already expired variable. 
- Filter the full array for devices that have not checked in for 60 days. 
- If that array is not empty, organize those items into an HTML table and write that table to the no check in variable. 
#### (Right Branch) 
- Pull all items from Sharepoint that don't have an expiration date, renewal status, or check in date. 
- Initialize variable for null values. 
- If the Sharepoint array for missing values is not empty, organize those items into an HTML table and write that table to the null values variable. 
#### (Closing Branch) 
- If the variables had data written to them, send out an email with those variables as the contents.
 
## Processing the data 
#### (Left Branch) 
I needed a way to tell if a device was expired or not. This was solved by adding a new property that would calculate how many days away from today the device is from expiry. I wrote the following expression to achieve this: 
 
``addProperty(item(), 'DaysToExpiry', div(sub(ticks(item()?['WarrantyExpirationDate']), ticks(utcNow())), 864000000000)) ``
 
It converts today's date to ticks, the warranty expiration date to ticks, subtracts the two, and divides the result by the number of ticks in a day. This results in a number that represents the difference between dates. In this case, today vs expiration. 
 
I did the same to calculate the days since last check in, using an identical expression in another action: 
 
``addProperty(item(), 'DaysSinceCheckIn', div(sub(ticks(item()?['Last_x0020_Check_x0020_In']), ticks(utcNow())), 864000000000))`` 
 
I then parse this new array that has both of the new properties so that they will be selectable. 
 
Finally, I filter that parsed array and only include devices that have 30 days or less from expiration. This includes negative numbers. -5 days would mean 5 days past expiry. 
 
#### (Right Branch) 
I also needed a way to find devices that were missing details in the Sharepoint list. If some were missing expiration dates, I wanted it to be known and addressed. I achieved this by pulling all devices from the Sharepoint list that had a null value for their expiration date, renewal status, or check in date. If any of those values were null, that item would be in the resulting array. 
 
### Setting the variables 
#### (Left Branch) 
I created three variables to store different email responses. One is for devices that are close to expiring, one is for devices that have expired, and another is for devices that haven't checked in within the past 60 days. 
 
When I created the variables, I gave them all the value Alt+255 (blank unicode character) as a way to represent the idea "nothing has been written to this variable". More on this later. 
 
Close to expiring, but not expired: 
I filter the full array for objects that are greater than or equal to 0 days away from expiring. Keep in mind that the full array only includes devices that are 30 days away or less from expiring. This results in finding devices that are between 0-30 days away from expiration. 
 
I use a conditional statement to find out whether or not this filtered array is empty. If it is, then nothing happens. This is a simple expression used in a portion of the conditional statement: 
 
``empty(body('devices_close_to_expiring,_but_not_expired')) ``
 
If the body of the filtered array is not empty, an HTML table is created that details the properties of all of the items in the array. I then use the compose action to format the HTML table, in this fashion. The output block is the previously created HTML table. 
 
![EWNL10.2](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.2LCompose.png)

The variable that represents close to expiring devices is then assigned its value; the HTML table with a heading. 
 
These same steps are repeated for devices that are already expired (``DaysToExpiry<0``), and devices that are ≤30 days from expiry but have not checked in recently (``DaysSinceCheckIn≤-60``). All tables are written to their respective variables. 
 
#### (Right Branch) 
A variable to store tables containing devices with missing values is initialized. The same logic is run as before; if the array is empty, do nothing. If the array is not empty, create a table and write it to the variable. 
 
### Sending the notification 
There is a final conditional statement that joins the two branches. If all four variables still contain the original string Alt+255 that was assigned at their creation, nothing happens. If one or more variables had their original value overwritten (HTML table assigned), the flow continues. 
 
(There are probably better ways to achieve the goal of figuring out if a variable was overwritten from ``null``). 
 
This leads to the final action of sending the email, which is quite simple. 
 
![EWN11.1L](/ExpirationWarningNotifications/Flow/Screenshots/EWN11.1LSendanemailV2.png)
 
The body of the email is just the contents of the variables. If the variable is empty, a blank unicode character will take its place.

[Previous page](/IntuneToSharepoint/Flow/readme.md) | [Next page](/ExpirationWarningNotifications/Flow/readme.md)
