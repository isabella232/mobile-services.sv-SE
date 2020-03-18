---
description: I följande tabell visas de mått och mått som mobilbiblioteket kan mäta automatiskt efter att livscykeln har implementerats.
seo-description: I följande tabell visas de mått och mått som mobilbiblioteket kan mäta automatiskt efter att livscykeln har implementerats.
seo-title: Livscykelvärden
solution: Marketing Cloud,Analytics
title: Livscykelvärden
topic: Developer and implementation
uuid: b795e383-d59b-4a3c-9e14-ffe8fb58412c
translation-type: tm+mt
source-git-commit: a6608bf4d36a6fb6aca00f50cc058c09dbd931b1

---


# Livscykelstatistik {#lifecycle-metrics}

Här är mätvärden och mått som kan mätas automatiskt av mobilbiblioteket efter att livscykeln har implementerats.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya SDK:er för Adobe Experience Platform Mobile kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till [Experience Platform Launch](https://launch.adobe.com/)för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).


## Livscykelvärden och dimensioner {#section_78F036C4296F4BA3A47C2044F79C86C1}

När livscykelmätvärden har konfigurerats skickas mätvärdena i kontextdataparametrar till Analytics, parametrar till Target med varje mbox-anrop och som en signal till Audience Manager. Analytics och Target har samma format, medan Audience Manager använder olika prefix för varje mätvärde.

För Analytics hämtas och rapporteras kontextdata som skickas med varje livscykelspårningsanrop automatiskt med hjälp av de mått eller dimensioner som listas i den första kolumnen.

>[!TIP]
>
>Undantag anges i beskrivningen.

### Mått

* **Första starten**

   Utlöses vid första körningen efter installation eller ominstallation.

   * Parametern Analytics Context Data/Target: `a.InstallEvent`
   * Audience Manager-signal: `c_a_InstallEvent`

* **Uppgraderingar**

   Utlöses vid första körningen efter uppgraderingen eller när som helst när versionsnumret ändras.

   * Parametern Analytics Context Data/Target: `a.UpgradeEvent`
   * Audience Manager-signal: `c_a_UpgradeEvent`

* **Dagliga engagerade användare**

   Utlöses när programmet används en viss dag.

   * Parametern Analytics Context Data/Target: `a.DailyEngUserEvent`
   * Audience Manager-signal: `c_a_DailyEngUserEvent`

* **Engagerade användare varje månad**

   Utlöses när programmet används under en viss månad.

   * Parametern Analytics Context Data/Target: `a.MonthlyEngUserEvent`
   * Audience Manager-signal: `c_a_MonthlyEngUserEvent`

* **Startar**

   Utlöses vid varje körning, inklusive krascher och installationer. Utlöses också när programmet återupptas från bakgrunden efter att tidsgränsen för livscykelsessionen har överskridits.

   * Parametern Analytics Context Data/Target: `a.LaunchEvent`
   * Audience Manager-signal: `c_a_LaunchEvent`

* **Krascher**

   Utlöses när programmet inte är bakgrundsbelagt innan det stängs. Händelsen skickas när programmet startas igen efter kraschen.  Adobe Mobile-kraschrapporter implementerar inte en global hanterare för ej infångade undantag.

   * Parametern Analytics Context Data/Target: `a.CrashEvent`
   * Audience Manager-signal: `c_a_CrashEvent`

* **Längd på föregående session**

   Rapporterar antalet sekunder som en tidigare programsession varade baserat på hur länge programmet var öppet och i förgrunden.

   * Parametern Analytics Context Data/Target: `a.PrevSessionLength`
   * Audience Manager-signal: `c_a_PrevSessionLength`

>[!IMPORTANT]
>
> Mätvärdena för *Daglig engagerad användare* och *Månadsengagerad användare* lagras inte automatiskt i en analyssiffra. Du måste skapa en bearbetningsregel som ställer in en anpassad händelse för att hämta dessa mått.

#### Dimensioner

* **Installationsdatum**

   Datum för första start efter installation.  Datumformatet är `MM/DD/YYYY`.

   * Data/mål för analyskontext: `a.InstallDate`
   * Målgruppshantering: `c_a_InstallDate`

* **Program-ID**

   Sparar programnamnet och versionen i `[AppName] [BundleVersion]` formatet. Exempel, `myapp 1.1`.

   * Data/mål för analyskontext: `a.AppID`
   * Målgruppshantering: `c_a_AppID`

* **Startnummer**

   Antal gånger som programmet startades eller togs bort från bakgrunden.

   * Data/mål för analyskontext: `a.Launches`
   * Målgruppshantering: `c_a_Launches`

* **Dagar sedan första användningen**

   Antal dagar sedan första körningen.

   * Data/mål för analyskontext: `a.DaysSinceFirstUse`
   * Målgruppshantering: `c_a_DaysSinceFirstUse`

* **Dagar sedan senaste användning**

   Antal dagar sedan senaste användning.

   * Data/mål för analyskontext: `a.DaysSinceLastUse`
   * Målgruppshantering: `c_a_DaysSinceLastUse`

* **Timme på dagen**

   Mäter timmen då appen startades och använder det numeriska 24-timmarsformatet. Används för tidsdelning för att bestämma maximal användningstid.

   * Data/mål för analyskontext: `a.HourOfDay`
   * Målgruppshantering: `c_a_HourOfDay`

* **Veckodag**

   Antal veckor som appen startades.

   * Data/mål för analyskontext: `a.DayOfWeek`
   * Målgruppshantering: `c_a_DayOfWeek`

* **Operativsystemsversion**

   Antal dagar sedan programversionsnumret ändrades.

   * Data/mål för analyskontext: `a.OSVersion`
   * Målgruppshantering: `c_a_OSVersion|OS version`

* **Dagar sedan senaste uppgraderingen**

   Dagar sedan senaste uppgraderingen.

   * Data/mål för analyskontext: `a.DaysSinceLastUpgrade`
   * Målgruppshantering: `c_a_DaysSinceLastUpgrade`

* **Startar sedan senaste uppgraderingen**

   Antal starter sedan programversionsnumret har ändrats.

   * Data/mål för analyskontext: `a.LaunchesSinceUpgrade`
   * Målgruppshantering: `c_a_LaunchesSinceUpgrade`

* **Enhetsnamn**

   Lagrar enhetsnamnet.  Kommaavgränsad tvåsiffrig sträng som identifierar iOS-enheten. Det första talet representerar vanligtvis enhetsgenereringen och det andra numret är vanligtvis olika versioner av olika medlemmar i enhetsfamiljen. En lista med vanliga enhetsnamn finns i iOS-enhetsversioner.

   * Data/mål för analyskontext: `a.DeviceName`
   * Målgruppshantering: `c_a_DeviceName`

* **Transportföretagets namn**

   Lagrar namnet på leverantören av mobiltjänster enligt vad som angetts av enheten.

   * Data/mål för analyskontext: `a.CarrierName`
   * Målgruppshantering: `c_a_CarrierName`

* **Upplösning**

   Bredd x höjd i pixlar.

   * Data/mål för analyskontext: `a.Resolution`
   * Målgruppshantering: `c_a_Resolution`
   >[!IMPORTANT]
   >
   >De *dagar som gått sedan den senaste uppgraderingen*, *Startar sedan den senaste uppgraderingen* och dimensionerna för *transportföretagets namn* lagras inte automatiskt i en Analytics-variabel. Du måste skapa en bearbetningsregel för att kopiera värdena till en Analytics-variabel för rapportering.


## Ytterligare mobilstatistik och dimensioner {#section_0B32BBF9CA734103BEDB5E755FFE5B31}

Följande mått och mått hämtas in i mobillösningsvariabler med den listade metoden.

### Mått

* **Total åtgärdstid**

   Fylls i av trackTimedAction-metoder.

   * Parametern Analytics Context Data/Target: `a.action.time.total`
   * Audience Management-egenskap: `c_a_action_time_total`

* **Åtgärdstid i app**

   Fylls i av trackTimedAction-metoder.

   * Parametern Analytics Context Data/Target: `a.action.time.inapp`
   * Audience Management-egenskap: `c_a_action_time_inapp`

* **Livstidsvärde (händelse)**

   Fylls i av trackLifetimeValue-metoder.

   * Parametern Analytics Context Data/Target: `a.ltv.amount`
   * Audience Management-egenskap: `c_a_ltv_amount`


### Dimensioner

* **Placering (ned till 10 km)**

   Fylls i med `trackLocation` metoder.

   * Parametern Analytics Context Data/Target:

      * `a.loc.lat.a`
      * `a.loc.lon.a`
   * Audience Management-egenskap:

      * `c_a_loc_lat_a`
      * `c_a_loc_lon_a`


* **Plats (ned till 100 m)**

   Fylls i av trackLocation-metoder.

   * Parametern Analytics Context Data/Target:

      * `a.loc.lat.b`
      * `a.loc.lon.b`
   * Audience Management-egenskap:

      * `c_a_loc_lat_b`
      * `c_a_loc_lon_b`


* **Plats (ned till 1 m)**

   Fylls i med `trackLocation` metoder.

   * Parametern Analytics Context Data/Target:

      * `a.loc.lat.c`
      * `a.loc.lon.c`
   * Audience Management-egenskap:

      * `c_a_loc_lat_c`
      * `c_a_loc_lon_c`


* **Intressepunktens namn**

   Fylls i av trackLocation-metoder när enheten är i en definierad POI.

   * Parametern Analytics Context Data/Target: `a.loc.poi`
   * Audience Management-egenskap: `c_a_loc_poi`

* **Avstånd till intressecentrum**

   Fylls i av trackLocation-metoder när enheten är i en definierad POI.

   * Parametern Analytics Context Data/Target: `a.loc.dist`
   * Audience Management-egenskap: `c_a_loc_dist`

* **Livstidsvärde (konverteringsvariabel)**

   Fylls i av trackLifetimeValue-metoder.

   * Parametern Analytics Context Data/Target: `a.ltv.amount`
   * Audience Management-egenskap: `c_a_ltv_amount`

* **Spårningskod**

   Fylls i av Anskaffning av mobilapp. Genereras automatiskt av Adobes mobiltjänster.

   * Parametern Analytics Context Data/Target: `a.referrer.campaign.trackingcode`
   * Audience Management-egenskap: `c_a_referrer_campaign_trackingcode`

* **Campaign**

   Namnet på kampanjen, som också lagras i kampanjvariabeln. Fylls i av Anskaffning av mobilapp.

   * Parametern Analytics Context Data/Target: `a.referrer.campaign.name`
   * Audience Management-egenskap: `c_a_referrer_campaign_name`

* **Kampanjinnehåll**

   Namnet eller ID för innehållet som visade länken. Fylls i av Anskaffning av mobilapp.

   * Parametern Analytics Context Data/Target: `a.referrer.campaign.content`
   * Audience Management-egenskap: `c_a_referrer_campaign_content`

* **Kampanjmedium**

   Marknadsföringsmedium, som banner eller e-post. Fylls i av Anskaffning av mobilapp.

   * Parametern Analytics Context Data/Target: `a.referrer.campaign.medium`
   * Audience Management-egenskap: `c_a_referrer_campaign_medium`

* **Kampanjkälla**

   Ursprunglig hänvisare, till exempel nyhetsbrev eller sociala medier. Fylls i av Anskaffning av mobilapp.

   * Parametern Analytics Context Data/Target: `a.referrer.campaign.source`
   * Audience Management-egenskap: `c_a_referrer_campaign_source`

* **Kampanjperiod**

   Betalnyckelord eller andra termer som du vill spåra med förvärvet. Fylls i av Anskaffning av mobilapp.

   * Parametern Analytics Context Data/Target: `a.referrer.campaign.term`
   * Audience Management-egenskap: `c_a_referrer_campaign_term`
