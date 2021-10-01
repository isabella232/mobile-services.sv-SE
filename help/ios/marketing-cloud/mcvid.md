---
description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida integreringar med Experience Cloud.
solution: Experience Cloud,Analytics
title: Experience Cloud ID
topic-fix: Developer and implementation
uuid: 13628ea8-3cd4-4cfc-8ff6-722c33f7813a
exl-id: aa7db365-ad21-431f-bff6-2a6da212dd0c
source-git-commit: d1ebb2bbc4742f5288f90a90e977d252f3f30aa3
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Experience Cloud ID {#experience-cloud-id}

Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida integreringar med Experience Cloud.

>[!TIP]
>
>Du behöver inte fylla i Experience Cloud-ID om du inte använder Adobe Experience Platform identitetstjänst. Mer information finns i dokumentationen till [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html).

## Aktivera Experience Cloud-ID {#section_79F984271C3B4366B7B04F864F4FF8C2}

Dessa steg kräver en SDK version 4.3 eller senare.

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i ditt projekt* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Kontrollera att `ADBMobileConfig.json`-filerna innehåller `marketingCloud` `org`:

   ```js
   "marketingCloud" : { 
     "org": "YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organisations-ID:n är unika för alla klientföretag i Adobe Experience Cloud och liknar följande värde: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Du måste inkludera `@AdobeOrg`.

   Om dessa värden inte finns kan du hämta en uppdaterad `ADBMobileConfig.json`-fil från Adobe Mobile-tjänster. Mer information finns i [ADBMomobile JSON config](/help/ios/getting-started/requirements.md).

Efter konfigurationen genereras ett Experience Cloud-ID och inkluderas i alla träffar. Andra besökar-ID:n, som anpassade och automatiskt genererade, kommer att fortsätta skickas med varje träff.
