---
description: Du kan skapa och hantera intressepunkter, som gör att du kan definiera geografiska platser som du kan använda för korrelationssyften, mål med meddelanden i appen och så vidare. När en träff skickas i en intressepunkt kopplas den till träffen.
keywords: mobile
seo-description: Du kan skapa och hantera intressepunkter, som gör att du kan definiera geografiska platser som du kan använda för korrelationssyften, mål med meddelanden i appen och så vidare. När en träff skickas i en intressepunkt kopplas den till träffen.
seo-title: Hantera intressepunkter
solution: Marketing Cloud,Analytics
title: Hantera intressepunkter
topic: Metrics
uuid: 7b362534-54fb-43a3-b6b2-dfc8f45ff7c6
translation-type: tm+mt
source-git-commit: d028fe0f9477bc011aa8fda21a0a389808df0fce

---


# Hantera intressepunkter {#manage-points-of-interest}

Du kan skapa och hantera POI:er, som gör att du kan definiera geografiska platser som du kan använda för korrelationssyften, rikta dig mot meddelanden i appen och så vidare. När en träff skickas i en POI kopplas POI till träffen.

Kontrollera följande krav innan du kan använda Plats:

* Ni måste ha Analytics - Mobile Apps eller Analytics Premium.
* Du måste aktivera **[!UICONTROL Location Reports]** för appen.
* Om du använder en version av iOS SDK eller Android SDK som är äldre än version 4.2 måste du hämta en ny konfigurationsfil och ge den till programutvecklarna när du har lagt till ny **[!UICONTROL Points of Interest]** version.

   Om du använder iOS SDK eller Android SDK version 4.2 eller senare behöver du inte skicka in någon appuppdatering till butiken för att uppdatera din **[!UICONTROL Points of Interest]**. När du klickar **[!UICONTROL Save]** på sidan Hantera intressepunkter paketeras ändringarna i **[!UICONTROL Points of Interest]** listan och konfigurationsfilen för live-appen uppdateras. När du sparar uppdateras även listan med punkter i appen på användarenheterna, så länge appen använder den uppdaterade SDK:n och konfigurationen med en fjärr-POI-URL.

För att en träff ska tilldelas till en användare på användarens enhet **[!UICONTROL Points of Interest]** måste platsen aktiveras för appen.

Gör så här om du vill använda Plats:

1. Klicka på appens namn för att gå till sidan Hantera appinställningar.
1. Klicka på **[!UICONTROL Location]** > **[!UICONTROL Manage Points of Interest]**.

   ![Stegresultat](assets/poi.png)

1. Skriv informationen i följande fält:

   * **[!UICONTROL Point Name]**

      Skriv **[!UICONTROL Point of Location]** namnet.

      Det kan vara namnet på en stad, ett land eller en region. Du kan också skapa en **[!UICONTROL Point of Location]** runt vissa platser, till exempel sportarenor eller företag.

   * **[!UICONTROL Latitude ]**

      Ange latituden för **[!UICONTROL Point of Location]** objektet. Den här informationen finns från andra källor, bland annat Internet.

   * **[!UICONTROL Longitude]**

      Skriv in longituden för **[!UICONTROL Point of Location]**. Den här informationen finns från andra källor, bland annat Internet.

   * **[!UICONTROL Radius (Meters)]**

      Skriv radien (i meter) runt den **[!UICONTROL Point of Location]** som du vill ta med. Om du till exempel skapar en POI för Denver, Colorado, kan du ange en radie som är tillräckligt stor för att inkludera staden Denver och de omgivande områdena, men exkludera Colorado-strängar.

   * **[!UICONTROL Map Icon]**

      Välj en ikon som ska visas i [översikts](/help/using/location/c-location-overview.md) - och [kartrapporterna](/help/using/location/c-map-points.md) .

1. Lägg till ytterligare POI efter behov.

   Vi rekommenderar att du inte lägger till fler än 5 000 POI. Om du lägger till fler än 5 000 kan du spara punkterna, men du får ett varningsmeddelande som informerar dig om att bästa praxis innebär att färre än 5 000 poäng används.

1. Klicka på **[!UICONTROL Save]**.

Om du vill ta bort en eller flera POI:er markerar du de tillämpliga kryssrutorna och klickar på **[!UICONTROL Remove Selected]**.

Klicka **[!UICONTROL Import]** eller **[!UICONTROL Export]** för att arbeta med data genom att använda en `.csv` fil i stället för att använda användargränssnittet i Adobe Mobile.
