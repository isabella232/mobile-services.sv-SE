---
description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida Experience Cloud-integreringar.
seo-description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida Experience Cloud-integreringar.
seo-title: Experience Cloud-ID
solution: Marketing Cloud,Analytics
title: Experience Cloud-ID
topic: Developer and implementation
uuid: 13628ea8-3cd4-4cfc-8ff6-722c33f7813a
translation-type: tm+mt
source-git-commit: 82b3dc38a0325b3aa733b491ddad9b59dbe84eaa

---


# Experience Cloud-ID {#experience-cloud-id}

Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida Experience Cloud-integreringar.

>[!TIP]
>
>Du behöver inte fylla i Experience Cloud-ID om du inte använder Adobe Experience Platform Identity Service. Mer information finns i [Adobe Experience Platform Identity Service](https://docs.adobe.com/content/help/en/id-service/using/home.html).

**Kräver SDK version 4.3 eller senare**

## Aktivera Experience Cloud-ID {#section_79F984271C3B4366B7B04F864F4FF8C2}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Kontrollera att `ADBMobileConfig.json` filerna innehåller `marketingCloud``org`:

   ```js
   "marketingCloud" : { 
     "org": "YOUR-MCORG-ID" 
   }
   ```

   Organisations-ID för Experience Cloud identifierar unikt varje klientföretag i Adobe Experience Cloud och liknar följande värde: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Du måste inkludera `@AdobeOrg`.

   Om dessa värden saknas hämtar du en uppdaterad `ADBMobileConfig.json` fil från Adobe Mobile Services. Mer information finns i [ADBMomobile JSON-konfiguration](/help/ios/getting-started/requirements.md).

Efter konfigurationen genereras ett Experience Cloud-ID som ingår i alla träffar. Andra besökar-ID:n, som anpassade och automatiskt genererade, kommer att fortsätta skickas med varje träff.
