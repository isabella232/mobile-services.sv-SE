---
description: Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.
title: PII-eftersläpningar
uuid: 08f76a52-75dd-4fc1-b4cc-4f5eef93d0f7
exl-id: 180c21f7-0fba-4b9b-ab7f-7afe81b85f38
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# PII-återanslag {#pii-postbacks}

Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.

När du vill använda Adobe SDK för att samla in PII-filer bör du skicka ett PII-spårsamtal. Även om det här anropet möjliggör insamling av PII-data, skickar SDK inte data automatiskt till någon Adobe-slutpunkt. En PII-typ för återanslående måste konfigureras med rätt slutpunkt.

>[!TIP]
>
>En slutpunkt som stöder HTTPS krävs för att använda typen PII-återanslående.

## Spåra PII-återanslag {#section_36B967B888CF467EACCDEF61DFA0B12B}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i ditt projekt* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. När du är redo att hämta PII-filer ringer du `trackPII` för att skicka en träff för den här åtgärden, händelsen eller vyn:

   ```objective-c
   [ADBMobile collectPII data:nil];
   ```
