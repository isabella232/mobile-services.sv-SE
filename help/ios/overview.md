---
description: Med iOS SDK 4.x for Experience Cloud Solutions kan ni mäta Apple iPhone- och iPad-applikationer, leverera riktat innehåll i era appar samt utnyttja och samla in målgruppsdata via Audience Manager.
solution: Experience Cloud Services,Analytics
title: iOS SDK 4.x for Experience Cloud Solutions
topic-fix: Developer and implementation
uuid: 8b374cee-1432-460b-aac2-70623dd80a04
exl-id: d4dbddf7-c8be-4936-adfb-2f7aa07a0dd4
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# iOS SDK 4.x for Experience Cloud Solutions{#ios-sdk-x-for-experience-cloud-solutions}

Med iOS SDK 4.x for Experience Cloud Solutions kan ni mäta Apple iPhone- och iPad-applikationer, leverera riktat innehåll i era appar samt utnyttja och samla in målgruppsdata via Audience Manager.

>[!IMPORTANT]
>
>Från och med version 4.21.0 har iOS SDK minst den version av Xcode 12 som krävs. Om du använder Cocoapods för att hantera beroenden i din app kräver Adobe SDK version 1.10.0 eller senare av Cocopods.

Om du använder 4.21.0 eller senare läser du dokumentationen med följande ändringar i åtanke:

* När en binär biblioteksfil nämns bör XCFramwork-ersättaren användas i stället:
   * `AdobeMobileLibrary.a` > `AdobeMobile.xcframework`
   * `AdobeMobileLibrary_Extension.a` > `AdobeMobileExtension.xcframework`
   * `AdobeMobileLibrary_Watch.a` > `AdobeMobileWatch.xcframework`
   * `AdobeMobileLibrary_TV.a` > `AdobeMobileTV.xcframework`
* Om du lägger till Adobe XCFrameworks manuellt i ditt projekt måste du se till att de inte är inbäddade.

>[!IMPORTANT]
>
>Adobe Analytics Mobile Marketing Add-on SKU krävs för att Mobile Services ska kunna få tillgång till funktioner för mobilförvärv, djuplänkning, geolokalisering och mobilmeddelanden. Mer information får du om du kontaktar din Adobe CSM.

>[!IMPORTANT]
>
>iOS SDK 4.x för Experience Cloud Solutions har nu stöd för [iOS 13 och Xcode 11](https://developer.apple.com/ios/). Använd de senaste versionerna av iOS SDK 4.x för att säkerställa smidig kompatibilitet. Mer information om den senaste versionen finns i [versionsinformation](/help/ios/rel-notes.md).

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

Lite information att komma ihåg:

* iOS 8 eller senare stöds

   För iOS 11 eller senare **måste** har SDK version 4.13.8 eller senare.

* I version 4.2 av denna SDK och senare skickas nu alla träffar med HTTP-POST.

   Detta påverkar inte de data som samlas in eller rapporteras, men du måste använda en paketanalyserare som har stöd för att inspektera data om POSTEN för att visa träffar.

* Om du uppgraderar från en tidigare version (2.x eller 3.x), se [Migreringshandbok för 4.x](/help/ios/getting-started/migration-v3.md).

## Användardokumentation för Adobe Mobile {#section_7583FD5FDED143619048E9744A3F2D21}

Adobe Mobile-tjänster har ett nytt användargränssnitt som samlar funktioner för mobilmarknadsföring för mobilappar från hela Adobe Experience Cloud. Till att börja med erbjuder Mobile-tjänsten smidig integrering av funktioner för appanalys och målinriktning från lösningarna Adobe Analytics, Adobe Audience Manager och Adobe Target samt Adobe Experience Platform Identity Service.

Mer information om användargränssnittet för Mobile Services och användardokumentationen finns i [Adobe Mobile Services](/help/using/home.md).

## Använda Bloodhound

>[!IMPORTANT]
>
>Från och med **30 april 2017** Adobe Bloodhound har solnedgång. Från och med den 1 maj 2017 kommer inga ytterligare förbättringar att göras och ingen ytterligare support för tekniker eller Adobe Expert Care kommer att ges.
