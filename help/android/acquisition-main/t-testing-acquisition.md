---
description: Följande information hjälper dig att skicka en länk till en äldre kundvärvningskampanj på en Android-enhet.
keywords: android;library;mobile;sdk
seo-description: Följande information hjälper dig att skicka en länk till en äldre kundvärvningskampanj på en Android-enhet.
seo-title: Testar tidigare förvärv
solution: Marketing Cloud,Analytics
title: Testar tidigare förvärv
topic: Developer and implementation
uuid: bb7ace96-68eb-4f43-b3cf-af80730b9cee
translation-type: tm+mt
source-git-commit: bf076aa8e59d5c3e634fc4ae21f0de0d4541a83f

---


# Testa tidigare förvärv {#testing-legacy-acquisition}

Följande information hjälper dig att skicka en länk till en äldre kundvärvningskampanj på en Android-enhet.

Om mobilappen ännu inte finns i Google Play kan du välja vilken mobilapp som helst som mål när du skapar kampanjlänken. Detta påverkar bara den app som förvärvsservern dirigerar om dig till, efter att du klickat på länken för förvärv, och inte möjligheten att testa länken för förvärv. Frågesträngsparametrar skickas till Google Play-butiken, som skickas till appen vid installationen som en del av en kampanjsändning. Testning av mobilappsförvärv kräver simulering av den här typen av sändning.

Appen måste vara nyligen installerad eller ha data rensade i **[!UICONTROL Settings]** varje gång ett test körs. Detta garanterar att de inledande livscykelvärdena som är kopplade till parametrarna för kampanjfrågesträngen skickas när appen startas första gången.

1. Generera en URL för en äldre anskaffningskampanj i gränssnittet för mobila tjänster.

   Mer information finns i [Använda länkar](/help/using/acquisition-main/c-marketing-links-builder/t-create-edit-adobe-links/c-use-legacy-acquisition-links/c-use-legacy-acquisition-links.md)för äldre anskaffning.
1. Anslut enheten till en dator, starta ADB Shell och starta programmet på enheten.
1. Skicka en sändning i följande format:

   ```
   am broadcast -a com.android.vending.INSTALL_REFERRER -n com.example.adobetesttapp/com.google.analytics.tracking.android.CampaignTrackingReceiver --es "referrer" "utm_source=testSource&utm_medium=testMedium&utm_term=testTerm&utm_content=testContent&utm_campaign=testCampaign&trackingcode=trackingvalue"
   ```

1. Utför följande steg:
   1. Ersätt `com.example.adobetesttapp.com` med programmets inverterade DNS-post.
   1. Uppdatera mottagarreferensen med kampanjspårningsmottagarplatsreferensen i din app.
   1. Ersätt värden som är kopplade till `utm_source`, `utm_medium`, `utm_term`, `utm_content`, `utm_campaign`och så vidare, med lämpliga värden.

Om sändningen lyckas visas ett svar som liknar det nedan:

```
Broadcasting: Intent { act=com.android.vending.INSTALL_REFERRER cmp=com.example.analyticsecommtest/com.google.analytics.tracking.android.AnalyticsReceiver has extras) } Broadcast completed: result=0
```

Du ser också en bildförfrågan som skickas till Adobes datainsamlingsservrar. Om SDK väntar på den fullständiga tidslängden för referenstimeout, som du angav i steg 1, med en bildbegäran som inte innehåller kampanjparametrar, misslyckades sändningen.
