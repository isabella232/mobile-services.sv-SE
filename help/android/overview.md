---
description: Med Android SDK 4.x för Experience Cloud Solutions kan ni mäta Android-applikationer, leverera riktat innehåll i appen och utnyttja och samla in målgruppsdata via målgruppshantering.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Android SDK 4.x för Experience Cloud Solutions
topic-fix: Developer and implementation
uuid: 56f1ff41-0365-41dd-bdde-245c823dff07
exl-id: c2454e94-a9af-42f3-ab45-14f68531faab
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# Android SDK 4.x för Experience Cloud{#android-sdk-x-for-experience-cloud-solutions}

Med Android SDK 4.x för Experience Cloud Solutions kan ni mäta Android-applikationer, leverera riktat innehåll i appen och utnyttja och samla in målgruppsdata via målgruppshantering.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
>Adobe Analytics Mobile Marketing Add-on SKU krävs för att Mobile Services ska kunna få tillgång till funktioner för mobilförvärv, djuplänkning, geolokalisering och mobilmeddelanden. Mer information får du om du kontaktar din Adobe CSM.

>[!IMPORTANT]
>
>Även om du kan konfigurera funktioner i användargränssnittet fungerar dessa funktioner inte förrän du hämtar den genererade konfigurationsfilen och lägger till den i SDK:n. Mer information om hur du hämtar och konfigurerar SDK:er finns i [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

SDK:erna har stöd för följande versioner av Android:

* Version 4.6.0 eller tidigare stöder Android 2.2 (API 8) - Android 5.1.1 (API 22)
* Version 4.6.1 eller senare stöder Android 2.3 (API 9) eller senare

Lite information att komma ihåg:

* I version 4.2 och senare skickas nu alla träffar med HTTP-POST.

   Detta påverkar inte de data som samlas in eller rapporteras, men du måste använda en paketanalyserare som har stöd för att inspektera data om POSTEN för att visa träffar.

* Om du uppgraderar från en tidigare version kan du läsa [Migreringshandbok för 4.x](/help/android/getting-started/migration-v3.md).

## Användardokumentation för Adobe Mobile {#section_7583FD5FDED143619048E9744A3F2D21}

Adobe Mobile-tjänster har ett gränssnitt som samlar funktioner för mobilmarknadsföring för mobilappar från hela Adobe Experience Cloud. Mer information om gränssnittet och användardokumentationen finns i [Adobe Mobile Services](/help/using/home.md).

## Versionsinformation {#section_F8181DC052D44DD2A99AB40A41F6792C}

Den senaste informationen om Experience Cloud finns på [Versionsinformation för Experience Cloud](/help/using/home.md).

## Använda Bloodhound

>[!IMPORTANT]
>
>Från och med **30 april 2017** Adobe Bloodhound är solnedgång. Från och med 1 maj 2017 finns inga ytterligare förbättringar och ingen ytterligare support för tekniker eller Adobe Expert Care.
