---
description: Du kan läsa in en annan ADBMomobile JSON-konfigurationsfil när programmet startas.
solution: Experience Cloud Services,Analytics
title: Åsidosätt ADBMomobile JSON-konfigurationssökvägen
topic-fix: Developer and implementation
uuid: 6872a5d7-0c5a-4fdc-b7bf-ad1534763a6a
exl-id: 6ca8e264-af79-4734-aeb9-824582980953
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Åsidosätt ADBMomobile JSON-konfigurationssökvägen {#override-the-adbmobile-json-config-path}

Du kan läsa in en annan ADBMomobile JSON-konfigurationsfil när programmet startas.

The `Config.overrideConfigStream(configInput)` kan du ange sökvägen till en annan `ADBMobile.json` konfigurationsfilen när programmet startas. Den här metoden måste anropas före andra Experience Cloud SDK-anrop (före `Config.collectLifecycleData()` ), vanligtvis i `onCreate` metod för den första inlästa aktiviteten.

Om du anropar den här metoden med en annan sökväg åsidosätts konfigurationsfilen en gång tills programmet stängs.

```java
 try { 
   InputStream configInput = getAssets().open("ExampleJSONFile.json"); 
   Config.overrideConfigStream(configInput); 
   } catch (IOException ex) { 
   // do something with the exception if needed 
}
```
