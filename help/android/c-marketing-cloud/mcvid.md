---
description: Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida integreringar med Experience Cloud.
solution: Experience Cloud,Analytics
title: Experience Cloud ID-konfiguration
topic-fix: Developer and implementation
uuid: 8ebdf2bf-c581-448f-9542-f99a19784fe7
exl-id: 97dc6768-bf31-4a0d-a460-9caf9ecda5fb
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Experience Cloud ID-konfiguration {#experience-cloud-id-configuration}

Adobe Experience Platform Identity Service tillhandahåller ett universellt besökar-ID för alla Experience Cloud-lösningar. ID-tjänsten krävs av Analytics för Target, hjärtslag för video och framtida integreringar med Experience Cloud.

>[!TIP]
>
>Du behöver inte fylla i detta ID om du inte använder Adobe Experience Platform identitetstjänst. Mer information finns i [Adobe Experience Platform identitetstjänst](https://experienceleague.adobe.com/docs/id-service/using/home.html).

>[!IMPORTANT]
>
>Den här funktionen kräver SDK version 4.3 eller senare.

Så här aktiverar du Experience Cloud-ID:

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Kontrollera att `ADBMobileConfig.json`-filen innehåller `marketingCloudorg`:

   ```js
   "marketingCloud" : { 
     "org": "YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organisations-ID:n är unika för alla klientföretag i Adobe Experience Cloud och liknar följande värde:

   ```js
   016D5C175213CCA80A490D05@AdobeOrg`
   ```

   >[!IMPORTANT]
   >
   >Du måste inkludera `@AdobeOrg`.

   Om dessa ID:n inte har konfigurerats hämtar du en uppdaterad `ADBMobileConfig.json`-fil från Adobe Mobile-tjänster. Mer information finns i [Innan du startar](/help/android/getting-started/requirements.md).

När konfigurationen är klar genereras ett Experience Cloud-ID som ingår i alla träffar. Andra ID:n, till exempel anpassade och automatiskt genererade ID:n, fortsätter att skickas med varje träff.
