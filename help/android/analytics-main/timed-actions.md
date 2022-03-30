---
description: Med tidsbestämda åtgärder kan du mäta tiden i appen och den totala tiden mellan åtgärdens början och slut. SDK beräknar tiden för varje session och den totala tiden mellan sessionerna som behövs för att åtgärden ska kunna slutföras. Du kan använda tidsbestämda åtgärder för att definiera segment och jämföra tiden för inköp, skicka-nivå, utcheckningsflöde och så vidare.
solution: Experience Cloud Services,Analytics
title: Tidsbestämda åtgärder
topic-fix: Developer and implementation
uuid: 5a48a580-b942-4e49-9f1b-078fea7fccdb
exl-id: d9851440-6e65-4d89-a6b3-81c8abd2bf06
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Tidsbestämda åtgärder {#timed-actions}

Med tidsbestämda åtgärder kan du mäta tiden i appen och den totala tiden mellan åtgärdens början och slut. SDK beräknar tiden för varje session och den totala tiden mellan sessionerna som behövs för att åtgärden ska kunna slutföras. Du kan använda tidsbestämda åtgärder för att definiera segment och jämföra tiden för inköp, skicka-nivå, utcheckningsflöde och så vidare.

Följande mått rapporteras för tidsbestämda åtgärder:

* Totalt antal sekunder i programmet mellan start och slut (korssessioner)
* Totalt antal sekunder mellan start och slut (klocktid)

Med ett valfritt återanrop kan du utföra ytterligare åtgärder när tidsåtgärden har slutförts:

* Kör kod och lägg till eventuell logik - valfri anpassad logik baserad på varaktighetsresultat.
* Lägg till kontextdata innan varaktigheterna skickas.
* Avbryt träff och varaktighet har inte skickats än.

## Spåra tidsbestämda åtgärder {#section_FF5B1EDC1A5340A5B13BC0F1BF2E13E1}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livstid](/help/android/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Utlysning `trackTimedActionStart` och ange ett namn på en tidsbestämd åtgärd och valfria kontextdata.

   ```java
   HashMap cdata = new HashMap<String, Object>(); 
   cdata.put("ExperienceName", experience); 
   Analytics.trackTimedActionStart("TimeUntilPurchase", cdata);
   ```

1. (Valfritt) Du kan ringa `trackTimedActionUpdate` med det tidsbestämda åtgärdsnamnet för att lägga till ytterligare kontextdata.

   ```java
   HashMap cdata = new HashMap<String, Object>(); 
   cdata.put("myapp.ImageLiked", imageName); 
   Analytics.trackTimed​ActionUpdate("TimeUntilPurchase", cdata);
   ```

1. När händelsen är klar, ring `trackTimedActionEnd` och skicka timed funktionsmakrots namn och `TimedActionBlock` (återanrop), som söker upp alla data och beräknar varaktighet.

   ```java
   Analytics.trackTimedActionEnd("TimeUntilPurchase", cdata);
   ```

   Tidsbestämda händelsemått sparas i mobillösningens variabler för automatisk rapportering.

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom det tidsbestämda åtgärdsnamnet kan du även skicka ytterligare kontextdata med åtgärdsstart och åtgärdsuppdateringsanrop:

```java
HashMap cdata = new HashMap<String, Object>(); 
cdata.put("myapp.ImageLiked", imageName); 
Analytics.trackTimed​ActionUpdate("TimeUntilPurchase", cdata);
```

Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile-tjänster:

![](assets/map-variable-context-ltv.png)

## Exempel {#section_7BA344B8BD4F48DCBAE27AC9320CBCEA}

```java
// Timed Action Start Example 
HashMap cdata = new HashMap<String, Object>(); 
cdata.put("ExperienceName", experience); 
Analytics.trackTimedActionStart("TimeUntilPurchase", cdata); 
 
// Timed Action Update Example 
cdata = new HashMap<String, Object>(); 
cdata.put("ImageLiked", imageName); 
Analytics.trackTimed​ActionUpdate("TimeUntilPurchase", cdata); 
 
// Timed Action End Example 
Analytics.trackTimedActionEnd("TimeUntilPurchase", null); 
 
// Timed Action End Example with Callback 
Analytics.trackTimedActionEnd("TimeUntilPurchase", new Analytics.TimedActionBlock<Boolean>() { 
 @Override 
 public Boolean call(long inAppDuration, long totalDuration, Map<String, Object> contextData) { 
  contextData.put("PurchaseItem", "Item453"); 
  return true; // return true to send the hit, false to cancel 
 } 
});
```
