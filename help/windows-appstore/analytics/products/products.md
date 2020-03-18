---
description: Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.
seo-description: Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.
seo-title: Variabeln Produkter
solution: Marketing Cloud,Analytics
title: Variabeln Produkter
topic: Developer and implementation
uuid: 2057a564-06ae-4171-bbe7-0baffa71608b
translation-type: tm+mt
source-git-commit: 7aff336586058302046a728a0b1b0ce12660c1ba

---


# Variabeln Produkter{#products-variable}

Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.

Om du vill ställa in *`products`* variabeln anger du en kontextdatanyckel till `"&&products"`och anger värdet med den syntax som är definierad för *`products`*:

```js
cdata["&&products"] = "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]";
```

Exempel:

```js
//create a context data dictionary 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
 
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata["&&products"] = ";Running Shoes;1;69.95,;Running Socks;10;29.99"; 
cdata["m.purchaseid"] = "1234567890"; 
cdata["m.purchase"] = "1"; 
 
var ADB = ADBMobile; 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
ADB.Analytics.trackAction("purchase", cdata); 
// trackState example: 
ADB.Analytics.trackState("Order Confirmation", cdata);
```

*`products`* ställs in direkt på bildbegäran och de andra variablerna ställs in som kontextdata. Alla kontextdatavariabler måste mappas med bearbetningsregler:

![](assets/products-procrules.png)

Du behöver inte mappa *`products`* variabeln med bearbetningsregler eftersom den ställs in direkt på SDK:ns bildbegäran.
