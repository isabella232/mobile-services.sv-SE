---
description: Händelseserialisering stöds inte av bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-description: Händelseserialisering stöds inte av bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-title: Händelseserialisering
solution: Marketing Cloud,Analytics
title: Händelseserialisering
topic: Developer and implementation
uuid: 7220a001-1174-4013-91ff-e8603d8ab265
translation-type: tm+mt
source-git-commit: f5ba33fe805c502b8ae91ddafcaa0b57e68704b8

---


# Händelseserialisering {#event-serialization}

Händelseserialisering stöds inte av bearbetningsregler. I mobil-SDK måste du använda en speciell syntax i parametern kontextdata för att ange serialiserade händelser direkt i serveranropet.

```js
cdata["&&events"] = "event1:12341234";
```

Exempel:

```js
//create a context data dictionary 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
 
// add events 
cdata["&&events"] = "event1:12341234"; 
 
var ADB = ADBMobile; 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
ADB.Analytics.trackAction("action", cdata); 
// trackState example: 
ADB.Analytics.trackState("State Name", cdata);
```

