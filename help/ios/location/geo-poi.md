---
description: Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina iOS-appar.
seo-description: Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina iOS-appar.
seo-title: Geografisk placering och intressepunkter
solution: Marketing Cloud,Analytics
title: Geografisk placering och intressepunkter
topic: Developer and implementation
uuid: c800ec85-a33f-425d-b28f-bfe8bf229ae8
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Geografisk placering och intressepunkter {#geo-location-and-points-of-interest}

Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina iOS-appar.

Varje `trackLocation` samtal skickar följande:

* Latitud, longitud och plats i en intressepunkt (POI) som definieras i Adobes mobiltjänster.

   Den här informationen skickas till mobillösningsvariabler för automatisk rapportering.

* Avstånd från centrum och precision skickas som kontextdata.

   Dessa variabler hämtas inte automatiskt. Du måste mappa dessa kontextdatavariabler genom att använda instruktionerna i *Skicka ytterligare data* nedan.

## Dynamiska POI-uppdateringar {#section_3747B310DD5147E2AAE915E762997712}

Från och med version 4.2 definieras POI i Adobe Mobile-gränssnittet och synkroniseras dynamiskt till programkonfigurationsfilen. Synkroniseringen kräver en `analytics.poi` inställning i `ADBMobile.json` filen:

```js
“analytics.poi”: “https://assets.adobedtm.com/…/yourfile.json”,
```

Mer information finns i [ADBMomobile JSON Config](/help/ios/configuration/json-config/json-config.md).

Om detta inte är konfigurerat måste en uppdaterad version av `ADBMobile.json` filen hämtas och läggas till i ditt program. Mer information och instruktioner finns i *Hämta SDK och testverktygen* i [Innan du börjar](/help/ios/getting-started/requirements.md).

## Spåra geografiska platser och POI {#section_B1616E400A7548F9A672F97FEC75AE27}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Ring `trackLocation` för att spåra aktuell plats:

   ```objective-c
   CLLocation *currentLocation = location; 
   [ADBMobile trackLocation: currentLocation data: nil]; 
   ```

   >[!TIP]
   >
   >Du kan ringa `trackLocation` när som helst.

   Om du vill ta reda på platsen som skickas till `trackLocation` samtalet använder du [Hämta användarens plats](https://developer.apple.com/Library/ios/documentation/UserExperience/Conceptual/LocationAwarenessPG/CoreLocation/CoreLocation.html).

Om platsen identifieras som i en definierad POI-radie skickas dessutom en `a.loc.poi` kontextdatavariabel med `trackLocation` träffen och rapporteras som en POI i platsrapporter. En `a.loc.dist` sammanhangsvariabel skickas också med avståndet i meter från de definierade koordinaterna.

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

Vissa precisionsnivåer kan visas som &quot;00&quot; beroende på den aktuella platsens precision. Om platsen till exempel för närvarande är exakt 100 m, `a.loc.lat.c` och `a.loc.lon.c` fylls med &quot;00&quot;.

## Ytterligare information {#section_931AC1E0D88147E29FE1B6E3CC1E9550}

Kom ihåg följande information:

* En `trackLocation` begäran skickas som motsvarar ett `trackAction` samtal.

* POI skickas inte som en del av normala samtal `trackAction` och `trackState` samtal, så du måste använda ett `trackLocation` anrop för att spåra POI.

* `trackLocation` anropas så ofta som krävs för att spåra plats och POI.

   Vi rekommenderar att du ringer `trackLocation` när appen startar och sedan efter behov utifrån programmets krav.

* POI fylls bara i efter att de har definierats i appkonfigurationsfilen.

   De tillämpas inte på tidigare skickade `trackLocation` samtal.
* `trackLocation` anrop har stöd för att skicka ytterligare kontextdata som liknar `trackAction` anrop.

* När två POI har överlappande diametrar används den första POI som innehåller den aktuella platsen.

   Om dina POI överlappar ska du ange POI i ordning från den mest granulära till den minst granulära för att säkerställa att den mest detaljerade POI rapporteras.

