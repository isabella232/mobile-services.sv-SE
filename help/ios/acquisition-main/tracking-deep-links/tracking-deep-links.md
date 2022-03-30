---
description: You can use this information to track deep and deferred deep links in your mobile apps by using the Adobe Mobile iOS SDK.
solution: Experience Cloud Services,Analytics
title: Spåra djuplänkar
uuid: 08dc2820-7fd3-419f-ac2d-dcf12532578a
exl-id: a8b20233-d800-4318-ad4f-39229d8b3a5e
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Tracking deep links{#tracking-deep-links}

Du kan använda den här informationen för att spåra djupa och fördröjda länkar i dina mobilappar med Adobe Mobile iOS SDK.

Mer information om hur marknadsförare använder djuplänkning i sina program finns i [Förvärv](/help/ios/acquisition-main/acquisition.md) i Mobile Services-dokumentationen.

## Tracking deep links

1. Lägg till SDK i ditt projekt och implementera livscykelvärden.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i projektet* in [Kärnimplementering och livscykel](/help/ios/getting-started/dev-qs.md).
1. Register the application to handle Inter-App Communications or support Universal Links.

   Mer information finns i [Kommunikation mellan appar](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html#//apple_ref/doc/uid/TP40007072-CH6-SW10) eller [Stöd för universallänkar](https://developer.apple.com/library/ios/documentation/General/Conceptual/AppSearch/UniversalLinks.html)

1. Spåra djuplänk i openURL.

   Här är ett exempel på en djup länk för spår:

   ```objective-c
   - (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url { 
       [ADBMobile trackAdobeDeepLink:url]; 
       /* 
        Handle deep link 
        */ 
       return YES; 
   } 
   - (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString *, id> *)options { 
       [ADBMobile trackAdobeDeepLink:url]; 
       /* 
        Handle deep link 
        */ 
   
       return YES; 
   }
   ```

The Adobe Mobile SDK can parse key and value pairs of data appended to any deep or Universal Link, provided that the link contains a key with a `a.deeplink.id` label and a corresponding non-null and user generated value. All key and value pairs of data that are appended to the link will be parsed, attached to a lifecycle hit, and sent to Adobe Analytics, provided the link contains the `a.deeplink.id` key and value.

Du kan också välja att lägga till en eller flera av följande reserverade nycklar (med användargenererade värden) till djupet eller Universallänken:

* `a.launch.campaign.trackingcode`
* `a.launch.campaign.source`
* `a.launch.campaign.medium`
* `a.launch.campaign.term`
* `a.launch.campaign.content`

Dessa nycklar är förmappade variabler för rapportering i Adobe Analytics. For more information on mapping and processing rules, see [Processing Rules and Context Data](/help/ios/getting-started/proc-rules.md).

### Tracking deferred deep links

1. Registrera Adobe-dataåteranrop.

   ```objective-c
   [ADBMobile registerAdobeDataCallback:^(ADBMobileDataEvent event, NSDictionary * _Nullable adobeData) { 
   }];
   ```

1. Handtag `ADBMobileDataEventDeepLink` inom `AdobeDataCallback`.

   ```objective-c
   [ADBMobile registerAdobeDataCallback:^(ADBMobileDataEvent event, NSDictionary * _Nullable adobeData) { 
       if (event == ADBMobileDataEventDeepLink) { 
           [self handleDeepLink:adobeData[ADBConfigKeyCallbackDeepLink]]; 
       } 
   }];
   ```

## Deep link public information {#section_44600E9AA68D4A53AA0C14BD86CC5284}

### Metoder

```objective-c
/** 
 * @brief Tracks a Adobe Deep Link click-through 
 * @param url The URL resource received from UIApplication delegate method. 
 * @note Adobe Link data will be appended to the lifecycle call if it is a launch event, otherwise an extra call will be sent. 
 */ 
+ (void) trackAdobeDeepLink:(nullable NSURL *)url;
```

#### Konstanter

```objective-c
/* 
 * Used within ADBMobileDataCallback 
 * Key for deep link URL. 
 */ 
FOUNDATION_EXPORT NSString *const __nonnull ADBConfigKeyCallbackDeepLink;
```
