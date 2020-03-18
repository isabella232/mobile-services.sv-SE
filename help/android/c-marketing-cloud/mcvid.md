---
description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida Experience Cloud-integreringar.
seo-description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida Experience Cloud-integreringar.
seo-title: Experience Cloud ID-konfiguration
solution: Marketing Cloud,Analytics
title: Experience Cloud ID-konfiguration
topic: Developer and implementation
uuid: 8ebdf2bf-c581-448f-9542-f99a19784fe7
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Experience Cloud ID-konfiguration {#experience-cloud-id-configuration}

Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida Experience Cloud-integreringar.

>[!TIP]
>
>Du behöver inte fylla i detta ID om du inte använder Adobe Experience Platform Identity Service. Mer information finns i [Adobe Experience Platform Identity Service](https://marketing.adobe.com/resources/help/en_US/mcvid/).

>[!IMPORTANT]
>
>Den här funktionen kräver SDK version 4.3 eller senare.

Så här aktiverar du Experience Cloud-ID:

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Kontrollera att `ADBMobileConfig.json` filen innehåller `marketingCloudorg`:

   ```js
   "marketingCloud" : { 
     "org": "YOUR-MCORG-ID" 
   }
   ```

   Organisations-ID för Experience Cloud identifierar unikt varje klientföretag i Adobe Experience Cloud och liknar följande värde:

   ```js
   016D5C175213CCA80A490D05@AdobeOrg`
   ```

   >[!IMPORTANT]
   >
   >Du måste inkludera `@AdobeOrg`.

   Om dessa ID:n inte har konfigurerats hämtar du en uppdaterad `ADBMobileConfig.json` fil från Adobe Mobile Services. Mer information finns i [Innan du börjar](/help/android/getting-started/requirements.md).

När konfigurationen är klar genereras ett Experience Cloud-ID som ingår i alla träffar. Andra ID:n, till exempel anpassade och automatiskt genererade ID:n, fortsätter att skickas med varje träff.
