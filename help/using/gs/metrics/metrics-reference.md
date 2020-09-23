---
description: Här är referensinformationen för standardvärden och -dimensioner för mobila enheter.
keywords: mobile
seo-description: Här är referensinformationen för standardvärden och -dimensioner för mobila enheter.
seo-title: Mobile Metrics and Dimensions Reference
solution: Experience Cloud,Analytics
title: Mobile Metrics and Dimensions Reference
topic: Metrics
uuid: 96170ae7-8553-4f3e-ae01-65e5b664adf4
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '629'
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

   Utlöses på en körning som inte är en installation eller uppgradering. Detta utlöses också när programmet tas bort från bakgrunden. Som standard utlöses en ny start när programmet är i bakgrunden i fem eller fler minuter. Hur lång bakgrundstid det tar innan en ny start aktiveras kan konfigureras på sidan Hantera programinställningar **[!UICONTROL SDK Analytics Options]** . Mer information finns i *sessionstimeout (sekunder)* -raden i [Konfigurera SDK-analysalternativ](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-analytics/t-config-analytics.md).

   >[!IMPORTANT]
   >Eftersom besöken i [!UICONTROL Adobe Analytics] och mobilappstarter [!UICONTROL Adobe Mobile Services] beräknas kan du se olika resultat i rapporteringen. Mer information finns i [Jämför besök och starta](https://helpx.adobe.com/analytics/kb/compare-visits-and-mobile-app-launches.html)mobilappar.

* **Krascher**

   Utlöses när programmet inte avslutas korrekt. Den här händelsen skickas när programmet startas efter en krasch.

   >[!TIP]
   >Programmet kraschar om det inte anropas att avsluta.

* **Total sessionslängd**

   Sammanställd total sessionslängd.

## Dimensioner {#section_1784C7E859F64CCEB95C5DD1DCF5C98D}

Här är en lista över mobila standarddimensioner:

* **Installationsdatum**

   Datum för första start efter installationen. Datumet är i formatet *MM/DD/ÅÅÅÅ* .

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

   Lagrar enhetsnamnet. I iOS identifierar en kommaavgränsad tvåsiffrig sträng i iOS-enheten. Det första talet representerar enhetsgenereringen och det andra numret som representerar olika medlemmar i enhetsfamiljen. En fullständig lista över vanliga enhetsnamn finns i [iOS-enhetsversioner](/help/ios/reference/device-versions.md).

* **Transportföretagets namn**

   Lagrar namnet på mobiltjänstleverantören.

* **Upplösning**

   Bredd och höjd i pixlar.
