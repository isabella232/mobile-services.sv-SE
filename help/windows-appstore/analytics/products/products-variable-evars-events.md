---
description: Ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.
seo-description: Ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.
seo-title: Produkterna kan variera med Merchandising eVars och produktspecifika event
solution: Marketing Cloud,Analytics
title: Produkterna kan variera med Merchandising eVars och produktspecifika event
topic: Developer and implementation
uuid: 94e882e4-b19d-4c48-9dfb-331465490347
translation-type: tm+mt
source-git-commit: b630c5cf09be7fbe31018cbf50564001eb6e2a5a

---


# Produktvariabel med eVars för försäljning och produktspecifika händelser{#products-variable-with-merchandising-evars-and-product-specific-events}

Ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.

```
//create a context data dictionary 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
  
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata["&&events"] = "event1 "; 
cdata["&&products"] = ";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99"; 
cdata["m.purchaseid"] = "1234567890"; 
cdata["m.purchase"] = "1"; 
  
var ADB = ADBMobile; 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
ADB.Analytics.trackAction("purchase", cdata); 
// trackState example: 
ADB.Analytics.trackState("Order Confirmation", cdata);
```

>[!TIP]
>
>Om du utlöser en produktspecifik händelse med hjälp av *`&&products`* variabeln måste du även ange den händelsen i *`&&events`* variabeln, annars filtreras händelsen bort under bearbetningen.

