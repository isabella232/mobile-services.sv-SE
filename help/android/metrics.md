---
description: Här är mätvärden och mått som kan mätas automatiskt av mobilbiblioteket, efter att livscykeln har implementerats, och en länk för att felsöka livscykeldata.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Livscykelstatistik
topic-fix: Developer and implementation
uuid: a8f3ebac-be3b-4948-82bb-105d46cfff6d
exl-id: 1e50318d-894c-4039-ba45-71cb9edbc5b5
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 2%

---

# Livscykelstatistik{#lifecycle-metrics}

I det här avsnittet finns information om mått och mått som kan mätas automatiskt av mobilbiblioteket, efter att livscykeln har implementerats, och en länk för att felsöka livscykeldata. Mer information om felsökning finns på [Felsöka livscykeldata](https://helpx.adobe.com/analytics/kb/troubleshoot-lifecycle-data.html).

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Livscykelvärden och dimensioner {#section_78F036C4296F4BA3A47C2044F79C86C1}

När livscykelmätvärden är konfigurerade skickas de i kontextdataparametrar till Analytics, i parametrar till Target för varje mbox-anrop och som en signal till målgruppshanteringen. Analyserna och Target har samma format, medan målgruppshanteringen använder olika prefix för varje mätvärde.

För Analytics hämtas och rapporteras kontextdata som skickas med varje livscykelspårningsanrop automatiskt med hjälp av mätvärden eller dimensioner, och undantagen noteras.

### Mätvärden

* **Första starten**

   Utlöses vid första körningen efter installation eller ominstallation.

   * Kontextdata/målparameter för analyser: `a.InstallEvent`
   * Audience Manager Signal: `c_a_InstallEvent`

* **Uppgraderingar**

   Utlöses vid första körningen efter en uppgradering eller när versionsnumret ändras.

   * Kontextdata/målparameter för analyser: `a.UpgradeEvent`
   * Audience Manager Signal: `c_a_UpgradeEvent`

* **Dagliga engagerade användare**

   Utlöses när programmet används en viss dag.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Kontextdata/målparameter för analyser: `a.DailyEngUserEvent`
   * Audience Manager Signal: `c_a_DailyEngUserEvent`

* **Engagerade användare varje månad**

   Utlöses när programmet används under en viss månad.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Kontextdata/målparameter för analyser: `a.MonthlyEngUserEvent`
   * Audience Manager Signal: `c_a_MonthlyEngUserEvent`

* **Launches**

   Utlöses vid varje körning, inklusive krascher och installationer. Utlöses också vid ett återköp från bakgrunden när tidsgränsen för livscykelsessionen har överskridits.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Kontextdata/målparameter för analyser: `a.LaunchEvent`
   * Audience Manager Signal: `c_a_LaunchEvent`

* **Krascher**

   Utlöses när programmet inte är bakgrundsbelagt innan det stängs. Händelsen skickas när programmet startas efter kraschen.  Kraschrapportering för Adobe Mobile implementerar inte en global hanterare för ej infångade undantag.

   * Kontextdata/målparameter för analyser: `a.CrashEvent`
   * Audience Manager Signal: `c_a_CrashEvent`

* **Längd på föregående session**

   Rapporterar antalet sekunder som en tidigare programsession varade, baserat på hur länge programmet var öppet och i förgrunden.

   * Kontextdata/målparameter för analyser: `a.PrevSessionLength`
   * Audience Manager Signal: `c_a_PrevSessionLength`


### Mått

* **Installationsdatum**

   Datum för första start efter installation. Datumformatet är MM/DD/ÅÅÅÅ.

   * Kontextdata/målparameter för analyser: `a.InstallDate`
   * Audience Manager: `c_a_InstallDate`

* **Program-ID**

   Lagrar programnamnet och versionen i `[AppName] [BundleVersion]` format. Ett exempel på det här formatet är `myapp 1.1`.

   * Kontextdata/målparameter för analyser: `a.AppID`
   * Audience Manager: `c_a_AppID`

* **Startnummer**

   Antal gånger som programmet startades eller togs bort från bakgrunden.

   * Kontextdata/målparameter för analyser: `a.Launches`
   * Audience Manager: `c_a_Launches`

* **Dagar sedan första användningen**

   Antal dagar sedan första körningen.

   * Kontextdata/målparameter för analyser: `a.DaysSinceFirstUse`
   * Audience Manager: `c_a_DaysSinceFirstUse`

* **Dagar sedan senaste användning**

   Antal dagar sedan senaste användning.

   * Kontextdata/målparameter för analyser: `a.DaysSinceLastUse`
   * Audience Manager: `c_a_DaysSinceLastUse`

* **Timme på dagen**

   Mäter timmen då appen startades.  Det här måttet använder det numeriska 24-timmarsformatet och används för tidsdelning för att bestämma den maximala användningstiden.

   * Kontextdata/målparameter för analyser: `a.HourOfDay`
   * Audience Manager: `c_a_HourOfDay`

* **Veckodag**

   Antal dagar i veckan då appen startades.

   * Kontextdata/målparameter för analyser: `a.DayOfWeek`
   * Audience Manager: `c_a_DayOfWeek`

* **Operativsystemsversion**

   OS-versionen.

   * Kontextdata/målparameter för analyser: `a.OSVersion`
   * Audience Manager: `c_a_OSVersion`

* **Dagar sedan senaste uppgraderingen**

   Antal dagar sedan programversionsnumret ändrades.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata/målparameter för analyser: `a.DaysSinceLastUpgrade`
   * Audience Manager: `c_a_DaysSinceLastUpgrade`

* **Startar sedan senaste uppgraderingen**

   Antal starter sedan programversionsnumret har ändrats.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata/målparameter för analyser: `a.LaunchesSinceUpgrade`
   * Audience Manager: `c_a_LaunchesSinceUpgrade`

* **Enhetsnamn**

   Lagrar enhetsnamnet.

   * Kontextdata/målparameter för analyser: `a.DeviceName`
   * Audience Manager: `c_a_DeviceName`

* **Transportföretagets namn**

   Lagrar namnet på leverantören av mobiltjänster enligt vad som angetts av enheten.  Viktigt: Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata/målparameter för analyser: `a.CarrierName`
   * Audience Manager: `c_a_CarrierName`

* **Upplösning**

   Bredd x höjd i pixlar.

   * Kontextdata/målparameter för analyser: `a.Resolution`
   * Audience Manager: `c_a_Resolution`

## Ytterligare mobilstatistik och dimensioner {#section_0B32BBF9CA734103BEDB5E755FFE5B31}

Följande mått och mått hämtas in i mobillösningens variabler med den metod som listas i **Beskrivning** kolumn.

### Mätvärden

* **Total åtgärdstid**

   Fylls i av `trackTimedAction` metoder.

   * Kontextdata/målparameter för analyser: `a.action.time.total`
   * Audience Manager: `c_a_action_time_total`

* **Åtgärdstid i app**

   Fylls i av `trackTimedAction` metoder.

   * Kontextdata/målparameter för analyser: `a.action.time.inapp`
   * Audience Manager: `c_a_action_time_inapp`

* **Livstidsvärde (händelse)**

   Fylls i av `trackLifetimeValue` metoder.

   * Kontextdata/målparameter för analyser: `a.ltv.amount`
   * Audience Manager: `c_a_ltv_amount`

### Mått

* **Placering (ned till 10 km)**

   Fylls i av `trackLocation` metoder.

   * Kontextdata/målparametrar för analyser:

      * `a.loc.lat.a`
      * `a.loc.lon.a`
   * Audience Manager traits:

      * `c_a_loc_lat_a`
      * `c_a_loc_lon_a`


* **Plats (ned till 100 m)**

   Fylls i av trackLocation-metoder.

   * Kontextdata/målparametrar för analyser:

      * `a.loc.lat.b`
      * `a.loc.lon.b`
   * Audience Manager traits:

      * `c_a_loc_lat_b`
      * `c_a_loc_lon_b`


* **Plats (ned till 1 m)**

   Fylls i av trackLocation-metoder.

   * Kontextdata/målparametrar för analyser:

      * `a.loc.lat.c`
      * `a.loc.lon.c`
   * Audience Manager traits:

      * `c_a_loc_lat_c`
      * `c_a_loc_lon_c`


* **Intressepunktens namn**

   Fylls i av trackLocation-metoder när enheten finns inom en definierad POI.

   * Kontextdata/målparametrar för analyser: `a.loc.poi`
   * Audience Manager: `c_a_loc_poi`

* **Avstånd till intressecentrum**

   Fylls i av trackLocation-metoder när enheten finns inom en definierad POI.

   * Kontextdata/målparametrar för analyser: `a.loc.dist`
   * Audience Manager: `c_a_loc_dist`

* **Livstidsvärde (konverteringsvariabel)**

   Fylls i av trackLifetimeValue-metoder.

   * Kontextdata/målparametrar för analyser: `a.ltv.amount`
   * Audience Manager: `c_a_ltv_amount`

* **Spårningskod**

   Fylls i av Mobile App Acquisition och genereras automatiskt av Adobe mobiltjänster.

   * Kontextdata/målparametrar för analyser: `a.referrer.campaign.trackingcode`
   * Audience Manager: `c_a_referrer_campaign_trackingcode`

* **Campaign**

   Namnet på kampanjen, som också lagras i kampanjvariabeln. Fylls i av Anskaffning av mobilapp.

   * Kontextdata/målparametrar för analyser: `a.referrer.campaign.name`
   * Audience Manager: `c_a_referrer_campaign_name`

* **Kampanjinnehåll**

   Namnet eller ID för innehållet som visade länken. Fylls i av Anskaffning av mobilapp.

   * Kontextdata/målparametrar för analyser: `a.referrer.campaign.content`
   * Audience Manager: `c_a_referrer_campaign_content`

* **Kampanj mellan**

   Marknadsföringsmedium, t.ex. en banderoll eller ett e-postmeddelande. Fylls i av Anskaffning av mobilapp.

   * Kontextdata/målparametrar för analyser: `a.referrer.campaign.medium`
   * Audience Manager: `c_a_referrer_campaign_medium`

* **Kampanjkälla**

   Ursprunglig hänvisare, till exempel ett nyhetsbrev eller ett nätverk för sociala medier. Fylls i av Anskaffning av mobilapp.

   * Kontextdata/målparametrar för analyser: `a.referrer.campaign.source`
   * Audience Manager: `c_a_referrer_campaign_source`

* **Kampanjperiod**

   Betalnyckelord eller andra termer som du vill spåra med förvärvet. Fylls i av Anskaffning av mobilapp.

   * Kontextdata/målparametrar för analyser: `a.referrer.campaign.term`
   * Audience Manager: `c_a_referrer_campaign_term`
