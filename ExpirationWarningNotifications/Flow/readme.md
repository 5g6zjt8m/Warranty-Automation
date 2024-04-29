# Expiration Warning Notifications

[Previous page](/ExpirationWarningNotifications/readme.md) | [Back home](/README.md)

## Top Level

This is what the flow looks like from the top level.

![EWN0](/ExpirationWarningNotifications/Flow/Screenshots/EWN0toplevel.png)

This gives a general idea for how the flow is planned out. The following section of this page will give exact details and code behind every step shown here.

## Flow

Here is a closer look into how this flow runs, in order. It may be helpful to reference the top level image to better understand where exactly in the flow these actions are being run.

It is also useful to take a look at the json behind these actions. This gives insight as to what data the action is exactly referencing. Example being, actually seeing what array ``value`` is referring to.

In addition, the json will show the full expressions that I had to write for these actions to work.

### Left Branch

![EWN1L](/ExpirationWarningNotifications/Flow/Screenshots/EWN1Lpullallwithexpirationdatemarkedforrenewalandlastcheckin.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN1Lpullallwithexpirationdatemarkedforrenewalandlastcheckin.json)

_

![EWN2L](/ExpirationWarningNotifications/Flow/Screenshots/EWN2LaddDaysToExpirytoobjects.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN2LaddDaysToExpirytoobjects.json)

_

![EWN3L](/ExpirationWarningNotifications/Flow/Screenshots/EWN3LaddDaysSinceCheckIntoobjects2.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN3LaddDaysSinceCheckIntoobjects2.json)

_

![EWN4L](/ExpirationWarningNotifications/Flow/Screenshots/EWN4LmakeDaysToExpiryanavailableproperty.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN4LmakeDaysToExpiryanavailableproperty.json)

_

![EWN5L](/ExpirationWarningNotifications/Flow/Screenshots/EWN5LdevicesclosetoexpiringANDalreadyexpiredfulllist.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN5LdevicesclosetoexpiringANDalreadyexpiredfulllist.json)

_

![EWN6L](/ExpirationWarningNotifications/Flow/Screenshots/EWN6Lclosetoexpiringvariable.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN6Lclosetoexpiringvariable.json)

_

![EWN7L](/ExpirationWarningNotifications/Flow/Screenshots/EWN7Lalreadyexpiredvariable.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN7Lalreadyexpiredvariable.json)

_

![EWN8L](/ExpirationWarningNotifications/Flow/Screenshots/EWN8Lnocheckinvariable.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN8Lnocheckinvariable.json)

_

![EWNL9L](/ExpirationWarningNotifications/Flow/Screenshots/EWNL9Ldevicesclosetoexpiringbutnotexpired.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL9Ldevicesclosetoexpiringbutnotexpired.json)

_

![EWNL9C](/ExpirationWarningNotifications/Flow/Screenshots/EWNL9Conlyexpireddevices.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL9Conlyexpireddevices.json)

_

![EWNL9R](/ExpirationWarningNotifications/Flow/Screenshots/EWNL9Rdevicesthathavenotcheckedinfor60days.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL9Rdevicesthathavenotcheckedinfor60days.json)

_

![EWNL10L](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10Liftherearedevicesclosetoexpiringbutnotexpired.png)

No code for this step, but the expressions are ``empty(body('devices_close_to_expiring,_but_not_expired'))`` and ``true``

_

![EWNL10C](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10Cifthereareexpireddevices.png)

No code for this step, but the expressions are ``empty(body('only_expired_devices'))`` and ``true``

_

![EWNL10R](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10Riftherearedevicesthathavenotcheckedin.png)

No code for this step, but the expressions are ``empty(body('devices_that_have_not_checked_in_for_60+_days'))`` and ``true``

_

![EWNL10.1L](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.1LCreateHTMLtable.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.1LCreateHTMLtable.json)

_

![EWNL10.1C](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.1CCreateHTMLtable2.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.1CCreateHTMLtable2.json)

_

![EWNL10.1R](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.1RCreateHTMLtable4.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.1RCreateHTMLtable4.json)

_

![EWNL10.2L](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.2LCompose.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.2LCompose.json)

_

![EWNL10.2C](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.2CCompose2.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.2CCompose2.json)

_

![EWNL10.2R](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.2RCompose4.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.2RCompose4.json)

_

![EWNL10.3L](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.3LSetvariable.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.3LSetvariable.json)

_

![EWNL10.3C](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.3CSetvariable2.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.3CSetvariable2.json)

_

![EWNL10.3R](/ExpirationWarningNotifications/Flow/Screenshots/EWNL10.3RSetvariable4.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNL10.3RSetvariable4.json)

_

### Right Branch

![EWNR1](/ExpirationWarningNotifications/Flow/Screenshots/EWNR1pullallwithnullexpirationorstatus.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNR1pullallwithnullexpirationorstatus.json)

_

![EWNLR2](/ExpirationWarningNotifications/Flow/Screenshots/EWNR2nullvaluevariable.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNR2nullvaluevariable.json)

_

![EWNR3](/ExpirationWarningNotifications/Flow/Screenshots/EWNR3iftherearedeviceswithmissingvalues.png)

No code for this step, but the expressions are ``empty(body('devices_that_have_not_checked_in_for_60+_days'))`` and ``true``

_

![EWNR3.1](/ExpirationWarningNotifications/Flow/Screenshots/EWNR3.1CreateHTMLtable3.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNR3.1CreateHTMLtable3.json)

_

![EWNR3.2](/ExpirationWarningNotifications/Flow/Screenshots/EWNR3.2Compose3.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNR3.2Compose3.json)

_

![EWNR3.3](/ExpirationWarningNotifications/Flow/Screenshots/EWNR3.3SetVariable3.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWNR3.3SetVariable3.json)

_

### Joined Branches

![EWN11L](/ExpirationWarningNotifications/Flow/Screenshots/EWN11Liftheresanythingtoreportsendtheemail.png)

No code for this step, but the expressions are ``variables('Null values')``, ``variables('No check in')``, ``variables('Already expired')`` and ``variables('Close to expiring')``. The empty boxes on the right actually contain code Alt+255.

_

![EWN11.1L](/ExpirationWarningNotifications/Flow/Screenshots/EWN11.1LSendanemailV2.png)

[Peek Code](/ExpirationWarningNotifications/Flow/PeekCode/EWN11.1LSendanemailV2.json)

_


[Previous page](/ExpirationWarningNotifications/readme.md) | [Back home](/README.md)
