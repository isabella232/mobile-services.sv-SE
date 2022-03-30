---
description: Från och med WatchOS 2 kan WatchKit-tilläggen köras på en Apple Watch-enhet. Program som körs i den här miljön kräver att WatchConnectivity-ramverket delar data med det program som innehåller iOS.
solution: Experience Cloud Services,Analytics
title: Apple Watch-implementering med WatchOS 2
topic-fix: Developer and implementation
uuid: 9498467e-db5e-411e-a00e-d19841f485de
exl-id: 9fc9b799-1081-42e4-acf3-569fdeb07aff
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# Apple Watch-implementering med WatchOS 2{#apple-watch-implementation-with-watchos}

Från och med WatchOS 2 kan WatchKit-tilläggen köras på en Apple Watch. Program som körs i den här miljön kräver `WatchConnectivity` för att dela data med den iOS-app de innehåller.

>[!TIP]
>
>Börja med `AdobeMobileLibrary` v4.6.0, `WatchConnectivity` stöds.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

## Komma igång {#section_70BC28BB69414F169196953D3D264BC1}

>[!IMPORTANT]
>
>Se till att du har ett projekt med minst följande mål:
>
>* The containing app
>* Appen WatchKit
>* Tillägget WatchKit
>


Mer information om hur du utvecklar WatchKit-appar finns i [Den bevakade apparkitekturen](https://developer.apple.com/library/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/DesigningaWatchKitApp.html#//apple_ref/doc/uid/TP40014969-CH3-SW1).

## Konfigurera behållarappen {#section_0A2A3995575B4E2ABD12E426BA06AEFF}

Utför följande steg i Xcode-projektet:

1. Dra `AdobeMobileLibrary` till ditt projekt.
1. Se till att `ADBMobileConfig.json` filen är medlem i det program som innehåller målfilen.
1. I **[!UICONTROL Build Phases]** för det program du arbetar med expanderar du **[!UICONTROL Link Binary with Libraries]** och lägga till följande bibliotek:

   * `AdobeMobileLibrary.a`
   * `libsqlite3.tbd`
   * `SystemConfiguration.framework`

1. I klassen som implementerar `UIApplicationDelegate` -protokoll, lägga till `WCSessionDelegate` -protokoll.

   ```objective-c
   #import <WatchConnectivity/WatchConnectivity.h> 
   @interface AppDelegate : UIResponder <UIApplicationDelegate, WCSessionDelegate>
   ```

1. I implementeringsfilen för programdelegatklassen importerar du `AdobeMobileLibrary`.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Innan du ringer `ADBMobile` bibliotek, i `application:didFinishLaunchingWithOptions:` av din appdelegat, konfigurera `WCSession`.

   ```objective-c
   // check for session availability 
   if ([WCSession isSupported]) { 
       WCSession *session = [WCSession defaultSession]; 
       session.delegate = self; 
       [session activateSession]; 
   }
   ```

1. Implementera `session:didReceiveMessage:` och `session:didReceiveUserInfo:` metoder.

   `syncSettings:` anropas i `ADBMobile` bibliotek, som returnerar en bool som anger om ordlistan var avsedd för konsumtion av `ADBMobile` bibliotek. Om den returnerar `No`, meddelandet startades inte från Adobe SDK.

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

1. Se till att `ADBMobileConfig.json` filen ingår i målet för WatchKit-tillägget.
1. I **[!UICONTROL Build Phases]** för WatchKit-tilläggets mål, expandera **[!UICONTROL Link Binary with Libraries]** och lägga till följande bibliotek:

   * `AdobeMobileLibrary_Watch.a`
   * `libsqlite3.tbd`

1. I klassen som implementerar `WKExtensionDelegate` protokoll, importera `WatchConnectivity` och lägg till `WCSessionDelegate` -protokoll.

   ```objective-c
   #import <WatchConnectivity/WatchConnectivity.h> 
   @interface ExtensionDelegate : NSObject <WKExtensionDelegate, WCSessionDelegate>
   ```

1. Importera `AdobeMobileLibrary`.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. I `applicationDidFinishLaunching` för din tilläggsdelegat, konfigurera `WCSession` innan du ringer `ADBMobile` bibliotek.

   ```objective-c
   // check for session availability 
   if ([WCSession isSupported]) { 
       WCSession *session = [WCSession defaultSession]; 
       session.delegate = self; 
       [session activateSession]; 
   }
   ```

1. I `applicationDidFinishLaunching` initiera den bevakade appen för SDK:n.

   ```objective-c
   [ADBMobile initializeWatch];
   ```

1. Implementera `session:didReceiveMessage:` och `session:didReceiveUserInfo:` metoder.

   `syncSettings:` anropas i `ADBMobile` bibliotek, som returnerar en bool som anger om ordlistan var avsedd för konsumtion av `ADBMobile` bibliotek. Om den returnerar `NO`, meddelandet startades inte från Adobe SDK.

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

* För WatchKit-appar `a.RunMode` ställs in på `Extension`.
* Eftersom WatchKit-appar körs på bevakningen kommer apparna att rapportera sina namn korrekt i `a.AppID`.
* Inget livscykelanrop aktiveras för WatchOS2-appar.
