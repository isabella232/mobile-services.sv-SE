---
description: Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.
solution: Experience Cloud,Analytics
title: Variabeln Produkter
topic-fix: Developer and implementation
uuid: 607983d6-48ac-4274-bfc8-b1ca4e5dad1b
exl-id: 0575236c-9858-4bf9-a2ce-6e2667d58ddd
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---

# Variabeln Produkter {#products-variable}

Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.

Om du vill ställa in variabeln *`products`* anger du en kontextdatanyckel till `"&&products"` och anger värdet med den syntax som är definierad för variabeln *`products`:

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

Du behöver inte mappa variabeln *`products`* med bearbetningsregler eftersom den anges direkt på SDK:ns bildbegäran.

## Produktvariabel med eVars för försäljning och produktspecifika händelser {#section_685D53AD3D064F9A8E225F995A9BA545}

Ett exempel på variabeln *`products`* med Merchandising eVars och produktspecifika händelser.

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
>Om du utlöser en produktspecifik händelse med variabeln *`&&products`* måste du även ange den händelsen i variabeln *`&&events`*, annars filtreras händelsen bort under bearbetningen.
