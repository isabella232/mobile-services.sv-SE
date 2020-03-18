---
description: Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
keywords: android;library;mobile;sdk
seo-description: Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-title: Händelseserialisering
solution: Marketing Cloud,Analytics
title: Händelseserialisering
topic: Developer and implementation
uuid: acdeda16-ab83-4cfc-907d-33448b801b31
translation-type: tm+mt
source-git-commit: bf076aa8e59d5c3e634fc4ae21f0de0d4541a83f

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

