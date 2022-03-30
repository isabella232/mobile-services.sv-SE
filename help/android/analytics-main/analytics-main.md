---
description: Den här informationen hjälper dig att använda Android SDK med Adobe Analytics.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Analytics - översikt
topic-fix: Developer and implementation
uuid: cc9fa1d9-bc48-4d03-854a-f7b263580a91
exl-id: ed9f55e6-f3ab-4c1e-9a2f-1ee67a7b4c03
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Analytics - översikt {#analytics}

Informationen i det här avsnittet hjälper dig att använda Android SDK med Adobe Analytics.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

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

SDK genererar detta ID, som ibland även kallas spårnings-ID, när programmet inte är konfigurerat att använda ett MID. Värdet kvarstår mellan lanseringar och appuppgraderingar i `SharedPreferences`. Om användaren tar bort appen från sin enhet och sedan installerar om appen, eller om apputvecklaren rensar bort SharedPreferences, genereras en ny identifierare av SDK:n. Den här processen resulterar i en ny användare i Analytics-rapporter.

För användare i en app som introducerar stöd för identitetstjänst (MID) skickas befintliga AID-värden med Analytics-träffar, och Analytics-träffen innehåller ett AID och ett MID. För nya användare i en app med stöd för identitetstjänster innehåller Analytics-förfrågningar bara ett MID. Mer information om att identifiera besökare finns på [Unika besökare](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html) i Adobe Analytics-dokumentationen.
