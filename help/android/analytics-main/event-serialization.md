---
description: Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
keywords: android;bibliotek;mobil;sdk
seo-description: Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-title: Händelseserialisering
solution: Experience Cloud,Analytics
title: Händelseserialisering
topic-fix: Developer and implementation
uuid: acdeda16-ab83-4cfc-907d-33448b801b31
exl-id: 03556912-fdcc-402e-b1de-233771f4e719
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---

# Händelseserialisering {#event-serialization}

Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.

```java
cdata.put("&&events", "event1:12341234");
```

Exempel:

```java
//create a context data dictionary 
HashMap cdata = new HashMap<String, Object>(); 
 
// add events 
cdata.put("&&events", "event1:12341234"); 
 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
Analytics.trackAction("action", cdata); 
// trackState example: 
Analytics.trackState("State Name", cdata);
```
