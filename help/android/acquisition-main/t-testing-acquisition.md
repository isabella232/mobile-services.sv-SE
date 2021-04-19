---
description: Följande information hjälper dig att skicka en länk till en äldre kundvärvningskampanj på en Android-enhet.
keywords: android;bibliotek;mobil;sdk
seo-description: Följande information hjälper dig att skicka en länk till en äldre kundvärvningskampanj på en Android-enhet.
seo-title: Testar tidigare förvärv
solution: Experience Cloud,Analytics
title: Testar tidigare förvärv
topic-fix: Developer and implementation
uuid: bb7ace96-68eb-4f43-b3cf-af80730b9cee
exl-id: 43e3b24e-e8bc-407c-b788-5ab85e459a90
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Testar tidigare förvärv {#testing-legacy-acquisition}

Följande information hjälper dig att skicka en länk till en äldre kundvärvningskampanj på en Android-enhet.

Om mobilappen ännu inte finns i Google Play kan du välja vilken mobilapp som helst som mål när du skapar kampanjlänken. Detta påverkar bara den app som förvärvsservern dirigerar om dig till, efter att du klickat på länken för förvärv, och inte möjligheten att testa länken för förvärv. Frågesträngsparametrar skickas till Google Play-butiken, som skickas till appen vid installationen som en del av en kampanjsändning. Testning av mobilappsförvärv kräver simulering av den här typen av sändning.

Appen måste vara nyligen installerad, eller ha data rensade i **[!UICONTROL Settings]**, varje gång ett test körs. Detta garanterar att de inledande livscykelvärdena som är kopplade till parametrarna för kampanjfrågesträngen skickas när appen startas första gången.

1. Generera en URL för en äldre anskaffningskampanj i gränssnittet för mobila tjänster.

   Mer information finns i [Använd äldre förvärvslänkar](/help/using/acquisition-main/c-marketing-links-builder/t-create-edit-adobe-links/c-use-legacy-acquisition-links/c-use-legacy-acquisition-links.md).
1. Anslut enheten till en dator, starta ADB Shell och starta programmet på enheten.
1. Skicka en sändning i följande format:

   ```
   am broadcast -a com.android.vending.INSTALL_REFERRER -n com.example.adobetesttapp/com.google.analytics.tracking.android.CampaignTrackingReceiver --es "referrer" "utm_source=testSource&utm_medium=testMedium&utm_term=testTerm&utm_content=testContent&utm_campaign=testCampaign&trackingcode=trackingvalue"
   ```

1. Utför följande steg:
   1. Ersätt `com.example.adobetesttapp.com` med programmets inverterade DNS-post.
   1. Uppdatera mottagarreferensen med kampanjspårningsmottagarplatsreferensen i din app.
   1. Ersätt värden som är associerade med `utm_source`, `utm_medium`, `utm_term`, `utm_content`, `utm_campaign` och så vidare, med lämpliga värden.

Om sändningen lyckas visas ett svar som liknar det nedan:

```
Broadcasting: Intent { act=com.android.vending.INSTALL_REFERRER cmp=com.example.analyticsecommtest/com.google.analytics.tracking.android.AnalyticsReceiver has extras) } Broadcast completed: result=0
```

Du ser även en bildbegäran som skickas till Adobe datainsamlingsservrar. Om SDK väntar på den fullständiga tidslängden för referenstimeout, som du angav i steg 1, med en bildbegäran som inte innehåller kampanjparametrar, misslyckades sändningen.
