---
description: Om du trycker på gruppering kan program stoppa träffar från att skickas tills antalet träffar i kön har överskridit den konfigurerade gränsen.
keywords: android;library;mobile;sdk
seo-description: Om du trycker på gruppering kan program stoppa träffar från att skickas tills antalet träffar i kön har överskridit den konfigurerade gränsen.
seo-title: Träffa
solution: Experience Cloud,Analytics
title: Träffa
topic: Developer and implementation
uuid: ada35be3-242b-4b2b-a828-9bf998dd58b5
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Träffa {#hit-batching}

Om du trycker på gruppering kan program stoppa träffar från att skickas tills antalet träffar i kön har överskridit den konfigurerade gränsen.

>[!IMPORTANT]
>
>Om du vill använda träffbatchning **måste** du aktivera offlinespårning och ha SDK version 4.1 eller senare

Om du vill aktivera träffgrupper uppdaterar du din `ADBMobileConfig.json` fil och anger ett värde för `batchLimit`:

```js
"analytics": {
    "batchLimit": 5,
    ...
}
```

När värdet är större än 0 köar SDK antalet träffar som är lika med *`batchLimit`* värdet. När det här tröskelvärdet har passerats skickas alla träffar i kön.

Följande metoder används för gruppbearbetning av träffar:

* `Analytics.getQueueSize` returnerar ett värde `long` med antalet träffar i gruppbearbetningskön.

* `Analytics.sendQueuedHits` tvingar biblioteket att skicka alla träffar i kön oavsett hur många träffar som står i kö.
* `Analytics.clearQueue` tar bort alla träffar från kön utan att skicka dem.
