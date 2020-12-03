---
description: Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.
seo-description: Du kan använda Adobe SDK för att samla in personligt identifierbar information (PII) och skicka den till en tredje parts slutpunkt.
seo-title: PII-eftersläpningar
title: PII-eftersläpningar
uuid: 08f76a52-75dd-4fc1-b4cc-4f5eef93d0f7
translation-type: tm+mt
source-git-commit: 06144a1695ac40ce984656491456968888f9e96e
workflow-type: tm+mt
source-wordcount: '178'
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

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. När du är redo att hämta PII, anropa `trackPII` för att skicka en träff för den här åtgärden, händelsen eller vyn:

   ```objective-c
   [ADBMobile collectPII data:nil];
   ```

