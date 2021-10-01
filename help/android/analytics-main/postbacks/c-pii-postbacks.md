---
description: Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.
title: PII-eftersläpningar
uuid: 8d1f1fb8-6842-478b-a164-e7f727755bd9
exl-id: 9f0b9d7b-e51d-477b-ae04-72ab09fbc6fd
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '161'
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

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   #import "ADBMobile.h"
   ```

1. När du är redo att hämta PII-filer ringer du `trackPII` för att skicka en träff för den här åtgärden, händelsen eller vyn:

   ```java
   Config.collectPII(new HashMap<String, Object>(){{
     put("key","value");
   }});
   ```
