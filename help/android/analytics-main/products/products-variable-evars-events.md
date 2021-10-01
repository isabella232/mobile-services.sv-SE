---
description: Här är ett exempel på variabeln products med Merchandising eVars och produktspecifika händelser.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Produkterna kan variera med Merchandising eVars och produktspecifika event
topic-fix: Developer and implementation
uuid: 64f822a0-6ccf-48e7-8886-31b93d8198a3
exl-id: 2ede6341-3068-4423-a509-c0ec3a2db5e8
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '80'
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
>Om du utlöser en produktspecifik händelse med hjälp av variabeln *`&&products`* måste du även ange den händelsen i variabeln *`&&events`*. Om du inte anger den händelsen filtreras den bort under bearbetningen.
