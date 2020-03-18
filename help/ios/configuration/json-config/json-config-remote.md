---
description: Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.
seo-description: Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.
seo-title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
solution: Marketing Cloud,Analytics
title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
topic: Developer and implementation
uuid: 0d1be674-c634-4a48-aa31-5701681911b9
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Åsidosätt ADBMomobile JSON-konfigurationssökvägen {#override-the-adbmobile-json-config-path}

Du kan läsa in en annan ADBMomobile JSON Config-fil när programmet startas.

Med den här `ADBMobile overrideConfigPath:filePath` metoden kan du ange sökvägen till en annan `ADBMobile.json` konfigurationsfil när programmet startas. Den här metoden måste anropas i `applicationDidFinishLaunchingWithOptions` metoden och anropet måste ske före andra Experience Cloud SDK-anrop, till exempel `collectLifecycleData`.

När du anropar den här metoden med en annan sökväg sker en engångsåsidosättning av konfigurationsfilen tills programmet stängs.

Exempel:

```objective-c
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile" ofType:@"json"]; 
[ADBMobile overrideConfigPath:filePath];
```

