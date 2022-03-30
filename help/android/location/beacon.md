---
description: Med Beacon tracking kan du mäta och inrikta dig på mikroplatser med iBeacon och Bluetooth Low Energy.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Beacon tracking
topic-fix: Developer and implementation
uuid: 16c1d267-85f4-4a6a-a6d3-d6ffb0f80b29
exl-id: b8493e9d-ed1c-4404-a218-47a18a9c8faa
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Beacon tracking {#beacon-tracking}

Med Beacon tracking kan du mäta och inrikta dig på mikroplatser med iBeacon och Bluetooth Low Energy.

Följande beacon-data skickas till Analytics och Target när `trackBeacon` anropas:

* `a.beacon.uuid` - Beacons ProximityUID
* `a.beacon.major` - Betydande nummer på beacon (t.ex. butiksnummer)
* `a.beacon.minor` - Ett mindre nummer på beacon (t.ex. ett unikt nummer i en butik)
* `a.beacon.prox` - Värdena 0-3 representerar hur nära användaren är beacon.

Här är vad dessa värden betyder:

* 0 = okänd
* 1 = omedelbar
* 2 = nära
* 3 = långt

Dessa beacon-data samlas in i mobillösningsvariabler.

## Spåra fyrar {#section_FC3F213545944A468B1E6D5D5C8E2F1F}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Samla beacon-plats.

   Det finns flera bibliotek från tredje part som kan skanna Bluetooth LE-beacons, beroende på beacons tillverkare.
1. När beacon-informationen har hämtats använder du följande anrop för att spåra platsen:

   ```java
   // assumed that the following variables will have been retrieved by the 3rd party beacon library 
   String beaconUUID; 
   String major; 
   String minor; 
   Analytics.BEACON_PROXIMITY proximity;  
   // BEACON_PROXIMITY is an enum available in the SDK. Number 0-3 representing how close the 
   // user is to the beacon. 0 unknown, 1 immediate, 2 near, 3 far.  
   Analytics.trackBeacon(beaconUUID, major, minor, proximity, null);
   ```

1. När användaren lämnar beacons närhet, rensa den aktuella beacon:

   ```java
   Analytics.clearBeacon();
   ```

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Utöver beacon-data kan du skicka ytterligare kontextdata med varje `trackBeacon` ring:

```java
HashMap cdata = new HashMap<String, Object>(); 
cdata.put("myapp.ImageLiked", imageName); 
Analytics.trackBeacon(beaconUUID, major, minor, proximity, cdata);
```

Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile-tjänsterna:

![](assets/map-variable-context-ltv.png)
