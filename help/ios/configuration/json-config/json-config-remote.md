---
description: Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.
seo-description: Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.
seo-title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
solution: Experience Cloud,Analytics
title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
topic-fix: Developer and implementation
uuid: 0d1be674-c634-4a48-aa31-5701681911b9
exl-id: 3a191e9c-905f-4bea-8a6f-5ccf5ea02aff
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 1%

---

# Åsidosätt ADBMomobile JSON-konfigurationssökvägen {#override-the-adbmobile-json-config-path}

Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.

Med metoden `ADBMobile overrideConfigPath:filePath` kan du ange sökvägen till en annan `ADBMobile.json`-konfigurationsfil när programmet startas. Den här metoden måste anropas i metoden `applicationDidFinishLaunchingWithOptions` och anropet måste ske före andra Experience Cloud SDK-anrop, till exempel `collectLifecycleData`.

När du anropar den här metoden med en annan sökväg sker en engångsåsidosättning av konfigurationsfilen tills programmet stängs.

Exempel:

```objective-c
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile" ofType:@"json"]; 
[ADBMobile overrideConfigPath:filePath];
```
