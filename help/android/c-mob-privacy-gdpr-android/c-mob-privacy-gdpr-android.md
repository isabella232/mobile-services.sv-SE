---
description: Experience Cloud SDK för mobiler tillhandahåller GDPR-klara API:er för styrenheter som gör det möjligt för användare att hämta lokalt lagrade identiteter och ange alternativstatusflaggor för datainsamling och överföring.
seo-description: Experience Cloud SDK för mobiler tillhandahåller GDPR-klara API:er för styrenheter som gör det möjligt för användare att hämta lokalt lagrade identiteter och ange alternativstatusflaggor för datainsamling och överföring.
seo-title: Integritet och allmänna dataskyddsförordningen - översikt
title: Integritet och allmänna dataskyddsförordningen - översikt
uuid: 56d6f155-efec-4b3f-a972-a63155729167
translation-type: tm+mt
source-git-commit: 718e336b9002fe3d5282697d4302d12a89297181
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---


# Integritet och allmänna dataskyddsförordningen - översikt {#privacy-and-general-data-protection-regulation}

Experience Cloud SDK för mobiler tillhandahåller GDPR-klara API:er för styrenheter som gör det möjligt för användare att hämta lokalt lagrade identiteter och ange alternativstatusflaggor för datainsamling och överföring.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Översikt

>[!IMPORTANT]
>
>GDPR stöds **endast** i Mobile SDK version 4.16.0 eller senare.

När Adobe tillhandahåller programvara och tjänster till ett företag fungerar Adobe som personuppgiftsbiträde för alla personuppgifter som det behandlar och lagrar som en del av tillhandahållandet av dessa tjänster. Som personuppgiftsbiträde behandlar Adobe personuppgifter i enlighet med ditt företags tillstånd och instruktioner (till exempel enligt vad som anges i ditt avtal med Adobe).

Som personuppgiftsansvariga kan du använda Adobe Mobile Services SDK:er för att stödja GDPR-hämtnings- och borttagningsbegäranden från dina mobilappar.

För Adobe Mobile SDK-delar av dina mobilappar kan du använda följande inställningar och metoder:

* Använd `getAllIdentifiersAsync` metoden om du vill hämta data från SDK:n och skicka dessa data till servrarna.

   Mer information finns i [Hämta lagrade identifierare](/help/android/c-mob-privacy-gdpr-android/c-mob-gdpr-ret-stored-ids-android.md).

* Använd följande inställningar för att ange din valstatus och hjälpa dig med en begäran om att ta bort GDPR-data:

   * `privacyDefault`
   * `setPrivacyStatus`
   Mer information finns i [Ange användarens alternativstatus](/help/android/c-mob-privacy-gdpr-android/privacy.md).