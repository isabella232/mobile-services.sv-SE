---
description: Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.
seo-description: Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.
seo-title: Variabeln Produkter
solution: Experience Cloud,Analytics
title: Variabeln Produkter
topic: Developer and implementation
uuid: 607983d6-48ac-4274-bfc8-b1ca4e5dad1b
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Variabeln Produkter {#products-variable}

Det går inte att ange variabeln products med bearbetningsregler. I mobil-SDK måste du använda en särskild syntax i parametern context data för att ange produkter direkt på serveranropet.

Om du vill ställa in *`products`* variabeln anger du en kontextdatanyckel till `"&&products"`och anger värdet med den syntax som är definierad för variabeln *`products` :

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

De *`products`* ställs in direkt på bildbegäran och de andra variablerna ställs in som kontextdata. Alla kontextdatavariabler måste mappas med bearbetningsregler:

![](assets/products-procrules.png)

Du behöver inte mappa *`products`* variabeln med bearbetningsregler eftersom den ställs in direkt på SDK:ns bildbegäran.

## Produktvariabel med eVars för försäljning och produktspecifika händelser {#section_685D53AD3D064F9A8E225F995A9BA545}

Ett exempel på *`products`* variabeln med Merchandising eVars och produktspecifika händelser.

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

