---
description: Med geopositionering kan ni mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i era iOS-appar.
solution: Experience Cloud Services,Analytics
title: Geografisk placering och intressepunkter
topic-fix: Developer and implementation
uuid: c800ec85-a33f-425d-b28f-bfe8bf229ae8
exl-id: 732c3863-2010-4d04-a17b-a656e857f567
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 1%

---

# Geografisk placering och intressepunkter {#geo-location-and-points-of-interest}

Med geopositionering kan ni mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i era iOS-appar.

Varje `trackLocation` ring skickar följande:

* Latitud, longitud och plats i en intressepunkt (POI) som definieras i Adobe Mobile-tjänster.

   Den här informationen skickas till mobillösningsvariabler för automatisk rapportering.

* Avstånd från centrum och precision skickas som kontextdata.

   Dessa variabler hämtas inte automatiskt. Du måste mappa dessa kontextdatavariabler med hjälp av instruktionerna i *Skicka ytterligare data* nedan.

## Dynamiska POI-uppdateringar {#section_3747B310DD5147E2AAE915E762997712}

Från och med version 4.2 definieras POI i Adobe Mobile-gränssnittet och synkroniseras dynamiskt till programkonfigurationsfilen. Synkroniseringen kräver en `analytics.poi` i `ADBMobile.json` fil:

```js
"analytics.poi": "https://assets.adobedtm.com/…/yourfile.json",
```

Mer information finns i [ADBMomobile JSON-konfiguration](/help/ios/configuration/json-config/json-config.md).

Om detta inte är konfigurerat uppdateras en version av `ADBMobile.json` filen måste hämtas och läggas till i appen. Mer information och instruktioner finns i *Ladda ned SDK och testverktyg* in [Innan du börjar](/help/ios/getting-started/requirements.md).

## Spåra geografiska platser och POI {#section_B1616E400A7548F9A672F97FEC75AE27}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i projektet* in [Kärnimplementering och livscykel](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Utlysning `trackLocation` för att spåra den aktuella platsen:

   ```objective-c
   CLLocation *currentLocation = location; 
   [ADBMobile trackLocation: currentLocation data: nil]; 
   ```

   >[!TIP]
   >
   >Du kan ringa `trackLocation` när som helst.

   Bestämma platsen som skickas till `trackLocation` anrop, använda [Hämta användarens plats](https://developer.apple.com/Library/ios/documentation/UserExperience/Conceptual/LocationAwarenessPG/CoreLocation/CoreLocation.html).

Om platsen bestäms till att vara i en definierad POI-radie, kan dessutom en `a.loc.poi` kontextdatavariabeln skickas in med `trackLocation` hit och rapporteras som en POI i platsrapporter. An `a.loc.dist` kontextvariabeln skickas också med avståndet i meter från de definierade koordinaterna.

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom platsdata kan du skicka ytterligare kontextdata med varje spårplatsanrop:

```objective-c
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
[contextData setObject:@"GPS" forKey:@"myapp.location.LocationSource"]; 
[ADBMobile trackLocation: currentLocation data:contextData];
```

Kontextdatavärden måste mappas till anpassade variabler:

![](assets/map-location-context-data.png)

## Kontextdata för plats {#section_FFB71E6653F9410A89CC6ACC0C9164A9}

Latitud och longitud skickas var och en med tre olika kontextdataparametrar, där varje parameter representerar olika precisionsnivåer, för totalt sex kontextdataparametrar.

Koordinaterna lat = 40,93231, lon = -111.93152 representerar en plats med 1 m precision. Platsen delas upp efter precisionsnivån för följande variabler:

* `a.loc.lat.a`= 040.9
* `a.loc.lat.b` = 32
* `a.loc.lat.c` = 31
* `a.loc.lon.a` = -111.9
* `a.loc.lon.b` = 31
* `a.loc.lon.c` = 52

Vissa precisionsnivåer kan visas som &quot;00&quot; beroende på den aktuella platsens precision. Om platsen till exempel är exakt 100 m, `a.loc.lat.c` och `a.loc.lon.c` kommer att fyllas i med &quot;00&quot;.

## Ytterligare information {#section_931AC1E0D88147E29FE1B6E3CC1E9550}

Kom ihåg följande information:

* A `trackLocation` begäran skickar i motsvarighet till en `trackAction` ring.

* POI skickas inte som en del av normal `trackAction` och `trackState` så du måste använda en `trackLocation` anrop för att spåra POI.

* `trackLocation` anropas så ofta som krävs för att spåra plats och POI.

   Vi rekommenderar att vi ringer `trackLocation` när appen startar och sedan efter behov utifrån programmets krav.

* POI fylls bara i efter att de har definierats i appkonfigurationsfilen.

   De tillämpas inte på historiska `trackLocation` samtal som skickats tidigare.
* `trackLocation` anropar stöd för att skicka ytterligare kontextdata som liknar `trackAction` samtal.

* När två POI har överlappande diametrar används den första POI som innehåller den aktuella platsen.

   Om dina POI överlappar ska du ange POI i ordning från den mest granulära till den minst granulära för att säkerställa att den mest detaljerade POI rapporteras.
