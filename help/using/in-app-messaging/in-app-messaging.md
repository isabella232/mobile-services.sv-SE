---
description: Skapa, hantera och rapportera om meddelanden i programmet och push-meddelanden.
keywords: mobile
seo-description: Skapa, hantera och rapportera om meddelanden i programmet och push-meddelanden.
seo-title: Meddelanden
solution: Marketing Cloud,Analytics
title: Meddelanden
topic: Metrics
uuid: e32d3e35-2d09-4ddf-8919-75dc895abcb3
translation-type: tm+mt
source-git-commit: 3b744229b3fc288363be74c3c4adcd71ecc4fad4

---


# Meddelanden {#messaging}

Du kan skapa, hantera och rapportera om meddelanden i programmet och push-meddelanden.

## Ny Adobe Experience Cloud SDK-version

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya SDK:er för Adobe Experience Platform Mobile kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till [Launch](https://launch.adobe.com/)för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
> Om du använder Adobe Experience Platform Mobile SDK:er med Adobe Launch **måste** du också installera Adobe Analytics-tillägget för mobila tjänster för att kunna använda Adobe Mobile Services-funktioner som förvärvslänkar. Mer information finns i [Adobe Analytics - Mobiltjänster](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services). Mer information om hur du använder push-meddelanden och meddelanden i appen med Experience Platform SDK:er finns i [Konfigurera push-meddelanden](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-push-messaging) och [Konfigurera meddelanden](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-in-app-messaging)i appen.

## Meddelanden i appen {#section_8984F4568BC24D32A87429FFCB5184A6}

Meddelanden i appen levereras till användarna i realtid baserat på deras åtgärder och egenskaper. Meddelandena utlöses från analysdata som redan spårats av SDK:n.

Följande meddelandetyper stöds:

* Anpassat och tema
* Helskärm
* Inbyggda aviseringar
* Lokala meddelanden

Här finns ytterligare information som hjälper dig att förstå hur meddelanden i appen fungerar:

* Meddelanden i appen kräver SDK version 4.2 eller senare.
* Du måste ange vem som har administratörsbehörighet för mobilappar.

   Dessa rättigheter ger åtkomst till länkar för förvärv och meddelanden i appen. Mer information finns i [Roller och behörigheter](/help/using/gs/c-mob-roles-and-permissions.md).
* När ett meddelande har godkänts publiceras det automatiskt till programmet.
* SDK visar meddelandet för användarna när meddelandeparametrarna, som traits, trigger och schedule, uppfylls.
* Meddelanden kan innehålla egen HTML-kod eller en bild med en online-URL.

   En säkerhetskopia eller alternativ avbildning från apppaketet kan också anges för meddelanden som utlöses offline.
* Aktiva och slutförda meddelanden ger rapporter om totalt antal visningar, klickfrekvens och så vidare.
* Det finns mallar för anpassade meddelanden, som gör att du enkelt kan skapa egna meddelanden i appen.

## Push-meddelanden {#section_90555A55BCE7427A90B1577E14BEF51B}

Push-meddelanden skickas till användare som har valt att ta emot meddelanden. Du kan rikta dessa push-meddelanden till användare i Analytics-segment eller anpassade segment. Du kan använda push-meddelanden för att återengagera passiva användare eller för att förmedla tidsspecifik och platsspecifik information eftersom meddelandena visas utanför appen.

Innan du kan konfigurera push-meddelanden läser du [Krav för att aktivera push-meddelanden](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/prerequisites-push-messaging.md). När du har utfört dessa åtgärder måste du konfigurera push-meddelanden i appinställningarna. Mer information finns i [Konfigurera push-meddelanden](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/configure-push-messaging.md).
