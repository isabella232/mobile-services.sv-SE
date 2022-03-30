---
description: Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina Android-appar.
solution: Experience Cloud Services,Analytics
title: Geografisk placering och intressepunkter
topic-fix: Developer and implementation
uuid: b8209370-cbc4-40f9-97d8-017e2d74a377
exl-id: e1fed35b-5ce9-48ee-ade0-b1701cf2a3a9
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# Geografisk placering och intressepunkter {#geo-location-and-points-of-interest}

Med geopositionering kan du mäta positionsdata genom att använda latitud och longitud samt fördefinierade intressepunkter i dina Android-appar.

Varje `trackLocation` call skickar följande information:

* Latitud, longitud och plats i en intressepunkt (POI) som definieras i användargränssnittet för Mobile-tjänster i Adobe.

   Den här informationen skickas till mobillösningsvariabler för automatisk rapportering.

* Avstånd från centrum och precision skickas som kontextdata.

   Dessa variabler hämtas inte automatiskt. Du måste mappa dessa kontextdatavariabler med hjälp av instruktionerna i *Skicka ytterligare data* nedan.

## Dynamiska POI-uppdateringar {#section_3747B310DD5147E2AAE915E762997712}

Från och med version 4.2 definieras POI i användargränssnittet i Adobe Mobile och synkroniseras dynamiskt med programkonfigurationsfilen. Synkroniseringen kräver en `analytics.poi` i [ADBMomobile JSON-konfiguration](/help/android/configuration/json-config/json-config.md):

```js
"analytics.poi": "https://assets.adobedtm.com/…/yourfile.json",
```

Om detta inte är konfigurerat måste du hämta en uppdaterad version av `ADBMobile.json` och lägga till den i appen. Mer information finns i [Ladda ned SDK och testverktyg](/help/android/getting-started/requirements.md).

## Spåra geolokalisering och POI {#section_B1616E400A7548F9A672F97FEC75AE27}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Utlysning `trackLocation` för att spåra den aktuella platsen:

   ```java
   Location currentLocation = new Location("my location here"); 
   Analytics.trackLocation(currentLocation, null);
   ```

   >[!TIP]
   >
   >Du kan ringa `trackLocation` när som helst.

   Du kan använda platsstrategier för att bestämma platsen som skickas till `trackLocation` ring. Mer information finns i [Platsstrategier för Android](https://developer.android.com/guide/topics/location/strategies.html).

Om platsen bestäms till att vara i en definierad POI-radie, kan dessutom en `a.loc.poi` kontextdatavariabeln skickas in med `trackLocation` hit och rapporteras som en POI på **[!UICONTROL Location Breakdown]** rapporter. An `a.loc.dist` kontextvariabeln skickas också med avståndet i meter från de definierade koordinaterna.

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

Vissa precisionsnivåer kan visas som `00` beroende på den aktuella platsens noggrannhet. Om platsen till exempel är exakt 100 m, `a.loc.lat.c` och `a.loc.lon.c` kommer att fyllas med `00`.

Kom ihåg följande information:

* A `trackLocation` begäran skickar i motsvarighet till en `trackAction` ring.

* POI skickas inte som en del av typiska `trackAction` och `trackState` så du måste använda en `trackLocation` anrop för att spåra POI.

* `trackLocation` anropas så ofta som krävs för att spåra plats och POI.

   Vi rekommenderar att vi ringer `trackLocation` när appen startar och sedan efter behov, beroende på appens krav.

* POI fylls bara i efter att de har definierats i programmets konfigurationsfil.

   POI tillämpas inte på historiska `trackLocation` tidigare skickade samtal.
* `trackLocation` anropar stöd för att skicka ytterligare kontextdata som liknar `trackAction` samtal.

* När två POI har överlappande diametrar används den första POI som innehåller den aktuella platsen.

   Om dina POI överlappar bör du ange POI i ordningen för de flesta till minst granulära för att säkerställa att den mest detaljerade POI rapporteras.
