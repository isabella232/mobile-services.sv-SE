---
description: Du kan använda iOS-tillägget för att samla in användningsdata från Apple Watch Apps (WatchOS 1), Today Widgets, Photo Editing widgets och andra iOS-tilläggsappar.
seo-description: Du kan använda iOS-tillägget för att samla in användningsdata från Apple Watch Apps (WatchOS 1), Today Widgets, Photo Editing widgets och andra iOS-tilläggsappar.
seo-title: Implementering av iOS-tillägg
solution: Marketing Cloud,Analytics
title: Implementering av iOS-tillägg
topic: Developer and implementation
uuid: 8afc03fe-403e-4643-ada1-30e403ede238
translation-type: tm+mt
source-git-commit: 718e336b9002fe3d5282697d4302d12a89297181

---


# Implementering av iOS-tillägg {#ios-extension-implementation}

Du kan använda iOS-tillägget för att samla in användningsdata från Apple Watch Apps (WatchOS 1), Today Widgets, Photo Editing widgets och andra iOS-tilläggsappar.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya SDK:er för Adobe Experience Platform Mobile kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Rekommendationer för iOS SDK i stället för wrapper {#section_97577331FD9E4FFBBE05D402C67AEE69}

>[!IMPORTANT]
>
>Vi rekommenderar att du använder iOS SDK i stället för wrapper.

Apple innehåller en uppsättning API:er som gör att bevakningsappen kan kommunicera med innehållsappen genom att skicka begäranden till den innehållande appen och ta emot svaren. Även om du kan skicka spårningsdata som en ordlista från bevakningsappen till behållarappen och anropa en spårningsmetod i behållarappen för att skicka data, har den här lösningen begränsningar.

I de flesta fall när en användare använder bevakningsappen körs innehållsappen i bakgrunden och det är bara säkert att anropa `TrackActionInBackground`, `TrackLocation`och `TrackBeacon`. Anrop av andra spårningsmetoder stör livscykeldata, så du bör bara använda dessa tre metoder för att skicka data från bevakad app.

Även om dessa tre spårningsmetoder uppfyller dina krav kan du använda iOS SDK eftersom SDK för bevakningsappen innehåller alla mobilfunktioner förutom meddelanden i appen.

## Komma igång {#section_D0BE4F780C9C4CD8ADD2AD4EE0BD5FD4}

>[!IMPORTANT]
>
>Se till att du har ett projekt med minst följande mål:
>
>* Ett mål som ska innehålla appen.
>* Ett mål för tillägget.
>



Om du arbetar med en WatchKit-app bör du ha ett tredje mål. Mer information om hur du utvecklar för Apple Watch finns i [Utveckla för Apple Watch](https://developer.apple.com/library/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/index.html#//apple_ref/doc/uid/TP40014969-CH8-SW1).

## Konfigurera behållarappen {#section_0BAB0842E4C04A62B5E03DFC4BA77851}

Utför följande steg i Xcode-projektet:

1. Dra mappen AdobeMobileLibrary till ditt projekt.
1. Kontrollera att `ADBMobileConfig.json` filen är medlem i det program som innehåller filen.
1. On the **[!UICONTROL Build Phases]** tab of your containing app&#39;s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

   * `AdobeMobileLibrary.a`
   * `libsqlite3.dylib`
   * `SystemConfiguration.framework`

1. Öppna fliken **[!UICONTROL Capabilities]** för det program som innehåller, aktivera **[!UICONTROL App Groups]** och lägg till en ny programgrupp (till exempel `group.com.adobe.testAp`).

1. I programdelegaten anger du programgruppen i `application:didFinishLaunchingWithOptions` innan du gör några interaktioner med Adobe Mobile-biblioteket:

   ```objective-c
   [ADBMobile 
         setAppGroup:@"group.com.adobe.testApp"];
   ```

1. Bekräfta att appen byggs utan oväntade fel.

## Konfigurera tillägget {#section_28C994B7892340AC8D1F07AF26FF3946}

1. Kontrollera att `ADBMobileConfig.json` filen är medlem i tilläggets mål.
1. On the **[!UICONTROL Build Phases]** tab of your extension’s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

   * `AdobeMobileLibrary_Extension.a`
   * `libsqlite3.dylib`
   * `SystemConfiguration.framework`

1. Öppna fliken **[!UICONTROL Capabilities]** för tilläggets mål, aktivera **[!UICONTROL App Groups]** och välj den programgrupp som du lade till i steg 4 i *Konfigurera appen* ovan.

1. I InterfaceController anger du appgruppen i `awakeWithContext:` innan du gör några andra interaktioner med Adobe Mobile-biblioteket:

   ```objective-c
   [ADBMobile 
         setAppGroup:@"group.com.adobe.testApp"];
   ```

1. Bekräfta att appen byggs utan oväntade fel.

## Ytterligare information {#section_21497E81231549CB9F164DEECFF5BA0D}

Här är lite information att komma ihåg:

* Ytterligare ett kontextdatavärde har lagts till för att ange om data kommer från din app eller ditt tillägg: `a.RunMode`

   * `a.RunMode = Application`

      Det här värdet innebär att träffen kom från innehållsappen.
   * `a.RunMode = Extension`

      Detta värde innebär att träffen kom från tillägget.

* Om du uppgraderar från en äldre version av SDK migrerar Adobe automatiskt alla användarstandardvärden och cachelagrade filer från behållarappens mapp till appgruppens delade mapp när det aktuella programmet startas.
* Om programmet som innehåller inte startas ignoreras träffar från tillägget.
* Versionsnumret och build-numret måste vara samma mellan det program som innehåller det och tilläggsprogrammet.
* Inget livscykelanrop aktiveras för iOS-tilläggsprogram.

