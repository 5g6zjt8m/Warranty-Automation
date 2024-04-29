# Warranty Automation
[Next Page](/IntuneToSharepoint/readme.md)

# Navigating this project

There are readme files in most directories if you choose to poke around. Otherwise, here is a table of contents for how this repository is designed to be read:

Table of contents
1. [Intune to Sharepoint](/IntuneToSharepoint/readme.md)

    1. [Flow](/IntuneToSharepoint/Flow/readme.md)

2. [Expiration Warning Notifications](/ExpirationWarningNotifications/readme.md)

    1. [Flow](/ExpirationWarningNotifications/Flow/readme.md)

There will also be hyperlinks at the beginning and end of each readme to navigate pages in the intended way.

## What is this? 
I created a system that sends email reports regarding the warranty status of Android devices in Intune. This is primarily geared towards Zebra scanners since those are the only Android devices we have contracts with. This system still works with other stuff though, as long as there's an expiration date and a will to renew the warranty. 
 
### What are the most important things to know? 
When you add a new Android device to Intune, you'll need to manually input its warranty information into this Sharepoint list, screenshot below. The list refreshes overnight.

![Sharepoint list](/Screenshots/SPlist.png)
 
Find the device in the list > double click it > enter the warranty expiration date in MM/DD/YYYY format. By default, all devices added here will be flagged "Yes" for renewing at expiration. Change this to "No" if there is no contract that needs to be renewed. 
 
If a device does not have a warranty contract at all (perhaps not even a Zebra device), entering any date into the expiration field will work. Ensure that the renewal is flagged "No" for these devices and we will not be notified about them. 
 
Reports will be sent in an email weekly. If there's no important information to report, nothing will be sent out. The email is meant to notify us that action needs to be taken. 
 
### How does it work at a basic level? 
A Power Automate flow makes an Intune API call every night. It takes that info and sticks it into a Sharepoint list. Another Power Automate flow analyzes the contents of that list and determines where manual action needs to be taken (contracts close to expiring/expired, devices missing info, devices not checking into Intune). It then organizes this info into HTML tables and sends it out in an email. 
 
### What are the limitations? 
This only accounts for devices that are in Intune. This means Zebra devices TC75x or newer, and Android 8 or newer. If devices are not enrolled, they cannot be tracked using this tool. 
Human error is a risk when manually entering expiration dates. If a date is set wrong, we may not be notified in time to renew the contract. 
The ``devices_that_have_not_checked_in_for_60+_days`` filtered array only accounts for devices where the ``DaysSinceCheckIn`` property ≤-60, and devices that are expiring in ≤30 days. This means only devices close to expiry and past expiry will be analyzed for their check in date (as long as it is not ``null``). For the scope of this project, it is ok that this happens. It is designed to notify for expiring warranties, not all devices that have not checked in for a while regardless of warranty status.

# [Next Page](/IntuneToSharepoint/readme.md)