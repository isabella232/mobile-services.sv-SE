---
description: Med iOS SDK 4.x för Experience Cloud Solutions kan ni mäta iPhone- och iPad-applikationer från Apple, leverera riktat innehåll inifrån apparna samt utnyttja och samla in målgruppsdata via Audience Manager.
seo-description: Med iOS SDK 4.x för Experience Cloud Solutions kan ni mäta iPhone- och iPad-applikationer från Apple, leverera riktat innehåll inifrån apparna samt utnyttja och samla in målgruppsdata via Audience Manager.
seo-title: iOS SDK 4.x för Experience Cloud Solutions
solution: Experience Cloud,Analytics
title: iOS SDK 4.x för Experience Cloud Solutions
topic: Developer and implementation
uuid: 8b374cee-1432-460b-aac2-70623dd80a04
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# iOS SDK 4.x för Experience Cloud Solutions{#ios-sdk-x-for-experience-cloud-solutions}

Med iOS SDK 4.x för Experience Cloud Solutions kan ni mäta iPhone- och iPad-applikationer från Apple, leverera riktat innehåll inifrån apparna samt utnyttja och samla in målgruppsdata via Audience Manager.

>[!IMPORTANT]
>
>Adobe Analytics Mobile Marketing Add-on SKU krävs för att aktivera Mobile Services-åtkomst till mobilförvärv, djuplänkning, geolokalisering och funktioner för mobilmeddelanden. Mer information får du om du kontaktar din Adobe CSM.

>[!IMPORTANT]
>
>iOS SDK 4.x för Experience Cloud Solutions har nu stöd för [iOS 13 och Xcode 11](https://developer.apple.com/ios/). Använd de senaste versionerna av iOS SDK:erna för 4.x för att säkerställa sömlös kompatibilitet. Mer information om den senaste versionen finns i [versionsinformationen](/help/ios/rel-notes.md).

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

Lite information att komma ihåg:

* iOS 8 eller senare stöds

   För iOS 11 eller senare **måste** du ha SDK version 4.13.8 eller senare.

* I version 4.2 av denna SDK och senare skickas nu alla träffar med HTTP-POST.

   Detta påverkar inte de data som samlas in eller rapporteras, men du måste använda en paketanalyserare som har stöd för att inspektera data i POSTEN för att visa träffar.

* Om du uppgraderar från en tidigare version (2.x eller 3.x), se [4.x-migreringshandboken](/help/ios/getting-started/migration-v3.md).

## Användardokumentation för Adobe Mobile {#section_7583FD5FDED143619048E9744A3F2D21}

Adobe Mobile-tjänster har ett nytt användargränssnitt som samlar funktioner för mobilmarknadsföring för mobilappar från hela Adobe Experience Cloud. Från början erbjuder mobiltjänsten smidig integrering av funktioner för appanalys och målinriktning från Adobe Analytics, Adobe Audience Manager och Adobe Target samt Adobe Experience Platform Identity Service.

Mer information om gränssnittet för mobiltjänster och användardokumentationen finns i [Adobe Mobile Services](/help/using/home.md).

## Använda Bloodhound

>[!IMPORTANT]
>
>Från och med **den 30 april 2017** har Adobe Bloodhound lossnat. Från och med den 1 maj 2017 kommer inga ytterligare förbättringar att göras och ingen ytterligare support för tekniker eller Adobe Expert Care kommer att ges.
