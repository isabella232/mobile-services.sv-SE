---
description: Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.
title: Experience Cloud Device Co-op
uuid: 434a6f8f-ec24-439d-95f0-a246b384b3b5
exl-id: bf4f7a81-152c-4033-bcdf-22a939a3109e
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 2%

---

# Experience Cloud Device Co-op {#experience-cloud-device-co-op}

Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.

Om du vill aktivera dina mobilappar för Experience Cloud Device Co-op utför du följande steg för iOS SDK:n för Experience Cloud.

>[!IMPORTANT]
>
>Den här funktionen kräver iOS SDK version 4.8.5 eller senare.

Med början från SDK version 4.16.1 kan medlemmar i Device Co-op välja sina mobilenhetsdata från Experience Cloud Device Co-op. Mer information finns i [ADBMomobile JSON Config](/help/ios/configuration/json-config/json-config.md) och `visitorAPI.js`-metoden för [isCoopSafe](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/coopsafe.html) i dokumentationen för Adobe Experience Cloud identitetstjänst.

1. Implementera Adobe Mobile SDK.

   Mer information finns i [Core Implementation and Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Aktivera ditt Experience Cloud-ID.

   Mer information finns i [Experience Cloud ID](/help/ios/marketing-cloud/mcvid.md).
1. Skicka autentiserade identiteter som CRM-ID:n eller hash-kodade e-postmeddelanden med någon av de synkroniseringsmetoder som finns här.

   Mer information finns i [Adobe Experience Platform Identity Service Methods](/help/ios/marketing-cloud/mc-methods.md).

## `coopUnsafe` flagga

Här finns ytterligare information om flaggan `coopUnsafe`:

* Minsta SDK-version: 4.16.1
* Den booleska egenskapen för `marketingCloud`-objektet som, när det är inställt på `true`, gör att enheten avanmäls från Experience Cloud Device Co-Op.
* Standardvärdet är `false`.
* Den här inställningen används **endast** för Device Co-op-etablerade kunder.

För medlemmar i Device Co-op som kräver det här värdet inställt på `true` måste du arbeta med Co-op-teamet för att begära en blockeringslista-flagga på ditt Device Co-op-konto. Det finns ingen självbetjäningsväg för att aktivera dessa flaggor.

Kom ihåg följande information:

* När `coopUnsafe` är inställt på `true` läggs `coop_unsafe=1` alltid till i Audience Manager och besökar-ID-träffar.
* Om du aktiverar vidarebefordran på serversidan för Analytics till Audience Manager visas även `coop_unsafe=1` om Analytics-träffar.
