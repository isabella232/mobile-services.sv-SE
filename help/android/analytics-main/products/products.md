---
description: Det går inte att ange variabeln products genom att använda bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern kontextdata för att ange produkter på serveranropet.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Produktvariabel
topic-fix: Developer and implementation
uuid: f4484022-cb8b-4dea-9209-5a110ba607df
exl-id: 1d850ce1-6fd4-463e-8949-8b8cf40d8467
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 1%

---

# Variabeln Produkter {#products-variable}

Det går inte att ange variabeln products genom att använda bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern kontextdata för att ange produkter på serveranropet.

Om du vill ställa in variabeln *products* anger du en kontextdatanyckel till `"&&products"` och anger värdet med den syntax som är definierad för variabeln *products*:

```java
cdata.put("&&products", "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]");
```

Exempel:

```java
//create a context data dictionary 
HashMap cdata = new HashMap<String, Object>(); 
 
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata.put("&&products", ";Running Shoes;1;69.95,;Running Socks;10;29.99"); 
cdata.put("myapp.purchase", "1"); 
cdata.put("myapp.purchaseid", "1234567890"); 
 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
Analytics.trackAction("purchase", cdata); 
// trackState example: 
Analytics.trackState("Order Confirmation", cdata);
```

Variabeln *products* ställs in på bildbegäran och de andra variablerna ställs in som kontextdata. Alla kontextdatavariabler måste mappas med bearbetningsregler:

![](assets/map-products.png)

Du behöver inte mappa variabeln *products* med bearbetningsregler eftersom variabeln anges direkt på SDK:ns bildbegäran.
