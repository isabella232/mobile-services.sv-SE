---
description: Du kan läsa in en annan ADBMomobile JSON-konfigurationsfil när programmet startas.
seo-description: Du kan läsa in en annan ADBMomobile JSON-konfigurationsfil när programmet startas.
seo-title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
solution: Experience Cloud,Analytics
title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
topic: Developer and implementation
uuid: 6872a5d7-0c5a-4fdc-b7bf-ad1534763a6a
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Åsidosätt ADBMomobile JSON-konfigurationssökvägen {#override-the-adbmobile-json-config-path}

Du kan läsa in en annan ADBMomobile JSON-konfigurationsfil när programmet startas.

Med den här `Config.overrideConfigStream(configInput)` metoden kan du ange sökvägen till en annan `ADBMobile.json` konfigurationsfil när programmet startas. Den här metoden måste anropas före alla andra Experience Cloud SDK-anrop (före `Config.collectLifecycleData()` ), vanligtvis i den metod som `onCreate` används för den första inlästa aktiviteten.

Om du anropar den här metoden med en annan sökväg åsidosätts konfigurationsfilen en gång tills programmet stängs.

```java
 try { 
   InputStream configInput = getAssets().open("ExampleJSONFile.json"); 
   Config.overrideConfigStream(configInput); 
   } catch (IOException ex) { 
   // do something with the exception if needed 
}
```

