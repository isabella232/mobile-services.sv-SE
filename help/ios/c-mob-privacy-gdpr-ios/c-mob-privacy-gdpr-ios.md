---
description: Experience Cloud SDK för mobiler tillhandahåller GDPR-klara API:er för styrenheter som gör det möjligt för användare att hämta lokalt lagrade identiteter och ange alternativstatusflaggor för datainsamling och överföring.
seo-description: Experience Cloud SDK för mobiler tillhandahåller GDPR-klara API:er för styrenheter som gör det möjligt för användare att hämta lokalt lagrade identiteter och ange alternativstatusflaggor för datainsamling och överföring.
seo-title: Sekretess och allmänna dataskyddsföreskrifter
title: Sekretess och allmänna dataskyddsföreskrifter
uuid: 69bb82de-1993-440c-a1b0-8d37919b48b6
translation-type: tm+mt
source-git-commit: b690ec677cf5aedfb2673b707f82716af1851124
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---


# Sekretess och allmänna dataskyddsföreskrifter {#privacy-and-general-data-protection-regulation}

Experience Cloud SDK för mobiler tillhandahåller GDPR-klara API:er för styrenheter som gör det möjligt för användare att hämta lokalt lagrade identiteter och ange alternativstatusflaggor för datainsamling och överföring.

>[!IMPORTANT]
>
>GDPR stöds **endast** i Mobile SDK version 4.16.0 eller senare.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Översikt

När Adobe tillhandahåller programvara och tjänster till ett företag fungerar Adobe som personuppgiftsbiträde för alla personuppgifter som det behandlar och lagrar som en del av tillhandahållandet av dessa tjänster. Som personuppgiftsbiträde behandlar Adobe personuppgifter i enlighet med ditt företags tillstånd och instruktioner (till exempel enligt vad som anges i ditt avtal med Adobe).

Som personuppgiftsansvariga kan du använda Adobe Mobile Services SDK:er för att stödja GDPR-hämtnings- och borttagningsbegäranden från dina mobilappar.

För Adobe Mobile SDK-delar av dina mobilappar kan du använda följande inställningar och metoder:

* Använd `getAllIdentifiersAsync` metoden om du vill hämta data från SDK:n och skicka dessa data till servrarna.

   Mer information finns i [Hämta lagrade identifierare](/help/ios/c-mob-privacy-gdpr-ios/c-mob-gdpr-ret-stored-ids-ios.md).

* Använd följande inställningar för att ange din valstatus och hjälpa dig med en begäran om att ta bort GDPR-data:

   * `privacyDefault`
   * `setPrivacyStatus`

   Mer information finns i [Ange användarens alternativstatus](/help/ios/c-mob-privacy-gdpr-ios/privacy.md).

## Ytterligare information {#section_7C7124C50D85469C8C8714533FB1A37D}

* Mer information om GDPR finns i [GDPR och Ditt företag](https://www.adobe.com/se/privacy/general-data-protection-regulation.html).
* Om du vill se dokumentationen för GDPR API går du till API:t för [allmänna dataskyddsregler](https://adobe.io/apis/cloudplatform/gdpr.html).

