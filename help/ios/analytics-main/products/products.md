---
description: Det går inte att ange variabeln products genom att använda bearbetningsregler. I iOS 4.x SDK måste du använda en speciell syntax i parametern context data för att ange produkter direkt i serveranropet.
seo-description: Det går inte att ange variabeln products genom att använda bearbetningsregler. I iOS 4.x SDK måste du använda en speciell syntax i parametern context data för att ange produkter direkt i serveranropet.
seo-title: Produktvariabel
solution: Experience Cloud,Analytics
title: Produktvariabel
topic: Developer and implementation
uuid: 6ece4d27-ef86-435c-a6f7-bd76be1c95ca
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# Variabeln Produkter {#products-variable}

Det går inte att ange variabeln products genom att använda bearbetningsregler. I iOS 4.x SDK måste du använda en speciell syntax i parametern context data för att ange produkter direkt i serveranropet.

Om du vill ställa in *`products`* variabeln anger du en kontextdatanyckel till `"&&products"`och anger värdet med den syntax som är definierad för *`products`* variabeln:

```objective-c
[contextData setObject:@"Category;Product;Quantity;Price[,Category;Product;Quantity;Price]" forKey:@"&&products"];
```

Exempel:

```objective-c
//create a context data dictionary 
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
 
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
[contextData setObject:@";Running Shoes;1;69.95,;Running Socks;10;29.99" forKey:@"&&products"]; 
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"]; 
[contextData setObject:@"1" forKey:@"m.purchase"]; 
 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
[ADBMobile trackAction:@"purchase" data:contextData]; 
// trackState example: 
[ADBMobile trackState:@"Order Confirmation" data:contextData]; 
```

*`products`* ställs in direkt på bildbegäran och de andra variablerna ställs in som kontextdata. Alla kontextdatavariabler måste mappas med bearbetningsregler:

![](assets/map-products.png)

Du behöver inte mappa *`products`* variabeln med bearbetningsregler eftersom den ställs in direkt på SDK:ns bildbegäran.
