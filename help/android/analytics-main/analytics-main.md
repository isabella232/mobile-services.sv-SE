---
description: Den här informationen hjälper dig att använda Android SDK med Adobe Analytics.
keywords: android;library;mobile;sdk
seo-description: Den här informationen hjälper dig att använda Android SDK med Adobe Analytics.
seo-title: Analytics - översikt
solution: Marketing Cloud,Analytics
title: Analytics - översikt
topic: Developer and implementation
uuid: cc9fa1d9-bc48-4d03-854a-f7b263580a91
translation-type: tm+mt
source-git-commit: b690ec677cf5aedfb2673b707f82716af1851124

---


# Analytics - översikt {#analytics}

Informationen i det här avsnittet hjälper dig att använda Android SDK med Adobe Analytics.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya SDK:er för Adobe Experience Platform Mobile kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Genererar spårningsidentifierare för analyser

I SDK:er används identifierare för att spåra användare, och här är hierarkin med identifierare:

1. Anpassad besökaridentifierare (VID)
2. Analysspårnings-ID (AID)
3. Experience Cloud Identifier (MID)

>[!TIP]
>
>Den korrekta akronymen för Experience Cloud Identifier är ECID. Även om SDK fortfarande använder MID är det det gamla namnet.

SDK genererar detta ID, som ibland även kallas spårnings-ID, när programmet inte är konfigurerat att använda ett MID. Värdet kvarstår mellan lanseringar och appuppgraderingar i `SharedPreferences`. Om användaren tar bort appen från sin enhet och sedan installerar om appen, eller om apputvecklaren rensar bort SharedPreferences, genereras en ny identifierare av SDK:n. Den här processen resulterar i en ny användare i Analytics-rapporter.

För användare i en app som introducerar stöd för identitetstjänst (MID) skickas befintliga AID-värden med Analytics-träffar, och Analytics-träffen innehåller ett AID och ett MID. För nya användare i en app med stöd för identitetstjänster innehåller Analytics-förfrågningar bara ett MID. Mer information om att identifiera besökare finns i [Identifiera besökare](https://docs.adobe.com/content/help/en/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-visid.html).