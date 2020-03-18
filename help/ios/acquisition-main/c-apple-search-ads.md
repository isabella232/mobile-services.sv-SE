---
description: Adobe SDK utnyttjar Apples API:er för sökannonsering i appattribut så att utvecklare och marknadsförare kan spåra och attributera appnedladdningar som kommer från sökannonskampanjer i Apple App Store.
seo-description: Adobe SDK utnyttjar Apples API:er för sökannonsering i appattribut så att utvecklare och marknadsförare kan spåra och attributera appnedladdningar som kommer från sökannonskampanjer i Apple App Store.
seo-title: Apple Search Ads
solution: Marketing Cloud,Analytics
title: Apple Search Ads
topic: Developer and implementation
uuid: 790080e8-067e-4bfd-a169-0027db4fdff3
translation-type: tm+mt
source-git-commit: ebcc04ab3e80aafb9d9ec2e1fbc809c743554cb7

---


# Apple Search Ads {#apple-search-ads}

Adobe SDK utnyttjar Apples API:er för sökannonsering i appattribut så att utvecklare och marknadsförare kan spåra och attributera appnedladdningar som kommer från sökannonskampanjer i Apple App Store. Mer information om sökannonskampanjer finns i [Apple Search Ads](https://searchads.apple.com).

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

   Mer information finns i [Core-implementering och livscykel](/help/ios/getting-started/dev-qs.md).

1. Lägg till iAd-ramverket i Xcode-projektfilen för din app.

## Rapportering om attribut för sökannonser {#section_1AF4E0B4F8E94F36B38CA3D3E384D0A4}

1. Apple Search Ads-attribueringsdata anges i förvärvsnamn, källa och termvärden.

   Om attribution = `true`, inkluderas alla `iad-*` fält i livscykelträffen.

   Dessutom kommer följande värden att mappas från `"iad"` ordlistan till datafälten för det typiska kundvärvningssammanhanget:

   * `"iad-campaign-id"` --> `"a.referrer.campaign.trackingcode"`
   * `"iad-campaign-name"` --> `"a.referrer.campaign.name"`
   * `"iad-adgroup-id"` --> `"a.referrer.campaign.content"`
   * `"iad-keyword"` --> `"a.referrer.campaign.term"`
   Denna mappning säkerställer att värdena är tillgängliga i vår standardrapportering.
