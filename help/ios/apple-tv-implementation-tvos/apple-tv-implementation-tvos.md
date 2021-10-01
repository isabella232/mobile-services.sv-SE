---
description: Den här informationen hjälper dig att implementera Apple TV med tvOS.
solution: Experience Cloud,Analytics
title: Apple TV-implementering med tvOS
topic-fix: Developer and implementation
uuid: d1571ea2-a5de-4b96-a527-72abbf51fab8
exl-id: 35b7f02d-ae48-4c6f-9a3a-6d106a1026ad
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 1%

---

# Apple TV-implementering med tvOS {#apple-tv-implementation-with-tvos}

Den här informationen hjälper dig att implementera Apple TV med tvOS.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDK](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Översikt

Med Apple TV kan du nu skapa program som kan köras i den inbyggda tvOS-miljön. Du kan skapa ett systemspecifikt program med flera ramverk i iOS, eller så kan du skapa programmet med hjälp av XML-mallar och JavaScript.

>[!TIP]
>
>Stöd för tvOS finns från och med version 4.7.0 i `AdobeMobileLibrary`.

## Komma igång {#section_CAB40A5B5FC745068C8A5DF8F9AB6199}

>[!TIP]
>
>Vi antar att ditt projekt har ett mål som är en Apple TV-app som har tvOS som mål. Mer information finns i [tvOS](https://developer.apple.com/tvos/documentation/).

## Konfigurera en intern app för tvOS {#section_5095F19B3C4545F68E8C1E37A7E303AE}

Utför följande steg i Xcode-projektet:

1. Dra mappen AdobeMobileLibrary till ditt projekt.
1. Kontrollera att `ADBMobileConfig.json`-filen är medlem i ditt mål.
1. Expandera **[!UICONTROL Link Binary with Libraries]**-avsnittet på fliken **[!UICONTROL Build Phases]** i din tvOS-app och lägg till följande bibliotek:

   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

Mer information finns i iOS-dokumentationen om [iOS](https://developer.apple.com/ios/resources/).

## Konfigurera en TVML/TVJS-app för tvOS {#section_AB2EC8C326654F3387658EBBD990BB12}

1. Dra mappen `AdobeMobileLibrary` till ditt projekt.
1. Kontrollera att `ADBMobileConfig.json`-filen är medlem i ditt mål.
1. Expandera **[!UICONTROL Link Binary with Libraries]**-avsnittet på fliken **[!UICONTROL Build Phases]** i din tvOS-app och lägg till följande bibliotek:

   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

1. Importera SDK:n i implementeringsfilen för klassen `TVApplicationControllerDelegate`.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. I metoden `application:didFinishLaunchWithOptions:` för klassen `TVApplicationControllerDelegate` skickar du `TVApplicationController`-objektet till SDK med metoden `installTVMLHooks:`.

   Adobe SDK behöver tillgång till din apps `TVApplicationController` för att kunna registrera sig i JSContext för din app. I det här steget kan du anropa de inbyggda metoderna i Adobe SDK från dina JavaScript-filer.

   ```objective-c
   [ADBMobile installTVMLHooks:appController];
   ```

1. I dina JavaScript-filer använder du `ADBMobile`-objektet för att komma åt de inbyggda metoderna i Adobe SDK.

   En fullständig lista över tillgängliga metoder finns i [TVJS-metoder](/help/ios/apple-tv-implementation-tvos/tvjs-methods.md).
