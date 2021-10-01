---
description: Du kan använda den här informationen för att spåra djupa och fördröjda länkar i dina mobilappar med hjälp av Adobe Mobile iOS SDK.
solution: Experience Cloud,Analytics
title: Spåra djuplänkar
uuid: 08dc2820-7fd3-419f-ac2d-dcf12532578a
exl-id: a8b20233-d800-4318-ad4f-39229d8b3a5e
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Spåra djuplänkar{#tracking-deep-links}

Du kan använda den här informationen för att spåra djupa och fördröjda länkar i dina mobilappar med hjälp av Adobe Mobile iOS SDK.

Mer information om hur marknadsförare använder djuplänkning i sina program finns i [Förvärva](/help/ios/acquisition-main/acquisition.md) i dokumentationen för mobiltjänster.

## Spåra djuplänkar

1. Lägg till SDK i ditt projekt och implementera livscykelvärden.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i ditt projekt* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Registrera programmet för att hantera kommunikation mellan appar eller stödja universallänkar.

   Mer information finns i [Interapp Communications](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html#//apple_ref/doc/uid/TP40007072-CH6-SW10) eller [Support Universal Links](https://developer.apple.com/library/ios/documentation/General/Conceptual/AppSearch/UniversalLinks.html)

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

Adobe Mobile SDK kan analysera nyckel- och värdepar för data som läggs till i en djup eller universell länk, förutsatt att länken innehåller en nyckel med en `a.deeplink.id`-etikett och ett motsvarande värde som inte är null och som genererats av användaren. Alla nyckel- och värdepar med data som läggs till länken tolkas, kopplas till en livscykelträff och skickas till Adobe Analytics, förutsatt att länken innehåller nyckeln och värdet `a.deeplink.id`.

Du kan också välja att lägga till en eller flera av följande reserverade nycklar (med användargenererade värden) till djupet eller Universallänken:

* `a.launch.campaign.trackingcode`
* `a.launch.campaign.source`
* `a.launch.campaign.medium`
* `a.launch.campaign.term`
* `a.launch.campaign.content`

Dessa nycklar är förmappade variabler för rapportering i Adobe Analytics. Mer information om mappnings- och bearbetningsregler finns i [Bearbetningsregler och kontextdata](/help/ios/getting-started/proc-rules.md).

### Spåra fördröjda djuplänkar

1. Registrera Adobe-dataåteranrop.

   ```objective-c
   [ADBMobile registerAdobeDataCallback:^(ADBMobileDataEvent event, NSDictionary * _Nullable adobeData) { 
   }];
   ```

1. Hantera `ADBMobileDataEventDeepLink` inom `AdobeDataCallback`.

   ```objective-c
   [ADBMobile registerAdobeDataCallback:^(ADBMobileDataEvent event, NSDictionary * _Nullable adobeData) { 
       if (event == ADBMobileDataEventDeepLink) { 
           [self handleDeepLink:adobeData[ADBConfigKeyCallbackDeepLink]]; 
       } 
   }];
   ```

## Allmän information om länkar {#section_44600E9AA68D4A53AA0C14BD86CC5284}

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
