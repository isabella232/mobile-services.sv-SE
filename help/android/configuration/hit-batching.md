---
description: Om du trycker på gruppering kan program stoppa träffar från att skickas tills antalet träffar i kön har överskridit den konfigurerade gränsen.
keywords: android;bibliotek;mobil;sdk
seo-description: Om du trycker på gruppering kan program stoppa träffar från att skickas tills antalet träffar i kön har överskridit den konfigurerade gränsen.
seo-title: Träffa
solution: Experience Cloud,Analytics
title: Träffa
topic-fix: Developer and implementation
uuid: ada35be3-242b-4b2b-a828-9bf998dd58b5
exl-id: 74147f09-52fc-46dc-b4dd-2bf60b039f6e
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Tryck på batchvis {#hit-batching}

Om du trycker på gruppering kan program stoppa träffar från att skickas tills antalet träffar i kön har överskridit den konfigurerade gränsen.

>[!IMPORTANT]
>
>Om du vill använda träffgruppering måste du **aktivera offlinespårning och ha SDK version 4.1 eller senare**

Uppdatera din `ADBMobileConfig.json`-fil och ange ett värde för `batchLimit` om du vill aktivera träffbatchbearbetning:

```js
"analytics": {
    "batchLimit": 5,
    ...
}
```

När värdet är större än 0 köar SDK antalet träffar som är lika med *`batchLimit`*-värdet. När det här tröskelvärdet har passerats skickas alla träffar i kön.

Följande metoder används för gruppbearbetning av träffar:

* `Analytics.getQueueSize` returnerar en  `long` med antalet träffar i gruppbearbetningskön.

* `Analytics.sendQueuedHits` tvingar biblioteket att skicka alla träffar i kön oavsett hur många träffar som står i kö.
* `Analytics.clearQueue` tar bort alla träffar från kön utan att skicka dem.
