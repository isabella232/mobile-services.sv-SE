---
description: Här är mätvärden och mått som kan mätas automatiskt av mobilbiblioteket, efter att livscykeln har implementerats, och en länk för att felsöka livscykeldata.
keywords: android;bibliotek;mobil;sdk
seo-description: Här är mätvärden och mått som kan mätas automatiskt av mobilbiblioteket, efter att livscykeln har implementerats, och en länk för att felsöka livscykeldata.
seo-title: Livscykelstatistik
solution: Experience Cloud,Analytics
title: Livscykelstatistik
topic-fix: Developer and implementation
uuid: 5a371f11-6521-410f-a01f-fc3b285b050f
exl-id: d7436411-65bd-4cf7-ae3e-cec829a7690a
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---

# Livscykelstatistik {#lifecycle-metrics}

Här är mätvärden och mått som kan mätas automatiskt av mobilbiblioteket, efter att livscykeln har implementerats, och en länk för att felsöka livscykeldata.

Mer information finns i kunskapsbasen på [Troubleshoot Lifecycle data](https://helpx.adobe.com/analytics/kb/troubleshoot-lifecycle-data.html).

## Livscykelvärden och dimensioner {#section_78F036C4296F4BA3A47C2044F79C86C1}

När livscykelmätvärden är konfigurerade skickas de i kontextdataparametrar till Analytics, i parametrar till Target för varje mbox-anrop och som en signal till målgruppshanteringen. Analyserna och Target har samma format, medan målgruppshanteringen använder olika prefix för varje mätvärde.

För Analytics hämtas och rapporteras kontextdata som skickas med varje livscykelspårningsanrop automatiskt med hjälp av mätvärden eller dimensioner.

### Mätvärden

* **a.media.name**

   Utlöses vid första körningen efter installation eller ominstallation.

   * Kontextdata för analys/Target-parameter: `a.InstallEvent`
   * Audience Manager signal: `c_a_InstallEvent`

* **Uppgraderingar**

   Utlöses vid första körningen efter en uppgradering eller när versionsnumret ändras.

   * Kontextdata för analys/Target-parameter: `a.UpgradeEvent`
   * Audience Manager signal: `c_a_UpgradeEvent`

* **Dagliga engagerade användare**

   Utlöses när programmet används en viss dag.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Kontextdata för analys/Target-parameter: `a.DailyEngUserEvent`
   * Audience Manager signal: `c_a_DailyEngUserEvent`

* **Engagerade användare varje månad**

   Utlöses när programmet används under en viss månad.  >>>

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Kontextdata för analys/Target-parameter: `a.MonthlyEngUserEvent`
   * Audience Manager signal: `c_a_MonthlyEngUserEvent`

* **Launches**

   Utlöses vid varje körning, inklusive krascher och installationer. Utlöses också vid ett återköp från bakgrunden när tidsgränsen för livscykelsessionen har överskridits.

   * Kontextdata för analys/Target-parameter: `a.LaunchEvent`
   * Audience Manager signal: `c_a_LaunchEvent`

* **Krascher**

   Utlöses när programmet inte är bakgrundsbelagt innan det stängs. Händelsen skickas när programmet startas efter kraschen. Kraschrapportering för Adobe Mobile implementerar inte en global hanterare för ej infångade undantag.

   * Kontextdata för analys/Target-parameter: `a.CrashEvent`
   * Audience Manager signal: `c_a_CrashEvent`

* **Längd på föregående session**

   Rapporterar antalet sekunder som en tidigare programsession varade, baserat på hur länge programmet var öppet och i förgrunden.

   * Kontextdata för analys/Target-parameter: `a.PrevSessionLength`
   * Audience Manager signal: `c_a_PrevSessionLength`

### Mått

* **Installationsdatum**

   Datum för första start efter installation. Datumformatet är `MM/DD/YYYY`.

   * Kontextdata för analys/Target-parameter: `a.InstallDate`
   * Audience Manager signal: `c_a_InstallDate`

* **Program-ID**

   Lagrar programnamnet och versionen i följande format:
   `[AppName] [BundleVersion]`.

   Ett exempel på det här formatet är `myapp 1.1`.

   * Kontextdata för analys/Target-parameter: `a.AppID`
   * Audience Manager signal: `c_a_AppID`

* **Startnummer**

   Antal gånger som programmet startades eller togs bort från bakgrunden.

   * Kontextdata för analys/Target-parameter: `a.Launches`
   * Audience Manager signal: `c_a_Launches`

* **Dagar sedan första användningen**

   Antal dagar sedan första körningen.

   * Kontextdata för analys/Target-parameter: `a.DaysSinceFirstUse`
   * Audience Manager signal: `c_a_DaysSinceFirstUse`

* **Dagar sedan senaste användning**

   Antal dagar sedan senaste användning.

   * Kontextdata för analys/Target-parameter: `a.DaysSinceLastUse`
   * Audience Manager signal: `c_a_DaysSinceLastUse`

* **Timme på dagen**

   Mäter timmen då appen startades. Det här måttet använder det numeriska 24-timmarsformatet och används för tidsdelning för att bestämma den maximala användningstiden.

   * Kontextdata för analys/Target-parameter: `a.HourOfDay`
   * Audience Manager signal: `c_a_HourOfDay`

* **Veckodag**

   Antal dagar i veckan då appen startades.

   * Kontextdata för analys/Target-parameter: `a.DayOfWeek`
   * Audience Manager signal: `c_a_DayOfWeek`

* **Operativsystemsversion**

   Operativsystemets version.

   * Kontextdata för analys/Target-parameter: `a.OSVersion`
   * Audience Manager signal: `c_a_OSVersion`

* **Dagar sedan senaste uppgraderingen**

   Antal dagar sedan programversionsnumret ändrades.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata för analys/Target-parameter: `a.DaysSinceLastUpgrade`
   * Audience Manager signal: `c_a_DaysSinceLastUpgrade`

* **Startar sedan senaste uppgraderingen**

   Antal starter sedan programversionsnumret har ändrats.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata för analys/Target-parameter: `a.LaunchesSinceUpgrade`
   * Audience Manager signal: `c_a_LaunchesSinceUpgrade`

* **Enhetsnamn**

   Lagrar enhetsnamnet.

   * Kontextdata för analys/Target-parameter: `a.DeviceName`
   * Audience Manager signal: `c_a_DeviceName`

* **Transportföretagets namn**

   Lagrar namnet på leverantören av mobiltjänster enligt vad som angetts av enheten.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata för analys/Target-parameter: `a.CarrierName`
   * Audience Manager signal: `c_a_CarrierName`

* **Upplösning**

   Bredd x höjd i pixlar.

   * Kontextdata för analys/Target-parameter: `a.Resolution`
   * Audience Manager signal: `c_a_Resolution`

## Ytterligare mobilstatistik och dimensioner {#section_0B32BBF9CA734103BEDB5E755FFE5B31}

Följande mått och mått hämtas in i mobillösningsvariabler med den listade metoden.

* **Placering (ned till 10 km)**

   Fylls i av `trackLocation`-metoder.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.lat.a`
      * `a.loc.lon.a`
   * Audience Management-egenskap:

      * `c_a_loc_lat_a`
      * `c_a_loc_lon_a`


* **Plats (ned till 100 m)**

   Fylls i av `trackLocation`-metoder.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.lat.b`
      * `a.loc.lon.b`
   * Audience Management-egenskap:

      * `c_a_loc_lat_b`
      * `c_a_loc_lon_b`


* **Plats (ned till 1 m)**

   Fylls i av `trackLocation`-metoder.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.lat.c`
      * `a.loc.lon.c`
   * Audience Management-egenskap:

      * `c_a_loc_lat_c`
      * `c_a_loc_lon_c`


* **Intressepunktens namn**

   Fylls i av `trackLocation`-metoder när enheten finns inom en definierad POI.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.poi`
   * Audience Management-egenskap:

      * `c_a_loc_poi`


* **Avstånd till intressecentrum**

   Fylls i av `trackLocation`-metoder när enheten finns inom en definierad POI.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.dist`
   * Audience Management-egenskap:

      * `c_a_loc_dist`
