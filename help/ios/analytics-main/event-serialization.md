---
description: Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-description: Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.
seo-title: Händelseserialisering
solution: Marketing Cloud,Analytics
title: Händelseserialisering
topic: Developer and implementation
uuid: 19a27df4-0998-403d-800c-26ff61149208
translation-type: tm+mt
source-git-commit: 06144a1695ac40ce984656491456968888f9e96e

---


# Händelseserialisering {#event-serialization}

Händelseserialisering stöds inte av bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern context data för att ange serialiserade händelser direkt i serveranropet.

```objective-c
[contextData setObject:@"eventN:serial number" forKey:@"&&events"];
```

Exempel:

```objective-c
//create a context data dictionary 
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
 
// add events 
[contextData setObject:@"event1:12341234" forKey:@"&&events"]; 
 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
[ADBMobile trackAction:@"action" data:contextData]; 
// trackState example: 
[ADBMobile trackState:@"State Name" data:contextData]; 
```

