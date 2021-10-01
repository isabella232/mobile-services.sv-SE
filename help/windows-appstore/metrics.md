---
description: Visar mått och mått som kan mätas automatiskt av mobilbiblioteket.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Livscykelstatistik
topic-fix: Developer and implementation
uuid: c483271f-f620-46f4-aad8-d5f02d763f7d
exl-id: a1e4eeca-8b8f-47ca-a489-acc338238c42
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Livscykelstatistik{#lifecycle-metrics}

Visar mått och mått som kan mätas automatiskt av mobilbiblioteket.

Mer information finns i [Felsöka livscykeldata](https://helpx.adobe.com/analytics/kb/troubleshoot-lifecycle-data.html).

## Livscykelvärden och dimensioner {#section_78F036C4296F4BA3A47C2044F79C86C1}

När livscykelmätvärden är konfigurerade skickas de i kontextdataparametrar till Analytics, i parametrar till Target för varje mbox-anrop och som en signal till Audience Manager. Analytics och Target har samma format, och Audience Manager använder olika prefix för varje mätresultat.

För Analytics hämtas och rapporteras kontextdata som skickas med varje livscykelspårningsanrop automatiskt med hjälp av de mått eller dimensioner som listas nedan, och undantag noteras.

### Mätvärden

* **Första starten**

   Utlöses vid första körningen efter installation eller ominstallation.

   * Kontextdata för analys/Target-parameter: `a.InstallEvent`
   * Audience Manager signal: `c_a_InstallEvent`

* **Uppgraderingar**

   Utlöses vid första körningen efter en uppgradering eller när versionsnumret ändras.

   * Kontextdata för analys/Target-parameter: `a.UpgradeEvent`
   * Audience Manager signal: `c_a_UpgradeEvent`

* **Dagliga engagerade användare**

   Utlöses när programmet används en viss dag.

   >[!TIP]
   >
   >Det här måttet lagras inte automatiskt i ett Analytics-mått. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta det här måttet.

   * Kontextdata för analys/Target-parameter: `a.DailyEngUserEvent`
   * Audience Manager signal: `c_a_DailyEngUserEvent`

* **Engagerade användare varje månad**

   Utlöses när programmet används under en viss månad.

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

   * Kontextdata för analyser/Mål: `a.InstallDate`
   * Audience Manager: `c_a_InstallDate`

* **Program-ID**

   Sparar programnamnet och versionen i formatet `[AppName] [BundleVersion]`. Ett exempel på det här formatet är `myapp 1.1`.

   * Kontextdata för analyser/Mål: `a.AppID`
   * Audience Manager: `c_a_AppID`

* **Startnummer**

   Antal gånger som programmet startades eller togs bort från bakgrunden.

   * Kontextdata för analyser/Mål: `a.Launches`
   * Audience Manager: `c_a_Launches`

* **Dagar sedan första användningen**

   Antal dagar sedan första körningen.

   * Kontextdata för analyser/Mål: `a.DaysSinceFirstUse`
   * Audience Manager: `c_a_DaysSinceFirstUse`

* **Dagar sedan senaste användning**

   Antal dagar sedan senaste användning.

   * Kontextdata för analyser/Mål: `a.DaysSinceLastUse`
   * Audience Manager: `c_a_DaysSinceLastUse`

* **Timme på dagen**

   Mäter timmen då appen startades. Det här måttet använder det numeriska 24-timmarsformatet och används för tidsdelning för att bestämma den maximala användningstiden.

   * Kontextdata för analyser/Mål: `a.HourOfDay`
   * Audience Manager: `c_a_HourOfDay`

* **Veckodag**

   Antal dagar i veckan då appen startades.

   * Kontextdata för analyser/Mål: `a.DayOfWeek`
   * Audience Manager: `c_a_DayOfWeek`

* **Operativsystemsversion**

   OS-versionen.

   * Kontextdata för analyser/Mål: `a.OSVersion`
   * Audience Manager: `c_a_OSVersion`

* **Dagar sedan senaste uppgraderingen**

   Antal dagar sedan programversionsnumret ändrades.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata för analyser/Mål: `a.DaysSinceLastUpgrade`
   * Audience Manager: `c_a_DaysSinceLastUpgrade`

* **Startar sedan senaste uppgraderingen**

   Antal starter sedan programversionsnumret har ändrats.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata för analyser/Mål: `a.LaunchesSinceUpgrade`
   * Audience Manager: `c_a_LaunchesSinceUpgrade`

* **Enhetsnamn**

   Lagrar enhetsnamnet.

   * Kontextdata för analyser/Mål: `a.DeviceName`
   * Audience Manager: `c_a_DeviceName`

* **Transportföretagets namn**

   Lagrar namnet på leverantören av mobiltjänster enligt vad som angetts av enheten.

   >[!IMPORTANT]
   >
   >Det här måttet lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel om du vill kopiera det här värdet till en Analytics-variabel för rapportering.

   * Kontextdata för analyser/Mål: `a.CarrierName`
   * Audience Manager: `c_a_CarrierName`

* **Upplösning**

   Bredd x höjd i pixlar.

   * Kontextdata för analyser/Mål: `a.Resolution`
   * Audience Manager: `c_a_Resolution`


## Ytterligare mobilstatistik och dimensioner {#section_0B32BBF9CA734103BEDB5E755FFE5B31}

Följande mått och mått hämtas in i mobillösningens variabler med de metoder som listas i beskrivningen.

### Mätvärden

* **Total åtgärdstid**

   Fylls i av `trackTimedAction`-metoder.

   * Kontextdata för analys/Target-parameter: `a.action.time.total`
   * Audience Manager: `c_a_action_time_total`

* **Åtgärdstid i app**

   Fylls i av `trackTimedAction`-metoder.

   * Kontextdata för analys/Target-parameter: `a.action.time.inapp`
   * Audience Manager: `c_a_action_time_inapp`

* **Livstidsvärde (händelse)**

   Fylls i av `trackLifetimeValue`-metoder.

   * Kontextdata för analys/Target-parameter: `a.ltv.amount`
   * Audience Manager: `c_a_ltv_amount`

## Mått

* **Placering (ned till 10 km)**

   Fylls i av `trackLocation`-metoder.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.lat.a`
      * `a.loc.lon.a`
   * Audience Manager:

      * `c_a_loc_lat_a`
      * `c_a_loc_lon_a`


* **Plats (ned till 100 m)**

   Fylls i av `trackLocation`-metoder.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.lat.b`
      * `a.loc.lon.b`
   * Audience Manager:

      * `c_a_loc_lat_b`
      * `c_a_loc_lon_b`


* **Plats (ned till 1 m)**

   Fylls i av `trackLocation`-metoder.

   * Kontextdata för analys/Target-parameter:

      * `a.loc.lat.c`
      * `a.loc.lon.c`
   * Audience Manager:

      * `c_a_loc_lat_c`
      * `c_a_loc_lon_c`


* **Intressepunktens namn**

   Fylls i av `trackLocation`-metoder när enheten finns inom en definierad POI.

   * Kontextdata för analys/Target-parameter: `a.loc.poi`
   * Audience Manager: `c_a_loc_poi`

* **Avstånd till intressecentrum**

   Fylls i av `trackLocation`-metoder när enheten finns inom en definierad POI.

   * Kontextdata för analys/Target-parameter: `a.loc.dist`
   * Audience Manager: `c_a_loc_dist`

* **Livstidsvärde (konverteringsvariabel)**

   Fylls i av `trackLifetimeValue`-metoder.

   * Kontextdata för analys/Target-parameter: `a.ltv.amount`
   * Audience Manager: `c_a_ltv_amount`
