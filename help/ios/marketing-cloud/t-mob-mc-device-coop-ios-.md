---
description: Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.
seo-description: Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.
seo-title: Experience Cloud Device Co-op
title: Experience Cloud Device Co-op
uuid: 434a6f8f-ec24-439d-95f0-a246b384b3b5
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Experience Cloud Device Co-op {#experience-cloud-device-co-op}

Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.

Om du vill aktivera dina mobilappar för Experience Cloud Device Co-op utför du följande steg för Experience Cloud iOS SDK:er.

>[!IMPORTANT]
>
>Den här funktionen kräver iOS SDK version 4.8.5 eller senare.

Från och med SDK version 4.16.1 kan medlemmar i Device Co-op välja sina mobilenhetsdata från Experience Cloud Device Co-op. Mer information finns i [ADBMomobile JSON Config](/help/ios/configuration/json-config/json-config.md) och `visitorAPI.js` metoden för [isCoopSafe](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-coopsafe.html).

1. Implementera Adobe Mobile SDK.

   Mer information finns i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Aktivera ditt Experience Cloud ID.

   Mer information finns i [Experience Cloud ID](/help/ios/marketing-cloud/mcvid.md).
1. Skicka autentiserade identiteter som CRM-ID:n eller hash-kodade e-postmeddelanden med någon av de synkroniseringsmetoder som finns här.

   Mer information finns i [Adobe Experience Platform Identity Service-metoder](/help/ios/marketing-cloud/mc-methods.md).

## `coopUnsafe` flagga

Här finns ytterligare information om `coopUnsafe` flaggan:

* Minsta SDK-version: 4.16.1
* Den booleska egenskapen för det objekt `marketingCloud` som, när den är inställd på `true`det, gör att enheten avanmäts från Device Co-Op i Experience Cloud.
* Standardvärdet är `false`.
* Den här inställningen används **endast** för Device Co-op-etablerade kunder.

För medlemmar i Device Co-op som kräver det här värdet måste du `true`arbeta med Co-op-teamet för att begära en svartlistningsflagga på ditt Device Co-op-konto. Det finns ingen självbetjäningsväg för att aktivera dessa flaggor.

Kom ihåg följande information:

* När `coopUnsafe` är inställt på `true`läggs `coop_unsafe=1` alltid till i träffar för Audience Manager och Visitor ID.
* Om du aktiverar vidarebefordran på serversidan för Analytics till Audience Manager kan du även se `coop_unsafe=1` Analytics-träffar.


