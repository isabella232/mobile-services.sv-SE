---
description: Händelseserialisering stöds inte av bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-description: Händelseserialisering stöds inte av bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-title: Händelseserialisering
solution: Experience Cloud,Analytics
title: Händelseserialisering
topic-fix: Developer and implementation
uuid: a5966d05-e218-446f-9f19-8664a84b74cd
exl-id: 42ea5e0f-a69e-44ab-aa4e-bbec27815cc8
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 7%

---

# Händelseserialisering{#event-serialization}

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
