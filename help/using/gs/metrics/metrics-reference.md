---
description: Här är referensinformationen för standardvärden och -dimensioner för mobila enheter.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Mobile Metrics and Dimensions Reference
topic-fix: Metrics
uuid: 96170ae7-8553-4f3e-ae01-65e5b664adf4
exl-id: ddfbf11e-a4c3-4d59-92b3-1d192dc3e7cd
source-git-commit: dbe3af75010fbf5195a3f93fc43cb696aaa32b65
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---

# Mobilstatistik och dimensionsreferens {#mobile-metrics-and-dimensions-reference}

Den här informationen hjälper dig att förstå mer om standardvärden och -dimensioner för mobila enheter.

>[!TIP]
>
>Dimensions- och måttbehörigheterna som anges i Adobe Analytics gäller för mobiltjänster. När du försöker köra en rapport utan rätt behörigheter inträffar ett fel.

## Mätvärden {#section_6704C815147D44AF96151D626BEB813C}

Här är en lista över standardvärden för mobiler:

* **Första starten**

   Utlöses första gången efter en installation eller ominstallation.

* **Uppgraderingar**

   Utlöses första körningen efter en uppgradering eller när versionsnumret ändras.

* **Dagliga engagerade användare**

   Utlöses när programmet används en viss dag.

   >[!TIP]
   >
   >Händelsen Daglig engagerad användare lagras inte automatiskt i ett analysmått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

* **Engagerade användare varje månad**

   Utlöses när programmet används under en månad.

   >[!TIP]
   >Händelsen för Månadsengagerade användare lagras inte automatiskt i ett analysmått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

* **Launches**

   Utlöses på en körning som inte är en installation eller uppgradering. Detta utlöses också när programmet tas bort från bakgrunden. Som standard utlöses en ny start när programmet är i bakgrunden i fem eller fler minuter. Mängden bakgrundstid innan en ny start aktiveras kan konfigureras i **[!UICONTROL SDK Analytics Options]** på sidan Hantera appinställningar. Mer information finns i *Tidsgräns för session (sekunder)* rad in [Konfigurera alternativ för SDK-analys](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-analytics/t-config-analytics.md).

   >[!IMPORTANT]
   >På grund av hur besök på [!UICONTROL Adobe Analytics] och mobilappar lanseras i [!UICONTROL Adobe Mobile Services] är beräknade, kan du se olika resultat i rapporteringen. Mer information finns i [Jämför besök och startprogram för mobilappar](https://helpx.adobe.com/analytics/kb/compare-visits-and-mobile-app-launches.html).

* **Krascher**

   Utlöses när programmet inte avslutas korrekt. Den här händelsen skickas när programmet startas efter en krasch.

   >[!TIP]
   >Programmet kraschar om det inte anropas att avsluta.

* **Total sessionslängd**

   Sammanställd total sessionslängd.

## Mått {#section_1784C7E859F64CCEB95C5DD1DCF5C98D}

Här är en lista över mobila standarddimensioner:

* **Installationsdatum**

   Datum för första start efter installationen. Datumet finns i *MM/DD/ÅÅÅ* format.

* **Program-ID**

   Lagrar programnamnet och versionen i följande format: `[AppName] [BundleVersion]`. Exempel, `myapp 1.1`.

* **Startnummer**

   Antal gånger som programmet startades eller togs bort från bakgrunden.

* **Dagar sedan första användningen**

   Antal dagar sedan första körningen.

* **Dagar sedan senaste användning**

   Antal dagar sedan senaste användning.

* **Timme på dagen**

   Mäter timmen då appen startades och använder det numeriska 24-timmarsformatet. Detta mått används också för tidsdelning för att bestämma den maximala användningstiden.

* **Veckodag**

   Antal veckor som appen startades.

* **Operativsystem**

   Enhetens operativsystem.

* **Operativsystemsversion**

   Operativsystemversion.

* **Dagar sedan senaste uppgraderingen**

   Antal dagar sedan programversionsnumret ändrades.

   >[!TIP]
   >
   >Dagar sedan den senaste uppgraderingen lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

* **Startar sedan senaste uppgraderingen**

   Antal starter sedan programversionsnumret har ändrats.

   >[!TIP]
   >
   >Startar eftersom den senaste uppgraderingen inte lagras automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

* **Enhetsnamn**

   Lagrar enhetsnamnet. I iOS identifierar en kommaavgränsad tvåsiffrig sträng iOS-enheten. Det första talet representerar enhetsgenereringen och det andra numret som representerar olika medlemmar i enhetsfamiljen.

* **Transportföretagets namn**

   Lagrar namnet på mobiltjänstleverantören.

* **Upplösning**

   Bredd och höjd i pixlar.
