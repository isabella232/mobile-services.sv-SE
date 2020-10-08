---
description: Den här informationen hjälper dig att använda iOS SDK med Adobe Analytics.
seo-description: Den här informationen hjälper dig att använda iOS SDK med Adobe Analytics.
seo-title: Analytics - översikt
solution: Experience Cloud,Analytics
title: Analytics - översikt
topic: Developer and implementation
uuid: 8c7fb76a-be0b-4465-8151-ece7bad11b55
translation-type: tm+mt
source-git-commit: bc11c1e7a4a11657ee89c40ddcbd37377ce50bb5
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Analytics - översikt {#analytics}

Informationen i det här avsnittet hjälper dig att använda iOS SDK med Adobe Analytics.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Genererar spårningsidentifierare för analyser

I SDK:er används identifierare för att spåra användare, och här är hierarkin med identifierare:

1. Anpassad besökaridentifierare (VID)
1. Analysspårnings-ID (AID)
1. Experience Cloud-ID (MID)

>[!TIP]
>
>Den korrekta akronymen för Experience Cloud-identifieraren är ECID. Även om SDK fortfarande använder MID är det det gamla namnet.

SDK genererar detta ID, som ibland även kallas spårnings-ID, när programmet inte är konfigurerat att använda ett MID. Värdet kvarstår mellan lanseringar och appuppgraderingar i `NSUserDefaults`. Om användaren tar bort appen från sin enhet och sedan installerar om appen, eller om apputvecklaren rensar bort, genereras en ny identifierare av SDK:n. `NSUserDefaults` Den här processen resulterar i en ny användare i Analytics-rapporter.

För användare i en app som introducerar stöd för identitetstjänst (MID) skickas befintliga AID-värden med Analytics-träffar, och Analytics-träffen innehåller ett AID och ett MID. För nya användare i en app med stöd för identitetstjänster innehåller Analytics-förfrågningar bara ett MID. Mer information om att identifiera besökare finns i [Identifiera besökare](https://docs.adobe.com/content/help/en/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-visid.html).
