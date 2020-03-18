---
description: När du har konfigurerat URL:en för djuplänkning i Adobe Mobile Services-gränssnittet finns den här URL:en i push-nyttolasten med adb_deplink-nyckeln.
seo-description: När du har konfigurerat URL:en för djuplänkning i Adobe Mobile Services-gränssnittet finns den här URL:en i push-nyttolasten med adb_deplink-nyckeln.
seo-title: Implementera push-meddelanden med djup länkning
title: Implementera push-meddelanden med djup länkning
uuid: ee9590fc-8bd3-4111-9221-9011d9edbd84
translation-type: tm+mt
source-git-commit: 06144a1695ac40ce984656491456968888f9e96e

---


# Implementera push-meddelanden med djuplänkning {#implement-push-messaging-with-deep-linking}

När du har konfigurerat URL:en för djuplänkning i Adobe Mobile Services-gränssnittet finns den här URL:en i push-nyttolasten med `adb_deeplink` nyckeln.

1. I AppDelegate kan du få tillbaka URL:en för djuplänken och hantera den på egen hand på följande platser:

   * I `application:didFinishLaunchingWithOptions`:

      Om appen inte körs när ett push-klick inträffar, kan du hämta push-nyttolasten från `launchOptions`och djuplänk-URL:en finns i nyttolastordlistan av `adb_deeplink` nyckeln.

   * Delegatmetoderna för fjärrmeddelanden

      I `didReceiveRemoteNotification:` programmet eller i `didReceiveRemoteNotification:fetchCompletionHandler:` programmet kan du hämta URL:en genom att gå till `userInfo` ordlistan med `adb_deeplink` tangenten.

   * Delegatmetoder för `UNUserNotificationCenter`

      I `userNotificationCenter:didReceiveNotificationResponse:withCompletionHandler:` metoden kan du hämta push-nyttolasten från `userInfo` ordlistan, i `adb_deeplink` nyckeln.

Exempel:

```objective-c
- (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSDictionary *remoteNotification = launchOptions[UIApplicationLaunchOptionsRemoteNotificationKey]; 
    if (remoteNotification && [remoteNotification isKindOfClass:[NSDictionary class]]) { 
        NSString *deeplink = remoteNotification[@"adb_deeplink"]; 
        // handle deep link url 
    }
    return YES; 
} 
  
// app target < iOS 7 
- (void) application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo { 
    // only send the hit if the app is not active 
    if (application.applicationState == UIApplicationStateInactive) { 
        [ADBMobile trackPushMessageClickThrough:userInfo]; 
        NSString *deeplink = userInfo[@"adb_deeplink"]; 
        // handle deep link url 
    } 
} 
  
// app target >= iOS 7 
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler { 
    if (application.applicationState == UIApplicationStateInactive) { 
        [ADBMobile trackPushMessageClickThrough:userInfo]; 
        NSString *deeplink = userInfo[@"adb_deeplink"]; 
        // handle deep link url 
    } 
    ... 
} 
 
// if using UNUserNotificationCenterDelegate and device is running iOS 10 or newer 
- (void) userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler { 
    if ([response.notification.request.trigger isKindOfClass:UNPushNotificationTrigger.class]) { 
        [ADBMobile trackPushMessageClickThrough:response.notification.request.content.userInfo]; 
        NSString *deeplink = response.notification.request.content.userInfo[@"adb_deeplink"]; 
        // handle deep link url  
    } 
    ... 
}
```

