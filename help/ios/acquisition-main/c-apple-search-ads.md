---
description: Adobe SDK utnyttjar Apple API:er för sökannonsering i appattribut för att göra det möjligt för utvecklare och marknadsförare att spåra och attribuera appnedladdningar som kommer från sökannonskampanjer i Apple App Store.
solution: Experience Cloud Services,Analytics
title: Apple Search Ads
topic-fix: Developer and implementation
uuid: 790080e8-067e-4bfd-a169-0027db4fdff3
exl-id: efcdd430-f08d-4ee2-85f3-2697c3bd72db
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Apple Search Ads {#apple-search-ads}

Adobe SDK utnyttjar Apple API:er för sökannonsering i appattribut för att göra det möjligt för utvecklare och marknadsförare att spåra och attribuera appnedladdningar som kommer från sökannonskampanjer i Apple App Store. Mer information om Search Ad-kampanjer finns i [Apple Search Ads](https://searchads.apple.com).

## Fördelar {#section_CEA30C652AC8470784B8054E299B80FA}

Nedan följer några fördelar med att använda Apple-annonser:

* Mät enkelt hur effektiva era hämtningskampanjer för Search Ads-appar är genom att lägga till några kodrader i appen.
* Utvecklare kan komma åt datum/tid för nedladdningen och det budgade nyckelordet som driver konverteringen.

## Implementera Apple Ads {#section_F1094676793540CFA1DBB540174EEB6A}

>[!TIP]
>
>För att kunna implementera Apple Ads måste du ha iOS SDK version 4.13.2 eller senare.

Så här aktiverar du din app för sökannonsattribuering:

1. Implementera Adobe SDK version 4.13.2 eller senare.

   Mer information finns i [Kärnimplementering och livscykel](/help/ios/getting-started/dev-qs.md).

1. Lägg till iAd-ramverket i Xcode-projektfilen för din app.

## Rapportering om attribut för sökannonser {#section_1AF4E0B4F8E94F36B38CA3D3E384D0A4}

1. Apple Search Ads-attribueringsdata tillhandahålls i förvärvsnamn, källa och termvärden.

   If attribution = `true`, alla `iad-*` fält inkluderas i livscykelträffen.

   Dessutom kommer följande värden att mappas från `"iad"` ordbok för våra typiska datafält för kundvärvning:

   * `"iad-campaign-id"` --> `"a.referrer.campaign.trackingcode"`
   * `"iad-campaign-name"` —> `"a.referrer.campaign.name"`
   * `"iad-adgroup-id"` —> `"a.referrer.campaign.content"`
   * `"iad-keyword"` —> `"a.referrer.campaign.term"`
   Denna mappning säkerställer att värdena är tillgängliga i vår standardrapportering.
