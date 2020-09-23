---
description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida integreringar med Experience Cloud.
seo-description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida integreringar med Experience Cloud.
seo-title: Experience Cloud ID
solution: Experience Cloud,Analytics
title: Experience Cloud ID
topic: Developer and implementation
uuid: 13628ea8-3cd4-4cfc-8ff6-722c33f7813a
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---


# Experience Cloud ID {#experience-cloud-id}

Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida integreringar med Experience Cloud.

>[!TIP]
>
>Du behöver inte fylla i Experience Cloud-ID om du inte använder Adobe Experience Platform identitetstjänst. Mer information finns i [Adobe Experience Platform identitetstjänst](https://docs.adobe.com/content/help/sv-SE/id-service/using/home.html).

**Kräver SDK version 4.3 eller senare**

## Enable the Experience Cloud ID {#section_79F984271C3B4366B7B04F864F4FF8C2}

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

   Experience Cloud organisations-ID:n är unika för alla klientföretag i Adobe Experience Cloud och liknar följande värde: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Du måste inkludera `@AdobeOrg`.

   Om dessa värden inte finns kan du hämta en uppdaterad `ADBMobileConfig.json` fil från Adobe Mobile Services. Mer information finns i [ADBMomobile JSON-konfiguration](/help/ios/getting-started/requirements.md).

Efter konfigurationen genereras ett Experience Cloud-ID och inkluderas i alla träffar. Andra besökar-ID:n, som anpassade och automatiskt genererade, kommer att fortsätta skickas med varje träff.
