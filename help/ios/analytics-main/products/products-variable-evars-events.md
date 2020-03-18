---
description: Här är ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.
seo-description: Här är ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.
seo-title: Produkterna kan variera med Merchandising eVars och produktspecifika event
solution: Marketing Cloud,Analytics
title: Produkterna kan variera med Merchandising eVars och produktspecifika event
topic: Developer and implementation
uuid: f913211e-97ad-4237-bfe4-7ded01295caf
translation-type: tm+mt
source-git-commit: 06144a1695ac40ce984656491456968888f9e96e

---


# Produktvariabel med eVars för försäljning och produktspecifika händelser {#products-variable-with-merchandising-evars-and-product-specific-events}

Här är ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.

```
//create a context data dictionary 
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
  
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
[contextData setObject:@"event1" forKey:@"&&events"]; 
[contextData setObject:@";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99" forKey:@"&&products"]; 
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"]; 
[contextData setObject:@"1" forKey:@"m.purchase"]; 
  
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
[ADBMobile trackAction:@"purchase" data:contextData]; 
// trackState example: 
[ADBMobile trackState:@"Order Confirmation" data:contextData];
```

>[!TIP]
>
>Om du utlöser en produktspecifik händelse med hjälp av *`&&products`* variabeln måste du även ange den händelsen i *`&&events`* variabeln. Om du inte anger den händelsen filtreras den bort under bearbetningen.

