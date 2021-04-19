---
description: Livstidsvärdet gör att du kan mäta och inrikta dig på ett livstidsvärde för varje användare.
seo-description: Livstidsvärdet gör att du kan mäta och inrikta dig på ett livstidsvärde för varje användare.
seo-title: Livslängd för besökare
solution: Experience Cloud,Analytics
title: Livslängd för besökare
topic-fix: Developer and implementation
uuid: d830d18b-4313-43bb-8d75-3789869d0f1d
exl-id: f1b684b1-9919-400d-a88a-6d4a0809d9e1
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Livslängdsvärde för besökare {#visitor-lifetime-value}

Livstidsvärdet gör att du kan mäta och inrikta dig på ett livstidsvärde för varje användare.

Varje gång du skickar ett värde med `trackLifetimeValueIncrease` läggs värdet till det befintliga värdet. Livstidsvärdet lagras på enheten och kan hämtas när som helst genom att anropa `lifetimeValue`. Detta kan användas för att lagra livstidsinköp, annonsvisningar, videokompletteringar, sociala resurser, fotoöverföringar och så vidare.

## Spåra besökarens livstidsvärde {#section_390943A49AF841F2941E65D6DF2B3F5A}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i ditt projekt* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   import com.adobe.mobile.*;
   ```

1. Anropa `trackLifetimeValueIncrease` med beloppet för att öka värdet:

   ```objective-c
   [ADBMobile trackLifetimeValueIncrease:increaseAmount data:nil];
   ```

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom livstidsvärdet kan du skicka ytterligare kontextdata med varje spårningsåtgärdsanrop:

```objective-c
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
[contextData setObject:imageName forKey:@"myapp.ImageLiked"]; 
[ADBMobile trackLifetimeValueIncrease:increaseAmount data:contextData];
```

Kontextdatavärden måste mappas till anpassade variabler:

![](assets/map-variable-context-ltv.png)
