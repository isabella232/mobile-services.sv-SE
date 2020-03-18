---
description: Med iBeacon-spårning kan du mäta och inrikta dig på mikroplatser med iBeacon och Bluetooth med låg energinivå.
seo-description: Med iBeacon-spårning kan du mäta och inrikta dig på mikroplatser med iBeacon och Bluetooth med låg energinivå.
seo-title: Spårning av iBeacon
solution: Marketing Cloud,Analytics
title: Spårning av iBeacon
topic: Developer and implementation
uuid: 390883db-027e-4d12-8a16-86d514579db1
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Spårning av iBeacon {#ibeacon-tracking}

Med iBeacon-spårning kan du mäta och inrikta dig på mikroplatser med iBeacon och Bluetooth med låg energinivå.

Följande beacon-data skickas till Analytics och Target när `trackBeacon` anropas:

* `a.beacon.uuid` - Beacons ProximityUID
* `a.beacon.major` - Betydande nummer på beacon, t.ex. butiksnummer
* `a.beacon.minor` - Ett mindre nummer, t.ex. ett unikt nummer i en butik
* `a.beacon.prox` - Följande värden visar hur nära användaren är beacon:

   * `0` är okänd
   * `1` är omedelbart
   * `2` är nära
   * `3` är långt

## Spåra iBeacons {#section_FC3F213545944A468B1E6D5D5C8E2F1F}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. När en enhet är inom närheten av en signal, ring `trackBeacon`:

   ```objective-c
   [ADBMobile trackBeacon:beacon data:nil];
   ```

1. När användaren lämnar fyndet rensar du den aktuella fyren:

   ```objective-c
   [ADBMobile trackingClearCurrentBeacon];
   ```

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom det tidsbestämda åtgärdsnamnet kan du skicka ytterligare kontextdata med varje spårningsåtgärdsanrop:

```objective-c
[ADBMobile trackBeacon:beacon data:@{@"myapp.ImageLiked" : imageName}];
```

Kontextdatavärden måste mappas till anpassade variabler:

![](assets/map-variable-context-ltv.png)

## Exempel {#section_9749238BCBC148998CB18E97D7670D19}

```objective-c
- (void)locationManager:(CLLocationManager *)manager didRangeBeacons:(NSArray *)beacons inRegion:(CLBeaconRegion *)region { 
    if (beacons.count > 0) { 
        CLBeacon *beacon = beacons[0]; 
        // Adobe - track when in range of a beacon 
        [ADBMobile trackBeacon:beacon data:@{@"sampleContextData" : @"sampleContextDataVal"}]; 
    } 
} 
 
// When the user leaves the proximity of the beacon, clear the current beacon 
[ADBMobile trackingClearCurrentBeacon];
```
