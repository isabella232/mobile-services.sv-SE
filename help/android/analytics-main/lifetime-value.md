---
description: Med livstidsvärdet kan du mäta och rikta in dig på ett livstidsvärde för varje Android-användare. Värdet kan användas för att lagra livstidsinköp, annonsvisningar, videokompletteringar, sociala resurser, fotoöverföringar och så vidare.
seo-description: Med livstidsvärdet kan du mäta och rikta in dig på ett livstidsvärde för varje Android-användare. Värdet kan användas för att lagra livstidsinköp, annonsvisningar, videokompletteringar, sociala resurser, fotoöverföringar och så vidare.
seo-title: Livstidsvärde för besökare
solution: Experience Cloud,Analytics
title: Livstidsvärde för besökare
topic-fix: Developer and implementation
uuid: ba0308de-282e-46f9-a14c-19fb6d5c363e
exl-id: 93c6d711-c7c0-4fca-93b2-6a6fc19377bd
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Livslängdsvärde för besökare {#visitor-lifetime-value}

Med livstidsvärdet kan du mäta och rikta in dig på ett livstidsvärde för varje Android-användare. Värdet kan användas för att lagra livstidsinköp, annonsvisningar, videokompletteringar, sociala resurser, fotoöverföringar och så vidare.

Varje gång du skickar ett värde med `trackLifetimeValueIncrease` läggs värdet till det befintliga värdet. Livstidsvärdet lagras på enheten och kan hämtas när som helst genom att anropa `lifetimeValue`.

## Spåra besökarens livstidsvärde {#section_390943A49AF841F2941E65D6DF2B3F5A}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Anropa `trackLifetimeValueIncrease` med beloppet för att öka värdet:

   ```java
   Analytics.trackLifetimeValueIncrease(BigDecimal.valueOf(5.0), null);
   ```

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom livstidsvärdet kan du även skicka ytterligare kontextdata för varje spårningsåtgärd:

```java
HashMap cdata = new HashMap<String, Object>(); 
cdata.put("myapp.ImageLiked", imageName); 
Analytics.trackLifetimeValueIncrease(BigDecimal.valueOf(5.0), cdata);
```

Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile-tjänster:

![](assets/map-variable-context-ltv.png)
