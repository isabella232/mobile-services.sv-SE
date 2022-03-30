---
description: Händelseserialisering stöds inte av bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
solution: Experience Cloud Services,Analytics
title: Händelseserialisering
topic-fix: Developer and implementation
uuid: 7220a001-1174-4013-91ff-e8603d8ab265
exl-id: 9cb8d739-8b77-4fe7-8592-22e8cff172d4
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 8%

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
