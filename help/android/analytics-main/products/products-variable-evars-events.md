---
description: Här är ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.
keywords: android;library;mobile;sdk
seo-description: Här är ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.
seo-title: Produkterna kan variera med Merchandising eVars och produktspecifika event
solution: Experience Cloud,Analytics
title: Produkterna kan variera med Merchandising eVars och produktspecifika event
topic: Developer and implementation
uuid: 64f822a0-6ccf-48e7-8886-31b93d8198a3
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Produktvariabel med eVars för försäljning och produktspecifika händelser {#products-variable-with-merchandising-evars-and-product-specific-events}

Här är ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.

```java
//create a context data dictionary 
HashMap cdata = new HashMap<String, Object>(); 
  
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata.put("&&events", "event1"); 
cdata.put("&&products", ";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99"); 
cdata.put("myapp.purchase", "1"); 
cdata.put("myapp.purchaseid", "1234567890"); 
  
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
Analytics.trackAction("purchase", cdata); 
// trackState example: 
Analytics.trackState("Order Confirmation", cdata);
```

>[!TIP]
>
>Om du utlöser en produktspecifik händelse med hjälp av *`&&products`* variabeln måste du även ange den händelsen i *`&&events`* variabeln. Om du inte anger den händelsen filtreras den bort under bearbetningen.

