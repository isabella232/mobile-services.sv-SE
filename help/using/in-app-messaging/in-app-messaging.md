---
description: Skapa, hantera och rapportera om meddelanden i programmet och push-meddelanden.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Meddelanden
topic-fix: Metrics
uuid: e32d3e35-2d09-4ddf-8919-75dc895abcb3
exl-id: e6d076fc-3176-4591-8388-314b936c58cd
source-git-commit: 7cfaa5f6d1318151e87698a45eb6006f7850aad4
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# Meddelanden {#messaging}

{#eol}

Du kan skapa, hantera och rapportera om meddelanden i programmet och push-meddelanden.

## Ny Adobe Experience Cloud SDK-version

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* För att komma igång, gå till [Starta](https://launch.adobe.com/).
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
> Om du använder Adobe Experience Platform Mobile SDK:er med Adobe Launch ska du **måste** installera också Adobe Analytics-tillägget för mobiltjänster om du vill använda Adobe-funktioner för mobiltjänster, som t.ex. förvärvslänkar. Mer information finns i [Adobe Analytics - Mobiltjänster](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services). Mer information om hur du använder push-meddelanden och meddelanden i appen med SDK:n för Experience Platform finns i [Konfigurera push-meddelanden](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-push-messaging) och [Konfigurera meddelanden i appen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-in-app-messaging).

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
* Meddelanden kan innehålla HTML eller en bild med hjälp av en online-URL.

   En säkerhetskopia eller alternativ avbildning från apppaketet kan också anges för meddelanden som utlöses offline.
* Aktiva och slutförda meddelanden ger rapporter om totalt antal visningar, klickfrekvens och så vidare.
* Det finns mallar för anpassade meddelanden, som gör att du enkelt kan skapa egna meddelanden i appen.

## Push-meddelanden {#section_90555A55BCE7427A90B1577E14BEF51B}

Push-meddelanden skickas till användare som har valt att ta emot meddelanden. Du kan rikta dessa push-meddelanden till användare i Analytics-segment eller anpassade segment. Du kan använda push-meddelanden för att återengagera passiva användare eller för att förmedla tidsspecifik och platsspecifik information eftersom meddelandena visas utanför appen.

Innan du kan konfigurera push-meddelanden, se [Krav för att aktivera push-meddelanden](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/prerequisites-push-messaging.md). När du har utfört dessa åtgärder måste du konfigurera push-meddelanden i appinställningarna. Mer information finns i [Konfigurera push-meddelanden](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/configure-push-messaging.md).
