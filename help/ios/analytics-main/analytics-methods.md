---
description: Här är en lista över Adobe Analytics-metoder som finns i iOS-biblioteket.
seo-description: Här är en lista över Adobe Analytics-metoder som finns i iOS-biblioteket.
seo-title: Analysmetoder
solution: Experience Cloud,Analytics
title: Analysmetoder
topic: Developer and implementation
uuid: d49fe6de-cb32-4b96-9891-c567310e59a6
translation-type: tm+mt
source-git-commit: bc11c1e7a4a11657ee89c40ddcbd37377ce50bb5
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 33%

---


# Analysmetoder {#analytics-methods}

Här är en lista över Adobe Analytics-metoder som finns i iOS-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna är prefasta enligt lösningen. Experience Cloud ID-metoder har prefix med `track`.

Var och en av dessa metoder används för att skicka data till din Adobe Analytics rapportsvit.

* **trackState: &#x200B; data:**

   Lägen är de vyer som är tillgängliga i din app, till exempel `home dashboard`, `app settings`och `cart`så vidare. Dessa lägen liknar sidor på en webbplats och anropar `trackState` stegvisa sidvyer. Om `state` är tom visas den som *programnamnsprogramversion (build)* i rapporter. Om det här värdet visas i rapporter kontrollerar du att du anger det `state` i varje `trackState` samtal.

   >[!TIP]
   >
   >Det här är det enda spårningsanropet som ökar sidvisningen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void)  trackState:(NSString  *)state
                      data:(NSDictionary  *)data;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackState:@"loginScreen"
                        data:nil]; 
      ```

* **trackAction: &#x200B; data:**

   Spårar en åtgärd i din app. Åtgärder som du vill mäta, t.ex. `logons`, `banner taps`, `feed subscriptions`och andra mätvärden, utförs i appen.

   >[!TIP]
   >
   >Om du har kod som kan köras medan programmet är i bakgrunden (till exempel en hämtning av bakgrundsdata) använder du `trackActionFromBackground` istället.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +  (void)  trackAction:(NSString  *)action
                        data:(NSDictionary  *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackAction:@"heroBannerTouched"
                         data:nil]; 
      ```

* **trackingIdentifier**

   Hämtar identifieraren för analysspårning.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (NSString *) trackingIdentifier; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *trackingId = [ADBMobile trackingIdentifier];
      ```

* **trackActionFromBackground: &#x200B; data:**

   Spårar en åtgärd som har inträffat i bakgrunden, som förhindrar att livscykelhändelser utlöses i vissa scenarier.

   >[!TIP]
   >
   >Den här metoden ska bara anropas i kod som körs medan programmet finns i bakgrunden.

   * Här är syntaxen för den här metoden:

      ```objective-c
       +  (void)  trackActionFromBackground:(NSString  *)action
                                       data:(NSDictionary  *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackActionFromBackground:@"downloadedUpdate"
                                       data:nil];
      ```

* **trackLocation: &#x200B; data:**

   Skickar de aktuella x y-koordinaterna. I används även intressepunkter som är definierade i filen för att avgöra om den plats som anges som parameter finns i någon av dina POI:er. `ADBMobileConfig.json` Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation` anropet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +  (void)  trackLocation:(CLLocation  *)location
                          data:(NSDictionary  *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackLocation:userLocation
                           data:nil]; 
      ```

* **trackBeacon: &#x200B; data:**

   Spårar när en användare kommer in i närheten av en beacon.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +  (void)  trackLocation:(CLBeacon  *)beacon
                          data:(NSDictionary  *)data;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackBeacon:beacon
                         data:nil];
      ```

* **trackingClearCurrentBeacon**

   Rensar beacons data efter att en användare lämnat beacons närhet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) trackingClearCurrentBeacon;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile trackingClearCurrentBeacon];
      ```

* **trackLifetimeValueIncrease: &#x200B; data:**

   Lägger `amount` till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```objective-c
       +  (void)  trackLifetimeValueIncrease:(NSDecimalNumber  *)amount
                                       data:(NSDictionary  *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackLifetimeValueIncrease:30
                                         data:nil];
      ```

* **trackTimedActionStart: &#x200B; data:**

   Starta en tidsbestämd åtgärd med namnet `action`. Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +  (void)  trackTimedActionStart:(NSString  *)action
                                  data:(NSDictionary  *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackTimedActionStart:@"cartToCheckout"
                                  data:nil]; 
      ```

* **trackTimedActionUpdate: &#x200B; data:**

   Skicka in `data` för att uppdatera kontextdata som är associerade med den angivna `action`. Det `data` som skickas läggs till i befintliga data för åtgärden, och om samma nyckel redan har definierats för `action`skrivs data över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```objective-c
       +  (void)  trackTimedActionUpdate:(NSString  *)action
                                    data:(NSDictionary  *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackTimedActionUpdate:@"cartToCheckout"
                                    data:@{@"quantity":@"3"}];
      ```

* **trackTimedActionEnd: &#x200B; logik:**

   Avsluta en tidsbestämd åtgärd. Om du anger `block`det får du tillgång till de slutliga tidsvärdena och kan manipulera `data` innan den sista träffen skickas.

   >[!TIP]
   >
   >Om du anger `block`det måste du återvända `YES` för att skicka en träff. Om du skickar in `nil` för `block` skickas den sista träffen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +  (void)  trackTimedActionEnd:(NSString  *)action
                          logic:(BOOL  (^)  (NSTimeInterval  inAppDuration,
                                                  NSTimeInterval totalDuration,
                                                  NSMutableDictionary *data))block; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile  trackTimedActionEnd:@"cartToCheckout"
                    logic:^(NSTimeInterval inApp,
                    NSTimeInterval  total,
                    NSMutableDictionary  *data)  {
                        data[@"price"]  =  @"49.95";
                        return  YES;
                    }];
      ```

* **trackingTimedActionExists**

   Returnerar om en tidsbestämd åtgärd pågår.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (BOOL) trackingTimedActionExists:(NSString *)action;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      BOOL *actionExists = [ADBMobile trackingTimedActionExists];
      ```

* **trackingSendQueuedHits**

   Kräver SDK 4.1. Oavsett hur många träffar som är köade tvingas biblioteket att skicka alla träffar i offlinekön.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) trackingSendQueuedHits;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile trackingSendQueuedHits]; 
      ```

* **trackingGetQueueSize**

   Hämtar antalet träffar som för närvarande finns i offlinekö.

   * Här är syntaxen för den här metoden:

      ```objective-c
       + (NSUInteger) trackingGetQueueSize;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSUInteger *queueSize = [ADBMobile trackingGetQueueSize];
      ```

* **trackingClearQueue**

   Tar bort alla träffar från offlinekön.

   >[!CAUTION]
   >
   >Var försiktig när du rensar kön manuellt. Den här processen kan inte ångras.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) trackingClearQueue;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile trackingClearQueue]; 
      ```



* **trackPushMessageClickThrough**

   Spårar ett push-meddelande med klickfrekvens.

   >[!IMPORTANT]
   >
   >Den här metoden ökar inte sidvisningen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) trackPushMessageClickThrough:(NSDictionary *)userInfo;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      -  (void)application:(UIApplication  *)application  
      didReceiveRemoteNotification:(NSDictionary  *)userInfo  
      fetchCompletionHandler:(void  (^)
      (UIBackgroundFetchResult))completionHandler  {
          // only send the hit if the app is not active
          if (application.applicationState !=  UIApplicationStateActive)  {
              [ADBMobile  trackPushMessageClickThrough:userInfo];
      
          }
          completionHandler(UIBackgroundFetchResultNoData);
      }
      ```
