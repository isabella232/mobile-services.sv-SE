---
description: Om användaren trycker på en grupp kan program som har aktiverat offlinespårning hindra att träffar skickas tills antalet träffar i kön når en konfigurerbar gräns.
seo-description: Om användaren trycker på en grupp kan program som har aktiverat offlinespårning hindra att träffar skickas tills antalet träffar i kön når en konfigurerbar gräns.
seo-title: Träffa
solution: Experience Cloud,Analytics
title: Träffa
topic-fix: Developer and implementation
uuid: 3dda7372-0695-4cb7-b779-6abca2d6e0d9
exl-id: af21f435-13cb-4353-9fbb-c99274bce411
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Tryck på batchvis {#hit-batching}

Om användaren trycker på en grupp kan program som har aktiverat offlinespårning hindra att träffar skickas tills antalet träffar i kön når en konfigurerbar gräns.

>[!IMPORTANT]
>
>Gruppering kräver SDK version 4.1 eller senare.

Uppdatera din `ADBMobileConfig.json`-fil och ange ett värde för `batchLimit` om du vill aktivera träffbatchbearbetning:

```js
"analytics": {
    "batchLimit": 5,
    ...
}
```

Om värdet är ett tal som är högre än 0 köar SDK antalet träffar som är lika med *`batchLimit`*. När det här tröskelvärdet har passerats skickas alla träffar i kön.

Följande metoder används för gruppbearbetning av träffar:

* `trackingGetQueueSize()` returnerar ett värde  `NSUInteger` med antalet träffar i gruppbearbetningskön.
* `trackingSendQueuedHits()` tvingar biblioteket att skicka alla träffar i kön oavsett hur många som står i kö.
* `trackingClearQueue()` tar bort alla träffar från kön utan att skicka dem.

>[!CAUTION]
>
>Spårning offline måste vara aktiverat om du vill använda träffbatchning.
