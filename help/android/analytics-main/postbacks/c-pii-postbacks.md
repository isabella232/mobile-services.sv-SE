---
description: Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.
seo-description: Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.
seo-title: PII-eftersläpningar
title: PII-eftersläpningar
uuid: 8d1f1fb8-6842-478b-a164-e7f727755bd9
translation-type: tm+mt
source-git-commit: 7ae626be4d71641c6efb127cf5b1d3e18fccb907
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# PII-återanslag {#pii-postbacks}

Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.

När du vill använda Adobe SDK för att samla in PII-filer bör du skicka ett PII-spårsamtal. Även om det här anropet möjliggör insamling av PII-data, skickar SDK inte data automatiskt till en Adobe-slutpunkt. En PII-typ för återanslående måste konfigureras med rätt slutpunkt.

>[!TIP]
>
>En slutpunkt som stöder HTTPS krävs för att använda typen PII-återanslående.

## Spåra PII-återanslag {#section_36B967B888CF467EACCDEF61DFA0B12B}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   #import "ADBMobile.h"
   ```

1. När du är redo att hämta PII, anropa `trackPII` för att skicka en träff för den här åtgärden, händelsen eller vyn:

   ```java
   Config.collectPII(new HashMap<String, Object>(){{
     put("key","value");
   }});
   ```

