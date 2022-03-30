---
description: Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.
solution: Experience Cloud Services,Analytics
title: Variabeln Produkter
topic-fix: Developer and implementation
uuid: 2057a564-06ae-4171-bbe7-0baffa71608b
exl-id: b731e794-7134-4c6d-a41b-09ac9b84763d
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 1%

---

# Variabeln Produkter{#products-variable}

Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.

Så här anger du *`products`* variabel, ange kontextdatanyckeln till `"&&products"`och ange värdet med den syntax som är definierad för *`products`*:

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

Du behöver inte mappa *`products`* variabeln med bearbetningsregler eftersom den anges direkt på SDK:s bildbegäran.
