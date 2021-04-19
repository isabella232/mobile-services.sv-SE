---
description: Med Adobe Mobile och Adobe Mobile SDK kan du skicka push-meddelanden till dina användare. Med SDK kan du även enkelt rapportera användare som har öppnat din app genom att klicka dig igenom ett push-meddelande.
seo-description: Med Adobe Mobile och Adobe Mobile SDK kan du skicka push-meddelanden till dina användare. Med SDK kan du även enkelt rapportera användare som har öppnat din app genom att klicka dig igenom ett push-meddelande.
seo-title: Push-meddelanden
solution: Experience Cloud,Analytics
title: Push-meddelanden
topic-fix: Developer and implementation
uuid: 2e2d8175-d7d0-4b6b-a14e-d419da1f9615
exl-id: 89796668-e0e7-45d2-8391-3c26a7ac8496
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Push-meddelanden {#push-messaging}

Med Adobe Mobile och Adobe Mobile SDK kan du skicka push-meddelanden till dina användare. Med SDK kan du även enkelt rapportera användare som har öppnat din app genom att klicka dig igenom ett push-meddelande.

>[!IMPORTANT]
>
>Informationen i det här avsnittet är ett förslag till en eventuell implementering. Vi rekommenderar att du läser Apples iOS-dokumentation för att avgöra vilken implementering som är bäst för din app. Implementeringen bör avgöras av de ramverk som du använder och vilka versioner av iOS som appen ska ha som mål.

Om du vill använda push-meddelanden måste du **ha SDK version 4.6 eller senare.**

>[!IMPORTANT]
>
>Ange inte Experience Cloud-ID:t i appen manuellt. Detta skapar en ny unik användare som inte får push-meddelanden på grund av sin anmälningsstatus. Anta till exempel att en användare som har anmält sig till att ta emot push-meddelanden loggar in i din app. När du har loggat in skapas en ny unik användare som inte har valt att ta emot push-meddelanden om du manuellt anger ID:t i appen. Den nya användaren kommer inte att få dina push-meddelanden.

## Förutsättningar {#section_06655ABE973743DC965897B229A2118D}

* Lägg till biblioteket i ditt projekt och implementera livscykelvärden.

   Mer information finns i [Livscykelmått](/help/ios/metrics.md).


* SDK måste vara aktiverat för ID-tjänsten.
Mer information finns i [Konfigurera alternativ för tjänsten SDK ID](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-visitor.md).

>[!IMPORTANT]
>
>Det går inte att flytta appen till en ny rapportserie. Om du migrerar till en ny rapportserie kan din push-konfiguration brytas och meddelanden kanske inte skickas.

## Aktivera push-meddelanden {#section_CBD63C5B11FE4424BC2BF552C23F2BD9}

1. Kontrollera att filen `ADBMobileConfig.json` innehåller de inställningar som krävs för push-meddelanden.

   `"marketingCloud"`-objektet måste ha egenskapen `"org"` konfigurerad för push-meddelanden.

   ```objective-c
   "marketingCloud": { 
       "org": "3CE342C92046435B0A490D4C@AdobeOrg" 
   }
   ```

1. Importera biblioteket i din `AppDelegate`.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Om du vill ta reda på vilka inställningar ditt program behöver be om behörighet för går du igenom [Konfigurera stöd för fjärrmeddelanden](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1).

   Här är ett exempel på en möjlig implementering som kräver tillstånd att använda larm, badges, ljud och fjärrmeddelanden:

   ```objective-c
   // iOS 10 and newer 
   if (NSClassFromString(@"UNUserNotificationCenter")) { 
       UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];   
       [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert + UNAuthorizationOptionSound + UNAuthorizationOptionBadge) 
           completionHandler:^(BOOL granted, NSError * _Nullable error) { 
           if (granted) { NSLog(@"authorization given"); } 
           else { NSLog(@"authorization rejected"); } 
           if (error) { NSLog(@"error during authorization: %@", error.localizedDescription); } 
       }]; 
       // have to ask for permission for remote notifications separately  
       [application registerForRemoteNotifications]; 
       // make this class the delegate for user notification handling  
       center.delegate = self; 
   } 
   // iOS 8.0 to iOS 9.3.5 
   else if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) { 
   #pragma GCC diagnostic push 
   #pragma GCC diagnostic ignored "-Wdeprecated-declarations" 
       UIUserNotificationTypetypes = UIUserNotificationTypeAlert | UIUserNotificationTypeBadge| UIUserNotificationTypeSound; 
       UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:types categories:nil]; 
       [application registerUserNotificationSettings:settings]; 
       // have to ask for permission for remote notifications separately  
       [application registerForRemoteNotifications]; 
   } 
   // older than iOS 8.0  
   else { 
       [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge| UIRemoteNotificationTypeSound];  
   #pragma GCC diagnostic pop 
   }
   ```

1. Push-token måste skickas till SDK med metoden `setPushIdentifier:` i ADBMoble-klassen.

   ```objective-c
   - (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken { 
       ... 
       [ADBMobile setPushIdentifier:deviceToken]; 
       ... 
   }
   ```

1. Gå till [UserNotifications](https://developer.apple.com/documentation/usernotifications) om du vill ta reda på vilken implementering som är korrekt för din miljö.

   Det här steget hjälper dig att aktivera push-rapportering genom att skicka `userInfo`-ordlistan till SDK när användaren öppnar appen genom att klicka igenom ett push-meddelande.

   Följande kodexempel är ett exempel på en möjlig implementering:

   ```objective-c
   // device running < iOS 7 
   - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo { 
       // only send the hit if the app is inactive 
       if (application.applicationState == UIApplicationStateInactive) {  
           [ADBMobile trackPushMessageClickThrough:userInfo]; 
       } 
   } 
   // device running between iOS 7 and iOS 9.3.5 
   - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult)) completionHandler { 
       // only send the hit if the app is inactive 
       if (application.applicationState == UIApplicationStateInactive) { 
           // only run this code if the UNUserNotificationCenterclass is not available or its delegate is not set (pre iOS 10) 
           if (!NSClassFromString(@"UNUserNotificationCenter") || ![UNUserNotificationCenter currentNotificationCenter].delegate) {  
               [ADBMobiletrackPushMessageClickThrough:userInfo]; 
           } 
       } 
       completionHandler(UIBackgroundFetchResultNoData); 
   } 
   // device running >= iOS 10 
   - (void) userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler { 
       if ([response.notification.request.trigger isKindOfClass:UNPushNotificationTrigger.class]) { 
           [ADBMobile trackPushMessageClickThrough:response.notification.request.content.userInfo]; 
       } 
       completionHandler(); 
   }
   ```

1. Om du vill att din beräknade push-målgrupp ska vara korrekt underrättar du SDK när en användare manuellt inaktiverar push-meddelanden för din app genom att anropa `[ADBMobile setPushIdentifier: nil]` i `applicationDidBecomeActive:`-metoden i din `AppDelegate`.

   ```objective-c
   // device running < iOS 7 
   - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo { 
       // only send the hit if the app is inactive 
       if (application.applicationState == UIApplicationStateInactive) {  
           [ADBMobile trackPushMessageClickThrough:userInfo]; 
       } 
   } 
   // device running between iOS 7 and iOS 9.3.5 
   - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult)) completionHandler { 
       // only send the hit if the app is inactive 
       if (application.applicationState == UIApplicationStateInactive) { 
           // only run this code if the UNUserNotificationCenterclass is not available or its delegate is not set (pre iOS 10) 
           if (!NSClassFromString(@"UNUserNotificationCenter") || ![UNUserNotificationCenter currentNotificationCenter].delegate) {  
               [ADBMobiletrackPushMessageClickThrough:userInfo]; 
           } 
       } 
       completionHandler(UIBackgroundFetchResultNoData); 
   } 
   // device running >= iOS 10 
   - (void) userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler { 
       if ([response.notification.request.trigger isKindOfClass:UNPushNotificationTrigger.class]) { 
           [ADBMobile trackPushMessageClickThrough:response.notification.request.content.userInfo]; 
       } 
       completionHandler(); 
   }
   ```

## Exempel {#section_20BEA0D64F7C4D45A5EBEF21066E62AD}

Följande är ett exempel på hur en `AppDelegate.m`-implementering kan se ut:

```objective-c
#import "AppDelegate.h" 
#import "ADBMobile.h" 
 
@implementation AppDelegate 
  
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
    if (NSClassFromString(@"UNUserNotificationCenter")) { 
        UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter]; 
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert + UNAuthorizationOptionSound + UNAuthorizationOptionBadge) 
                              completionHandler:^(BOOL granted, NSError * _Nullable error) {  
            if (granted) { NSLog(@"authorization given"); } 
            else { NSLog(@"authorization rejected"); } 
            if (error) { NSLog(@"error during authorization: %@", error.localizedDescription); } 
        }]; 
        center.delegate = self; 
        [application registerForRemoteNotifications]; 
    } 
    else if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) { 
#pragma GCC diagnostic push 
#pragma GCC diagnostic ignored "-Wdeprecated-declarations"  
        UIUserNotificationType types = UIUserNotificationTypeAlert | UIUserNotificationTypeBadge| UIUserNotificationTypeSound; 
        UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:types categories:nil]; 
        [application registerUserNotificationSettings:settings];  
        [application registerForRemoteNotifications]; 
    } 
    else { 
        [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert| UIRemoteNotificationTypeBadge| UIRemoteNotificationTypeSound]; 
#pragma GCC diagnostic pop 
    } 
 
    return YES; 
} 
 
- (void) applicationDidBecomeActive:(UIApplication *)application {  
    if (NSClassFromString(@"UNUserNotifcationCenter")) { 
        UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter]; 
        [center getNotificationSettingsWithCompletionHandler:^(UNNotificationSettings * _Nonnull settings) { 
            if (settings.authorizationStatus != UNAuthorizationStatusAuthorized) {  
                [ADBMobile setPushIdentifier:nil]; 
            } 
        }]; 
    } 
#pragma GCC diagnostic push 
#pragma GCC diagnostic ignored "-Wdeprecated-declarations"  
    else if ([application respondsToSelector:@selector(isRegisteredForRemoteNotifications)]) { 
        if (![application isRegisteredForRemoteNotifications]) {  
            [ADBMobile setPushIdentifier:nil]; 
        } 
    } 
    else if ([application enabledRemoteNotificationTypes] == UIRemoteNotificationTypeNone) { 
        [ADBMobile setPushIdentifier:nil]; 
    } 
#pragma GCC diagnostic pop 
} 
 
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken { 
    [ADBMobile setPushIdentifier:deviceToken]; 
} 
 
- (void) application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error { 
    [ADBMobile setPushIdentifier:nil]; 
} 
 
- (void) application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo { 
    if (application.applicationState == UIApplicationStateInactive) {  
        [ADBMobile trackPushMessageClickThrough:userInfo];  
    } 
} 
 
- (void) application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler { 
    if (application.applicationState == UIApplicationStateInactive) {  
        if (!NSClassFromString(@"UNUserNotificationCenter") || ![UNUserNotificationCenter currentNotificationCenter].delegate) {  
            [ADBMobile trackPushMessageClickThrough:userInfo]; 
        } 
    } 
 
    completionHandler(UIBackgroundFetchResultNoData); 
} 
 
- (void) userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler { 
    if ([response.notification.request.trigger isKindOfClass:UNPushNotificationTrigger.class]) { 
        [ADBMobile trackPushMessageClickThrough:response.notification.request.content.userInfo]; 
    } 
 
    completionHandler(); 
} 
 
@end
```
