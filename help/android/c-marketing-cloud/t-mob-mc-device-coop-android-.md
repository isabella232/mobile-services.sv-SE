---
description: Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.
seo-description: Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.
seo-title: Experience Cloud Device Co-op
title: Experience Cloud Device Co-op
uuid: 7bb8a19c-4b80-4911-879d-f9941baa3b62
translation-type: tm+mt
source-git-commit: 86ba045b44bf6553e80727c0d61ccdd9a552d16c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---


# Experience Cloud Device Co-op {#experience-cloud-device-co-op}

Kontakta din Adobe-representant om du vill börja använda Experience Cloud Device Co-op.

Om du vill aktivera dina mobilappar för Experience Cloud Device Co-op utför du följande steg för Android SDK:n i Experience Cloud:

>[!IMPORTANT]
>
>Den här funktionen kräver Android SDK version 4.8.3 eller senare.

Med början från SDK version 4.16.1 kan medlemmar i Device Co-op välja sina mobilenhetsdata från Experience Cloud Device Co-op. Mer information finns i [ADBMomobile JSON Config](/help/android/configuration/json-config/json-config.md) och `visitorAPI.js` metoden för [isCoopSafe](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/configurations/coopsafe.html).

1. Implementera Adobe Mobile SDK.

   Mer information finns i [Core Implementation och Lifecycle](/help/android/getting-started/dev-qs.md).
1. Aktivera ditt Experience Cloud-ID.

   Mer information finns i [Experience Cloud ID-konfiguration](/help/android/c-marketing-cloud/mcvid.md).
1. Skicka autentiserade identiteter som CRM-ID:n eller hashad e-post med någon av synkroniseringsmetoderna.

   Mer information finns i [Adobe Experience Platform Identity Service-metoder](/help/android/c-marketing-cloud/mc-methods.md).

## `coopUnsafe` flagga

Här finns ytterligare information om `coopUnsafe` flaggan:

* Minsta SDK-version: 4.16.1
* Den booleska egenskapen för det objekt `marketingCloud` som, när den är inställd på `true`, gör att enheten väljs ut från Experience Cloud Device Co-Op.
* Standardvärdet är `false`.
* Den här inställningen används **endast** för Device Co-op-etablerade kunder.

För medlemmar i Device Co-op som kräver det här värdet `true`måste du arbeta med Co-op-teamet för att begära en blockeringslista-flagga på ditt Device Co-op-konto. Det finns ingen självbetjäningsväg för att aktivera dessa flaggor.

Kom ihåg följande information:

* När `coopUnsafe` är inställt på `true`läggs `coop_unsafe=1` alltid till i Audience Manager och i besöks-ID-träffar.
* Om du aktiverar vidarebefordran på serversidan för Analytics till Audience Manager visas även `coop_unsafe=1` Analytics-träffar.