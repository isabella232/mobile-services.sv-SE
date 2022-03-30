---
description: Med tidsbestämda åtgärder kan du mäta tiden i appen och den totala tiden mellan åtgärdens början och slut. SDK beräknar tiden för varje session och den totala tiden mellan sessioner som behövs för att åtgärden ska kunna slutföras. Du kan använda tidsbestämda åtgärder för att definiera segment och jämföra tiden för inköp, skicka-nivå, utcheckningsflöde och så vidare.
solution: Experience Cloud Services,Analytics
title: Tidsbestämda åtgärder
topic-fix: Developer and implementation
uuid: dbcbac5a-6345-49f6-b050-0db05292f005
exl-id: 3499766b-55f6-4861-8291-2269d56ba983
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Tidsbestämda åtgärder {#timed-actions}

Med tidsbestämda åtgärder kan du mäta tiden i appen och den totala tiden mellan åtgärdens början och slut. SDK beräknar tiden för varje session och den totala tiden mellan sessioner som behövs för att åtgärden ska kunna slutföras. Du kan använda tidsbestämda åtgärder för att definiera segment och jämföra tiden för inköp, skicka-nivå, utcheckningsflöde och så vidare.

Följande mått rapporteras för tidsbestämda åtgärder:

* Totalt antal sekunder i programmet mellan start och slut - tvärsessioner
* Totalt antal sekunder mellan start och slut (klocktid)

Med ett valfritt återanrop kan du utföra ytterligare åtgärder när tidsåtgärden har slutförts:

* Kör kod och lägg till eventuell logik - valfri anpassad logik baserad på varaktighetsresultat.
* Lägg till kontextdata innan varaktigheterna skickas.
* Avbryt träff och varaktighet har inte skickats än.

## Spåra tidsbestämda åtgärder {#section_FF5B1EDC1A5340A5B13BC0F1BF2E13E1}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i projektet* in [Kärnimplementering och livscykel](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Utlysning `trackTimedActionStart` och ange ett namn på en tidsbestämd åtgärd och valfria kontextdata.

   ```objective-c
   [ADBMobile trackTimedActionStart:@"TimeUntilPurchase"  
                               data:@{@"ExperienceName" : experience}];
   ```

1. (Valfritt) Om du vill lägga till ytterligare kontextdata kan du ringa `trackTimedActionUpdate` med det tidsbestämda åtgärdsnamnet.

   ```objective-c
   [ADBMobile trackTimedActionUpdate:@"TimeUntilPurchase"  
                                data:@{@"myapp.ImageLiked" : imageName}];
   ```

1. När händelsen är klar, ring `trackTimedActionEnd` och skicka timed funktionsmakrots namn och `TimedActionBlock` (återanrop), som söker upp alla data och beräknar varaktighet.

   Tidsbestämda händelsemått sparas i mobillösningens variabler för automatisk rapportering.

   ```objective-c
   [ADBMobile trackTimedActionEnd:@"TimeUntilPurchase"  
                            logic:nil];
   ```

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Utöver det tidsbestämda åtgärdsnamnet kan du skicka ytterligare kontextdata med åtgärdsstart och åtgärdsuppdateringsanrop:

```objective-c
[ADBMobile trackTimedActionUpdate:@"TimeUntilPurchase"  
                             data:@{@"myapp.ImageLiked" : imageName}];
```

Kontextdatavärden måste mappas till anpassade variabler:

![](assets/map-variable-context-ltv.png)

## Exempel {#section_7BA344B8BD4F48DCBAE27AC9320CBCEA}

```objective-c
// Timed Action Start Example 
[ADBMobile trackTimedActionStart:@"TimeUntilPurchase"  
                            data:@{@"ExperienceName" : experience}];

// Timed Action Update Example 
[ADBMobile trackTimedActionUpdate:@"TimeUntilPurchase"  
                             data:@{@"ImageLiked" : imageName}];

// Timed Action End Example 
[ADBMobile trackTimedActionEnd:@"TimeUntilPurchase"  
                         logic:nil]; 
 
// Timed Action End Example with Callback 
[ADBMobile trackTimedActionEnd:@"TimeUntilPurchase"  
                         logic:^BOOL(NSTimeInterval inAppDuration,  
                                     NSTimeInterval totalDuration,  
                                     NSMutableDictionary *data) { 
                                        [data setObject:@"PurchaseItem" forKey:@"Item453"]; 
                                        return YES; //return YES to send the hit, NO to cancel 
                                     }];
```
