---
description: Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Händelseserialisering
topic-fix: Developer and implementation
uuid: acdeda16-ab83-4cfc-907d-33448b801b31
exl-id: 03556912-fdcc-402e-b1de-233771f4e719
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 5%

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
