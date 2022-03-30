---
description: Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.
solution: Experience Cloud Services,Analytics
title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
topic-fix: Developer and implementation
uuid: 0d1be674-c634-4a48-aa31-5701681911b9
exl-id: 3a191e9c-905f-4bea-8a6f-5ccf5ea02aff
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 1%

---

# Åsidosätt ADBMomobile JSON-konfigurationssökvägen {#override-the-adbmobile-json-config-path}

Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.

The `ADBMobile overrideConfigPath:filePath` kan du ange sökvägen till en annan `ADBMobile.json` konfigurationsfilen när programmet startas. Den här metoden måste anropas i `applicationDidFinishLaunchingWithOptions` och anropet måste ske före andra Experience Cloud SDK-anrop, som `collectLifecycleData`.

När du anropar den här metoden med en annan sökväg sker en engångsåsidosättning av konfigurationsfilen tills programmet stängs.

Exempel:

```objective-c
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile" ofType:@"json"]; 
[ADBMobile overrideConfigPath:filePath];
```
