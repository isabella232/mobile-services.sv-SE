---
description: Det går inte att ange variabeln products genom att använda bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern kontextdata för att ange produkter på serveranropet.
keywords: android;library;mobile;sdk
seo-description: Det går inte att ange variabeln products genom att använda bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern kontextdata för att ange produkter på serveranropet.
seo-title: Variabeln Produkter
solution: Marketing Cloud,Analytics
title: Variabeln Produkter
topic: Developer and implementation
uuid: f4484022-cb8b-4dea-9209-5a110ba607df
translation-type: tm+mt
source-git-commit: 7aff336586058302046a728a0b1b0ce12660c1ba

---


# Variabeln Produkter {#products-variable}

Det går inte att ange variabeln products genom att använda bearbetningsregler. I Mobile SDK måste du använda en speciell syntax i parametern kontextdata för att ange produkter på serveranropet.

Om du vill ställa in *variabeln products* anger du en kontextdatanyckel till `"&&products"`och anger värdet med den syntax som är definierad för *variabeln products* :

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

Du behöver inte mappa *produktvariabeln* med bearbetningsregler eftersom den här variabeln ställs in direkt på SDK:ns bildbegäran.
