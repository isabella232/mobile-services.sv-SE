---
description: Livstidsvärdet gör att du kan mäta och inrikta dig på ett livstidsvärde för varje användare.
solution: Experience Cloud Services,Analytics
title: Livslängd för besökare
topic-fix: Developer and implementation
uuid: d830d18b-4313-43bb-8d75-3789869d0f1d
exl-id: f1b684b1-9919-400d-a88a-6d4a0809d9e1
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Livslängd för besökare {#visitor-lifetime-value}

Livstidsvärdet gör att du kan mäta och inrikta dig på ett livstidsvärde för varje användare.

Varje gång du skickar in ett värde med `trackLifetimeValueIncrease`läggs värdet till det befintliga värdet. Livstidsvärdet lagras på enheten och kan hämtas när som helst genom att anropa `lifetimeValue`. Detta kan användas för att lagra livstidsinköp, annonsvisningar, videokompletteringar, sociala resurser, fotoöverföringar och så vidare.

## Spåra besökarens livstidsvärde {#section_390943A49AF841F2941E65D6DF2B3F5A}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i projektet* in [Kärnimplementering och livscykel](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   import com.adobe.mobile.*;
   ```

1. Utlysning `trackLifetimeValueIncrease` med beloppet som ska öka värdet:

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
