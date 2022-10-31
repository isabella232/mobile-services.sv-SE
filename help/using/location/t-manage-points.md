---
description: Du kan skapa och hantera intressepunkter, som gör att du kan definiera geografiska platser som du kan använda för korrelationssyften, mål med meddelanden i appen och så vidare. När en träff skickas i en intressepunkt kopplas den till träffen.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Hantera intressepunkter
topic-fix: Metrics
uuid: 7b362534-54fb-43a3-b6b2-dfc8f45ff7c6
exl-id: 9598b06b-fb6a-436c-811c-f74015cc2ab0
source-git-commit: 7cfaa5f6d1318151e87698a45eb6006f7850aad4
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---

# Hantera intressepunkter {#manage-points-of-interest}

{#eol}

Du kan skapa och hantera POI:er, som gör att du kan definiera geografiska platser som du kan använda för korrelationssyften, rikta dig mot meddelanden i appen och så vidare. När en träff skickas i en POI kopplas POI till träffen.

Kontrollera följande krav innan du kan använda Plats:

* Ni måste ha Analytics - Mobile Apps eller Analytics Premium.
* Du måste aktivera **[!UICONTROL Location Reports]** för appen.
* Om du använder en version av iOS SDK eller Android SDK som är äldre än version 4.2, efter att ha lagt till ny **[!UICONTROL Points of Interest]** måste du hämta en ny konfigurationsfil och ge den till programutvecklarna.

   Om du använder iOS SDK eller Android SDK version 4.2 eller senare behöver du inte skicka in någon appuppdatering till butiken för att uppdatera din **[!UICONTROL Points of Interest]**. På sidan Hantera intressepunkter klickar du på **[!UICONTROL Save]**, sparas ändringarna i **[!UICONTROL Points of Interest]** -listan och konfigurationsfilen för live-appen uppdateras. När du sparar uppdateras även listan med punkter i appen på användarenheterna, så länge appen använder den uppdaterade SDK:n och konfigurationen med en fjärr-POI-URL.

På användarens enhet, för att en träff ska tilldelas en **[!UICONTROL Points of Interest]** måste platsen vara aktiverad för programmet.

Gör så här om du vill använda Plats:

1. Klicka på appens namn för att gå till sidan Hantera appinställningar.
1. Klicka på **[!UICONTROL Location]** > **[!UICONTROL Manage Points of Interest]**.

   ![Stegresultat](assets/poi.png)

1. Skriv informationen i följande fält:

   * **[!UICONTROL Point Name]**

      Skriv **[!UICONTROL Point of Location]** namn.

      Det kan vara namnet på en stad, ett land eller en region. Du kan också skapa en **[!UICONTROL Point of Location]** omkring specifika platser, t.ex. idrottsarenor eller företag.

   * **[!UICONTROL Latitude ]**

      Ange latituden för **[!UICONTROL Point of Location]**. Den här informationen finns från andra källor, bland annat Internet.

   * **[!UICONTROL Longitude]**

      Ange longituden för **[!UICONTROL Point of Location]**. Den här informationen finns från andra källor, bland annat Internet.

   * **[!UICONTROL Radius (Meters)]**

      Ange radien (i meter) runt **[!UICONTROL Point of Location]** som du vill ta med. Om du till exempel skapar en POI för Denver, Colorado, kan du ange en radie som är tillräckligt stor för att inkludera staden Denver och de omgivande områdena, men exkludera Colorado-strängar.

   * **[!UICONTROL Map Icon]**

      Välj en ikon som ska visas på [Översikt](/help/using/location/c-location-overview.md) och [Karta](/help/using/location/c-map-points.md) rapporter.

1. Lägg till ytterligare POI efter behov.

   Vi rekommenderar att du inte lägger till fler än 5 000 POI. Om du lägger till fler än 5 000 kan du spara punkterna, men du får ett varningsmeddelande som informerar dig om att bästa praxis innebär att färre än 5 000 poäng används.

1. Klicka på **[!UICONTROL Save]**.

Om du vill ta bort en eller flera POI:er markerar du de tillämpliga kryssrutorna och klickar på **[!UICONTROL Remove Selected]**.

Klicka **[!UICONTROL Import]** eller **[!UICONTROL Export]** arbeta med data genom att använda en `.csv` i stället för att använda användargränssnittet för Adobe Mobile.
