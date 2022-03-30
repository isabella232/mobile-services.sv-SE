---
description: Visar mått och mått som kan mätas automatiskt av mobilbiblioteket.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Livscykelstatistik
topic-fix: Developer and implementation
uuid: f958c3ef-1d79-4b30-8966-ef74bd48a5d6
exl-id: 19572f15-c5df-40fe-9979-3a5bdd581f2b
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# Livscykelstatistik {#lifecycle-metrics}

Visar mått och mått som kan mätas automatiskt av mobilbiblioteket.

Mer information finns i [Felsöka livscykeldata](https://helpx.adobe.com/analytics/kb/troubleshoot-lifecycle-data.html).


## Livscykelvärden och dimensioner {#section_78F036C4296F4BA3A47C2044F79C86C1}

När livscykelmätvärden är konfigurerade skickas de i kontextdataparametrar till Analytics, i parametrar till Target för varje mbox-anrop och som en signal till målgruppshanteringen. Analyserna och Target har samma format, medan målgruppshanteringen använder olika prefix för varje mätvärde.

För Analytics hämtas och rapporteras kontextdata som skickas med varje livscykelspårningsanrop automatiskt med hjälp av mätvärden eller dimensioner. Undantag noteras i innehållet.

## Mätvärden

* **Första starten**

   Utlöses vid första körningen efter installation eller ominstallation.

   * Parametern Analytics Context Data/Target: `a.InstallEvent`
   * Audience Manager signal: `c_a_InstallEvent`

* **Uppgraderingar**

   Utlöses vid första körningen efter en uppgradering eller när versionsnumret ändras.

   * Parametern Analytics Context Data/Target: `a.UpgradeEvent`
   * Audience Manager signal: `c_a_UpgradeEvent`

* **Dagliga engagerade användare**

   Utlöses när programmet används en viss dag.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Parametern Analytics Context Data/Target: `a.DailyEngUserEvent`
   * Audience Manager signal: `c_a_DailyEngUserEvent`

* **Engagerade användare varje månad**

   Utlöses när programmet används under en viss månad.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Parametern Analytics Context Data/Target: `a.MonthlyEngUserEvent`
   * Audience Manager signal: `c_a_MonthlyEngUserEvent`

* **Launches**

   Utlöses vid varje körning, inklusive krascher och installationer. Utlöses också vid ett återköp från bakgrunden när tidsgränsen för livscykelsessionen har överskridits.

   * Parametern Analytics Context Data/Target: `a.LaunchEvent`
   * Audience Manager signal: `c_a_LaunchEvent`

* **Krascher**

   Utlöses när programmet inte är bakgrundsbelagt innan det stängs. Händelsen skickas när programmet startas efter kraschen. Kraschrapportering för Adobe Mobile implementerar inte en global hanterare för ej infångade undantag.

   * Parametern Analytics Context Data/Target: `a.CrashEvent`
   * Audience Manager signal: `c_a_CrashEvent`

* **Längd på föregående session**

   Rapporterar antalet sekunder som en tidigare programsession varade, baserat på hur länge programmet var öppet och i förgrunden.

   * Parametern Analytics Context Data/Target: `a.PrevSessionLength`
   * Audience Manager signal: `c_a_PrevSessionLength`


## Mått

* **Installationsdatum**

   Datum för första start efter installation. Datumformatet är `MM/DD/YYYY`.

   * Parametern Analytics Context Data/Target: `a.InstallDate`
   * Audience Manager signal: `c_a_InstallDate`

* **Program-ID**

   Lagrar programnamnet och versionen i `[AppName] [BundleVersion]` format. Ett exempel på det här formatet är `myapp 1.1`.

   * Parametern Analytics Context Data/Target: `a.AppID`
   * Audience Manager signal: `c_a_AppID`

* **Startnummer**

   Antal gånger som programmet startades eller togs bort från bakgrunden.

   * Parametern Analytics Context Data/Target: `a.Launches`
   * Audience Manager signal: `c_a_Launches`

* **Dagar sedan första användningen**

   Antal dagar sedan första körningen.

   * Parametern Analytics Context Data/Target: `a.DaysSinceFirstUse`
   * Audience Manager signal: `c_a_DaysSinceFirstUse`

* **Dagar sedan senaste användning**

   Antal dagar sedan senaste användning.

   * Parametern Analytics Context Data/Target: `a.DaysSinceLastUse`
   * Audience Manager signal: `c_a_DaysSinceLastUse`

* **Timme på dagen**

   Mäter timmen då appen startades. Det här måttet använder det numeriska 24-timmarsformatet och används för tidsdelning för att bestämma den maximala användningstiden.

   * Parametern Analytics Context Data/Target: `a.HourOfDay`
   * Audience Manager signal: `c_a_HourOfDay`

* **Veckodag**

   Antal dagar i veckan då appen startades.

   * Parametern Analytics Context Data/Target: `a.DayOfWeek`
   * Audience Manager signal: `c_a_DayOfWeek`

* **Operativsystemsversion**

   OS-versionen.

   * Parametern Analytics Context Data/Target: `a.OSVersion`
   * Audience Manager signal: `c_a_OSVersion`

* **Dagar sedan senaste uppgraderingen**

   Antal dagar sedan programversionsnumret ändrades.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Parametern Analytics Context Data/Target: `a.DaysSinceLastUpgrade`
   * Audience Manager signal: `c_a_DaysSinceLastUpgrade`

* **Startar sedan senaste uppgraderingen**

   Antal starter sedan programversionsnumret har ändrats.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Parametern Analytics Context Data/Target: `a.LaunchesSinceUpgrade`
   * Audience Manager signal: `c_a_LaunchesSinceUpgrade`

* **Enhetsnamn**

   Lagrar enhetsnamnet.

   * Parametern Analytics Context Data/Target: `a.DeviceName`
   * Audience Manager signal: `c_a_DeviceName`

* **Transportföretagets namn**

   Lagrar namnet på leverantören av mobiltjänster enligt vad som angetts av enheten.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Parametern Analytics Context Data/Target: `a.CarrierName`
   * Audience Manager signal: `c_a_CarrierName`

* **Upplösning**

   Bredd x höjd i pixlar.

   * Parametern Analytics Context Data/Target: `a.Resolution`
   * Audience Manager signal: `c_a_Resolution`


## Ytterligare mobilstatistik och dimensioner {#section_0B32BBF9CA734103BEDB5E755FFE5B31}

Följande mått och mått hämtas in i mobillösningens variabler med följande metod:

### Mätvärden

* **Total åtgärdstid**

   Fylls i av `trackTimedAction` metoder.

   * Parametern Analytics Context Data/Target: `a.action.time.total`
   * Audience Manager signal: `c_a_action_time_total`

* **Åtgärdstid i app**

   Fylls i av `trackTimedAction` metoder.
   * Parametern Analytics Context Data/Target: `a.action.time.inapp`
   * Audience Manager signal: `c_a_action_time_inapp`

* **Livstidsvärde (händelse)**

   Fylls i av `trackLifetimeValue` metoder.

   * Parametern Analytics Context Data/Target: `a.ltv.amount`
   * Audience Manager signal: `c_a_ltv_amount`

### Mått

* **Placering (ned till 10 km)**

   Fylls i av `trackLocation` metoder.

   * Analyskontextdata/målparametrar:

      * `a.loc.lat.a`
      * `a.loc.lon.a`
   * Audience Manager:

      * `c_a_loc_lat_a`
      * `c_a_loc_lon_a`


* **Plats (ned till 100 m)**

   Fylls i av `trackLocation` metoder.

   * Analyskontextdata/målparametrar:

      * `a.loc.lat.b`
      * `a.loc.lon.b`
   * Audience Manager:

      * `c_a_loc_lat_b`
      * `c_a_loc_lon_b`


* **Plats (ned till 1 m)**

   Fylls i av `trackLocation` metoder.

   * Analyskontextdata/målparametrar:

      * `a.loc.lat.c`
      * `a.loc.lon.c`
   * Audience Manager:

      * `c_a_loc_lat_c`
      * `c_a_loc_lon_c`


* **Intressepunktens namn**

   Fylls i av `trackLocation` metoder när enheten är i en definierad POI.

   * Parametern Analytics Context Data/Target: `a.loc.poi`
   * Audience Manager: `c_a_loc_poi`

* **Avstånd till intressecentrum**

   Fylls i av `trackLocation` metoder när enheten finns inom en definierad POI.

   * Parametern Analytics Context Data/Target: `a.loc.dist`
   * Audience Manager: `c_a_loc_dist`

* **Livstidsvärde (konverteringsvariabel)**

   Fylls i av `trackLifetimeValue` metoder.

   * Parametern Analytics Context Data/Target: `a.ltv.amount`
   * Audience Manager: `c_a_ltv_amount`
