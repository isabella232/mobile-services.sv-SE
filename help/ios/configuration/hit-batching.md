---
description: Om användaren trycker på en grupp kan program som har aktiverat offlinespårning hindra att träffar skickas tills antalet träffar i kön når en konfigurerbar gräns.
seo-description: Om användaren trycker på en grupp kan program som har aktiverat offlinespårning hindra att träffar skickas tills antalet träffar i kön når en konfigurerbar gräns.
seo-title: Träffa
solution: Experience Cloud,Analytics
title: Träffa
topic: Developer and implementation
uuid: 3dda7372-0695-4cb7-b779-6abca2d6e0d9
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Träffa {#hit-batching}

Om användaren trycker på en grupp kan program som har aktiverat offlinespårning hindra att träffar skickas tills antalet träffar i kön når en konfigurerbar gräns.

>[!IMPORTANT]
>
>Gruppering kräver SDK version 4.1 eller senare.

Om du vill aktivera träffgrupper uppdaterar du din `ADBMobileConfig.json` fil och anger ett värde för `batchLimit`:

```js
"analytics": {
    "batchLimit": 5,
    ...
}
```

Om värdet är ett tal som är högre än 0 köas antalet träffar som är lika med *`batchLimit`*. När det här tröskelvärdet har passerats skickas alla träffar i kön.

Följande metoder används för gruppbearbetning av träffar:

* `trackingGetQueueSize()` returnerar ett värde `NSUInteger` med antalet träffar i gruppbearbetningskön.
* `trackingSendQueuedHits()` tvingar biblioteket att skicka alla träffar i kön oavsett hur många som står i kö.
* `trackingClearQueue()` tar bort alla träffar från kön utan att skicka dem.

>[!CAUTION]
>
>Spårning offline måste vara aktiverat om du vill använda träffbatchning.

