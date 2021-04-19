---
description: Från och med WatchOS 2 körs WatchKit-tilläggen på en Apple Watch-enhet. Program som körs i den här miljön kräver WatchConnectivity-ramverket för att dela data med den iOS-app som de innehåller.
seo-description: Från och med WatchOS 2 körs WatchKit-tilläggen på en Apple Watch-enhet. Program som körs i den här miljön kräver WatchConnectivity-ramverket för att dela data med den iOS-app som de innehåller.
seo-title: Apple Watch-implementering med WatchOS 2
solution: Experience Cloud,Analytics
title: Apple Watch-implementering med WatchOS 2
topic-fix: Developer and implementation
uuid: 9498467e-db5e-411e-a00e-d19841f485de
exl-id: 9fc9b799-1081-42e4-acf3-569fdeb07aff
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Apple Watch-implementering med WatchOS 2{#apple-watch-implementation-with-watchos}

Från och med WatchOS 2 kan WatchKit-tilläggen köras på en Apple Watch. Program som körs i den här miljön kräver `WatchConnectivity`-ramverket för att dela data med den iOS-app som innehåller dem.

>[!TIP]
>
>Från och med `AdobeMobileLibrary` v4.6.0 stöds `WatchConnectivity`.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDK](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Komma igång {#section_70BC28BB69414F169196953D3D264BC1}

>[!IMPORTANT]
>
>Se till att du har ett projekt med minst följande mål:
>
>* The containing app
>* Appen WatchKit
>* Tillägget WatchKit

>



Mer information om hur du utvecklar WatchKit-appar finns i [The Watch App Architecture](https://developer.apple.com/library/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/DesigningaWatchKitApp.html#//apple_ref/doc/uid/TP40014969-CH3-SW1).

## Konfigurera den innehållande appen {#section_0A2A3995575B4E2ABD12E426BA06AEFF}

Utför följande steg i Xcode-projektet:

1. Dra mappen `AdobeMobileLibrary` till ditt projekt.
1. Kontrollera att `ADBMobileConfig.json`-filen är medlem i det program som innehåller filen.
1. Expandera **[!UICONTROL Link Binary with Libraries]**-avsnittet på fliken **[!UICONTROL Build Phases]** för det program som innehåller och lägg till följande bibliotek:

   * `AdobeMobileLibrary.a`
   * `libsqlite3.tbd`
   * `SystemConfiguration.framework`

1. Lägg till protokollet `WCSessionDelegate` i den klass som implementerar protokollet `UIApplicationDelegate`.

   ```objective-c
   #import <WatchConnectivity/WatchConnectivity.h> 
   @interface AppDelegate : UIResponder <UIApplicationDelegate, WCSessionDelegate>
   ```

1. Importera `AdobeMobileLibrary`-filen i implementeringsfilen för din programdelegatklass.

   ```objective-c
   #import “ADBMobile.h”
   ```

1. Konfigurera din `WCSession` innan du gör ett anrop till `ADBMobile`-biblioteket i `application:didFinishLaunchingWithOptions:` för din appdelegat.

   ```objective-c
   // check for session availability 
   if ([WCSession isSupported]) { 
       WCSession *session = [WCSession defaultSession]; 
       session.delegate = self; 
       [session activateSession]; 
   }
   ```

1. Implementera metoderna `session:didReceiveMessage:` och `session:didReceiveUserInfo:` i din appdelegat.

   `syncSettings:` anropas i  `ADBMobile` biblioteket, vilket returnerar en bool som anger om ordlistan var avsedd att användas av  `ADBMobile` biblioteket. Om `No` returneras initierades inte meddelandet från Adobe SDK.

   ```objective-c
   - (void) session:(WCSession *)session didReceiveMessage:(NSDictionary<NSString *,id> *)message { 
       // pass message to ADBMobile 
       if (![ADBMobile syncSettings:message]) { 
           // handle your own custom messages 
       } 
   } 
   - (void) session:(WCSession *)session didReceiveUserInfo:(NSDictionary<NSString *,id> *)userInfo { 
       // pass userInfo to ADBMobile 
       if (![ADBMobile syncSettings:userInfo]) { 
           // handle your own custom messages 
       } 
   } 
   ```

## Konfigurera WatchKit-tillägget {#section_5ADE31741E514330A381F2E3CFD4A814}

1. Kontrollera att `ADBMobileConfig.json`-filen är medlem i WatchKit-tilläggets mål.
1. Expandera avsnittet **[!UICONTROL Link Binary with Libraries]** på fliken **[!UICONTROL Build Phases]** i WatchKit-tilläggets mål och lägg till följande bibliotek:

   * `AdobeMobileLibrary_Watch.a`
   * `libsqlite3.tbd`

1. I den klass som implementerar protokollet `WKExtensionDelegate` importerar du `WatchConnectivity` och lägger till protokollet `WCSessionDelegate`.

   ```objective-c
   #import <WatchConnectivity/WatchConnectivity.h> 
   @interface ExtensionDelegate : NSObject <WKExtensionDelegate, WCSessionDelegate>
   ```

1. Importera `AdobeMobileLibrary`-filen i implementeringsfilen för din tilläggsklass.

   ```objective-c
   #import “ADBMobile.h”
   ```

1. Konfigurera din `WCSession` innan du anropar `ADBMobile`-biblioteket i `applicationDidFinishLaunching` för din tilläggsdelegat.

   ```objective-c
   // check for session availability 
   if ([WCSession isSupported]) { 
       WCSession *session = [WCSession defaultSession]; 
       session.delegate = self; 
       [session activateSession]; 
   }
   ```

1. Initiera den bevakade appen för SDK i `applicationDidFinishLaunching` för din tilläggsdelegat.

   ```objective-c
   [ADBMobile initializeWatch];
   ```

1. Implementera metoderna `session:didReceiveMessage:` och `session:didReceiveUserInfo:` i din tilläggsdelegat.

   `syncSettings:` anropas i  `ADBMobile` biblioteket, vilket returnerar en bool som anger om ordlistan var avsedd att användas av  `ADBMobile` biblioteket. Om `NO` returneras initierades inte meddelandet från Adobe SDK.

   ```objective-c
   - (void) session:(WCSession *)session didReceiveMessage:(NSDictionary<NSString *,id> *)message { 
       // pass message to ADBMobile 
       if (![ADBMobile syncSettings:message]) { 
           // handle your own custom messages 
       } 
   } 
   - (void) session:(WCSession *)session didReceiveUserInfo:(NSDictionary<NSString *,id> *)userInfo { 
       // pass userInfo to ADBMobile 
       if (![ADBMobile syncSettings:userInfo]) { 
           // handle your own custom messages 
       } 
   } 
   ```

## Ytterligare information {#section_7BCDB5CF0D424DCA97883753D1881233}

Kom ihåg följande information:

* För WatchKit-appar ställs `a.RunMode` in på `Extension`.
* Eftersom WatchKit-appar körs på bevakningen kommer apparna att rapportera sina namn korrekt i `a.AppID`.
* Inget livscykelanrop aktiveras för WatchOS2-appar.
