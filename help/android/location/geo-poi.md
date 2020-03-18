---
description: Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina Android-appar.
seo-description: Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina Android-appar.
seo-title: Geografisk placering och intressepunkter
solution: Marketing Cloud,Analytics
title: Geografisk placering och intressepunkter
topic: Developer and implementation
uuid: b8209370-cbc4-40f9-97d8-017e2d74a377
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Geografisk placering och intressepunkter {#geo-location-and-points-of-interest}

Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina Android-appar.

Varje `trackLocation` samtal skickar följande information:

* Latitud, longitud och plats i en intressepunkt (POI) som definieras i användargränssnittet för Adobe Mobile Services.

   Den här informationen skickas till mobillösningsvariabler för automatisk rapportering.

* Avstånd från centrum och precision skickas som kontextdata.

   Dessa variabler hämtas inte automatiskt. Du måste mappa dessa kontextdatavariabler genom att använda instruktionerna i avsnittet *Skicka ytterligare data* nedan.

## Dynamiska POI-uppdateringar {#section_3747B310DD5147E2AAE915E762997712}

Från och med version 4.2 definieras POI i användargränssnittet för Adobe Mobile och synkroniseras dynamiskt till programkonfigurationsfilen. Synkroniseringen kräver en `analytics.poi` inställning i [ADBMomobile JSON-konfigurationen](/help/android/configuration/json-config/json-config.md):

```js
“analytics.poi”: “https://assets.adobedtm.com/…/yourfile.json”,
```

Om detta inte är konfigurerat måste du hämta en uppdaterad version av `ADBMobile.json` filen och lägga till den i programmet. Mer information finns i [Hämta SDK och testverktyg](/help/android/getting-started/requirements.md).

## Spåra geolokalisering och POI {#section_B1616E400A7548F9A672F97FEC75AE27}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Ring `trackLocation` för att spåra aktuell plats:

   ```java
   Location currentLocation = new Location("my location here"); 
   Analytics.trackLocation(currentLocation, null);
   ```

   >[!TIP]
   >
   >Du kan ringa `trackLocation` när som helst.

   Du kan använda platsstrategier för att fastställa platsen som skickas till `trackLocation` samtalet. Mer information finns i Platsstrategier för [Android](https://developer.android.com/guide/topics/location/strategies.html).

Dessutom, om platsen identifieras som i en definierad POI-radie, skickas en `a.loc.poi` kontextdatavariabel in med `trackLocation` träffen och rapporteras som en POI i **[!UICONTROL Location Breakdown]** rapporterna. En `a.loc.dist` sammanhangsvariabel skickas också med avståndet i meter från de definierade koordinaterna.

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom platsdata kan du skicka ytterligare kontextdata med varje spårplatsanrop:

```java
HashMap<String, Object> locationContextData = new HashMap<String, Object>(); 
locationContextData.put("myapp.location.LocationSource", "GPS"); 
 
Location currentLocation = new Location("my location here"); 
Analytics.trackLocation(currentLocation, locationContextData);
```

Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile Services-gränssnittet:

![](assets/map-location-context-data.png)

## Kontextdata för plats {#section_FFB71E6653F9410A89CC6ACC0C9164A9}

Latitud och longitud skickas med tre olika kontextdataparametrar, där varje parameter representerar olika precisionsnivåer, för totalt sex kontextdataparametrar.

Koordinaterna lat = 40,93231, long = -111.93152 representerar en plats med 1 m precision. Platsen delas upp efter precisionsnivån för följande variabler:

`a.loc.lat.a`= 040.9

`a.loc.lat.b` = 32

`a.loc.lat.c` = 31

`a.loc.lon.a` = -111.9

`a.loc.lon.b` = 31

`a.loc.lon.c` = 52

Vissa precisionsnivåer kan visas som `00` beroende på den aktuella platsens precision. Om platsen till exempel är exakt 100 m, `a.loc.lat.c` och `a.loc.lon.c` fylls med `00`.

Kom ihåg följande information:

* En `trackLocation` begäran skickas som motsvarar ett `trackAction` samtal.

* POI skickas inte som en del av vanliga `trackAction` samtal och `trackState` samtal, så du måste använda ett `trackLocation` anrop för att spåra POI.

* `trackLocation` anropas så ofta som krävs för att spåra plats och POI.

   Vi rekommenderar att du ringer `trackLocation` när appen startar och sedan efter behov, beroende på appens krav.

* POI fylls bara i efter att de har definierats i programmets konfigurationsfil.

   PoI används inte för tidigare `trackLocation` anrop.
* `trackLocation` anrop har stöd för att skicka ytterligare kontextdata som liknar `trackAction` anrop.

* När två POI har överlappande diametrar används den första POI som innehåller den aktuella platsen.

   Om dina POI överlappar bör du ange POI i ordningen för de flesta till minst granulära för att säkerställa att den mest detaljerade POI rapporteras.

