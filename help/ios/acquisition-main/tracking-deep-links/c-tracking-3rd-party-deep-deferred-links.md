---
description: Använd iOS SDK för att implementera spårning av fördröjda djuplänkar från tredje part.
seo-description: Använd iOS SDK för att implementera spårning av fördröjda djuplänkar från tredje part.
seo-title: Spåra fördröjda djuplänkar från tredje part
title: Spåra fördröjda djuplänkar från tredje part
uuid: 5525b609-e926-44b9-b0f5-38e9dd7c9761
translation-type: tm+mt
source-git-commit: 4b5be6c51c716114e597a80d475f838e23abb1b1

---


# Spåra fördröjda länkar från tredje part {#tracking-third-party-deferred-deep-links}

Använd iOS SDK för att implementera spårning av fördröjda djuplänkar från tredje part.

## Klassisk Adobe Mobile SDK-djuplänkning {#section_D114FA1EB9664EAA82E036A990694B26}

Adobe Mobile SDK har för närvarande stöd för djuplänkning där apputvecklaren förväntas anropa API:t och skicka URL:en för djuplänkning, som är den fingeravtrycks-URL som genereras i Adobe Mobile Services under konfigurationen. `trackAdobeDeepLink` SDK:n skickar fingeravtrycksdata till skrivaren för att hämta inhämtningsdata och lägger till dem i installations-/startanalysen för att anropa kontextdata som en del av livscykeln. Dessutom lägger SDK även till data för borttagning av länkar från URL-parametrar för överordnad länk. Mer information om djuplänkning finns i [Spåra djuplänkar](/help/ios/acquisition-main/tracking-deep-links/tracking-deep-links.md).

## Djuplänkning på Facebook {#section_6A9DACB54A2F4CDEBE9C744DEFADFDED}

En annonsskapare kan skapa en annons på Facebook som en länk. När användare klickar på annonsen på Facebook går den direkt till den information som de är intresserade av appen i. Den djupa länken är **inte** en fingerskrivars-URL. Under annonskonfigurationen finns det dock ett alternativ för att ange en webblänk-URL från tredje part. En apputvecklare som använder Experience Clouds SDK för mobiler och tjänster förväntas ange den Mobile Services-konfigurerade URL:en för fingeravtryck i det här fältet. Om allt är korrekt konfigurerat skickar Facebook SDK den här URL:en till programmet när appen installeras eller startas.

## Konfigurera SDK:er {#section_834CD3109175432B8173ECB6EA7DE315}

1. Konfigurera Facebook SDK.

   Mer information finns i följande:

   * [Komma igång med Facebook SDK för iOS](https://developers.facebook.com/docs/ios/getting-started)
   * [Installationsprogram för avlänkning](https://developers.facebook.com/docs/app-ads/deep-linking#os)

1. Om du vill konfigurera SDK anropar du `trackAdobeDeepLink` och skickar URL:en till SDK:erna:

   ```objective-c
   - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation 
   { 
     [ADBMobile trackAdobeDeepLink:url]; 
     return YES; 
   }
   ```

   >[!TIP]
   >
   >Se till att URL:en för djuplänken har en nyckel med namnet `a.deeplink.id`. Inga URL-parametrar läggs till i kontextdata om URL:en saknar `a.deeplink.id` parametern.

Om programmet är konfigurerat enligt beskrivningen ovan fungerar den aktuella AMSDK-versionen bra och lägger till djuplänksdata för att installera/starta analysanrop korrekt.

## Aktivera funktionen i ett exempelprogram {#section_64C15E269E89424B8E3D029F88094620}

1. Registrera ett URL-schema.

   Kontrollera att du har registrerat ett URL-schema, som är samma som URL:en för djuplänken.

   ```objective-c
   <key>CFBundleURLTypes</key> 
       <array> 
           <dict> 
               <key>CFBundleURLSchemes</key> 
               <array> 
                   <string>sampleapptest</string> 
               </array> 
           </dict> 
       </array>
   ```

1. Länka Facebooks SDK:er.

   ![Facebook-resurser](assets/link-fb-sdk.jpg)

1. Redigera `AppDelegate`.

   1. Importera sidhuvuden.

      ```objective-c
      /************************************************************************* 
      ADOBE SYSTEMS INCORPORATED 
      Copyright 2015 Adobe Systems Incorporated 
      All Rights Reserved. 
      NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the 
      terms of the Adobe license agreement accompanying it.  If you have received this file from a 
      source other than Adobe, then your use, modification, or distribution of it requires the prior 
      written permission of Adobe. 
      
      **************************************************************************/ 
      
      #import "AppDelegate.h" 
      #import "GalleryViewController.h" 
      #import "SimpleTrackingController.h" 
      #import "PostbackController.h" 
      #import "InAppMessageViewController.h" 
      #import "LifetimeValueController.h" 
      #import "LocationTargetingController.h" 
      #import "MediaViewController.h" 
      #import "TimedActionController.h"
      
      // Uncomment after including the facebook sdks. 
      @import FBSDKCoreKit; 
      @import Bolts;
      ```

   1. Lägg till handtaget för fördröjd djuplänkning.

      ```objective-c
      - (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
          /* 
           * Adobe Tracking - Analytics 
           * 
           * turn on debug logging for the ADBMobile SDK 
           * enable the collection of lifecycle data 
           */ 
              if (launchOptions[UIApplicationLaunchOptionsURLKey] == nil) { 
                  if (NSClassFromString(@"FBSDKAppLinkUtility") != nil) 
                  { 
                      [NSClassFromString(@"FBSDKAppLinkUtility") performSelector:@selector(fetchDeferredAppLink:) withObject:^(NSURL *url, NSError *error) { 
                          if (error) { 
                              NSLog(@"Received error while fetching deferred app link %@", error); 
                          } 
                          if (url) { 
                              [[UIApplication sharedApplication] openURL:url]; 
                          } 
                      }]; 
                  } 
          } 
          ..... 
          ..... 
          return YES; 
      }
      ```

   1. Anropa `trackAdobeDeepLink` API:t och skicka URL:en för djuplänken till SDK:n.

      ```objective-c
      - (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString *, id> *)options { 
          [self handleDeepLink:url]; 
      
          return YES; 
      }
      ```

