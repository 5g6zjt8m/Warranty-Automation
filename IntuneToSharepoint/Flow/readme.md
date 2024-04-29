# Intune to Sharepoint

[Previous page](/IntuneToSharepoint/readme.md) | [Next page](/ExpirationWarningNotifications/readme.md)

## Top Level

This is what the flow looks like from the top level.

![IS0](/IntuneToSharepoint/Flow/Screenshots/IS0toplevel.png)

This gives a general idea for how the flow is planned out. The following section of this page will give exact details and code behind every step shown here.

## Flow
Here is a closer look into how this flow runs, in order. It may be helpful to reference the top level image to better understand where exactly in the flow these actions are being run.

It is also useful to take a look at the json behind these actions. This gives insight as to what data the action is exactly referencing. Example being, actually seeing what array ``value`` is referring to.

In addition, the json will show the full expressions that I had to write for these actions to work.

![IS1L](/IntuneToSharepoint/Flow/Screenshots/IS1LIntuneAPIcall.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS1LIntuneAPIcall.json)

_

![IS1R.1](/IntuneToSharepoint/Flow/Screenshots/IS1R.1iftheyearis2026thecertisgoingtoexpiresoon.png)

No code for this step, but the expressions are ``formatDateTime(utcNow(), 'dd-MM-yyyy')`` and ``string(2026)``

_

![IS1R.2](/IntuneToSharepoint/Flow/Screenshots/IS1R.2SendanemailV2.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS1R.2SendanemailV2.json)

_

![IS2](/IntuneToSharepoint/Flow/Screenshots/IS2addformatteddatetointuneobjects.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS2addformatteddatetointuneobjects.json)

_

![IS3](/IntuneToSharepoint/Flow/Screenshots/IS3makeformatteddateanavailableproperty.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS3makeformatteddateanavailableproperty.json)

_

![IS4](/IntuneToSharepoint/Flow/Screenshots/IS4getallitemsfromsharepointlist.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS4getallitemsfromsharepointlist.json)

_

![IS5](/IntuneToSharepoint/Flow/Screenshots/IS5arrayintuneSN.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS55arrayintuneSN.json)

_

![IS6](/IntuneToSharepoint/Flow/Screenshots/IS6arraysharepointSN.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS6arraysharepointSN.json)

_

![IS7L](/IntuneToSharepoint/Flow/Screenshots/IS7Lexistsinintunebutnotsharepointbyserial.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS7Lexistsinintunebutnotsharepointbyserial.json)

_

![IS7R](/IntuneToSharepoint/Flow/Screenshots/IS7Rexistsinsharepointbutnotintunebyserial.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS7Rexistsinsharepointbutnotintunebyserial.json)

_

![IS8L](/IntuneToSharepoint/Flow/Screenshots/IS8Laddthosemissingdevicestosharepoint.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS8Laddthosemissingdevicestosharepoint.json)

_

![IS8R](/IntuneToSharepoint/Flow/Screenshots/IS8Rmakethepropertiesinthoseobjectsselectable.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS8Rmakethepropertiesinthoseobjectsselectable.json)

_

![IS9R](/IntuneToSharepoint/Flow/Screenshots/IS9Rremovethoseextradevicesfromsharepoint.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS9Rremovethoseextradevicesfromsharepoint.json)

_

![IS10.1](/IntuneToSharepoint/Flow/Screenshots/IS10.1updatepropertiesforallitemsinlist.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS10.1updatepropertiesforallitemsinlist.json)

_

![IS10.2](/IntuneToSharepoint/Flow/Screenshots/IS10.2Applytoeach2.png)

[Peek Code](/IntuneToSharepoint/Flow/PeekCode/IS10.2Applytoeach2.json)

_


[Previous page](/IntuneToSharepoint/readme.md) | [Next page](/ExpirationWarningNotifications/readme.md)