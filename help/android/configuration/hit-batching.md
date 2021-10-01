---
description: Om du trycker på gruppering kan program stoppa träffar från att skickas tills antalet träffar i kön har överskridit den konfigurerade gränsen.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Träffa
topic-fix: Developer and implementation
uuid: ada35be3-242b-4b2b-a828-9bf998dd58b5
exl-id: 74147f09-52fc-46dc-b4dd-2bf60b039f6e
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Träffa {#hit-batching}

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
