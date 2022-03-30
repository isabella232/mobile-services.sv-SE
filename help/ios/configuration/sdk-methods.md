---
description: Här är en lista över metoder som finns i iOS-biblioteket.
solution: Experience Cloud Services,Analytics
title: Konfigurationsmetoder
topic-fix: Developer and implementation
uuid: 623c7b07-fbb3-4d39-a5c4-e64faec4ca29
exl-id: b6841808-8fa8-4090-8cb3-ce647a3d5d08
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 21%

---

# Konfigurationsmetoder {#configuration-methods}

Här är en lista över metoder som finns i iOS-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service.

* **setAppExtensionType**

   Konfigurerar inställningen för Adobe Mobile SDK för att avgöra vilken typ av tillägg som körs för närvarande.

   Ange något av följande värden:
   * `ADBMobileAppExtensionTypeRegular` - tillägget medföljer ett program som innehåller det.
   * `ADBMobileAppExtensionTypeStandAlone` - tillägget paketeras inte med ett innehållande program.

   >[!TIP]
   >
   >Den här metoden bör **endast** användas om din app har ett tillägg eller är ett fristående tillägg. Mer information finns i *ADBMobleAppExtensionType* nedan.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) setAppExtensionType:(ADBMobileAppExtensionType)type;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile setAppExtensionType:ADBMobileAppExtensionTypeStandAlone]; 
      ```



* **version**

   Returnerar den aktuella versionen av Adobe Mobile-biblioteket.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(NSString*) version;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString*libraryVersion = [ADBMobileversion];
      ```

* **privacyStatus**

   Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus:

   * `ADBMobilePrivacyStatusOptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut` - träffar tas bort.
   * `ADBMobilePrivacyStatusUnknown` - Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras för att anmäla sig.
Standardvärdet anges i `ADBMobileConfig.json` -fil.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (ADBMobilePrivacyStatus) privacyStatus;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobilePrivacyStatus privacyStatus = [ADBMobileprivacyStatus];
      ```

* **setPrivacyStatus**

   Anger sekretessstatus för den aktuella användaren till `status`.

   Ange något av följande värden:

   * `ADBMobilePrivacyStatusOptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut` - träffar tas bort.
   * `ADBMobilePrivacyStatusUnknown` - Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras för att anmäla sig.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) setPrivacyStatus:(ADBMobilePrivacyStatus)status;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile setPrivacyStatus:ADBMobilePrivacyStatusOptIn];
      ```

* **lifeValue**

   Returnerar livstidsvärdet för den aktuella användaren. Standardvärdet är `0`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (NSDecimalNumber *) lifetimeValue;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDecimalNumber *lifeValue = [ADBMobile lifetimeValue];
      ```

* **trackingIdentifier**

   Returnerar den automatiskt genererade besökaridentifieraren. Detta är ett programspecifikt unikt besökar-ID som genereras av Adobe servrar. Om det inte går att nå Adobe vid genereringen genereras ID:t med Apple CFUID. Värdet genereras vid den första starten och lagras och används från den tidpunkten och framåt. Detta ID bevaras mellan programuppgraderingar, sparas och återställs under standardprocessen för säkerhetskopiering av program och tas bort vid avinstallation.

   >[!TIP]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas det tidigare anpassade eller automatiskt genererade besökar-ID:t och lagras som en anpassad användaridentifierare. Mer information finns i `userIdentifier` rad nedan. Detta bevarar besöksdata mellan SDK-uppgraderingar. För nya installationer på 4.x SDK är användaridentifieraren `nil` och spårnings-ID används.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (NSString *) trackingIdentifier;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *tid = [ADBMobile trackingIdentifier];
      ```

* **userIdentifier**

   Om en anpassad identifierare har angetts returneras användaridentifieraren. Om ingen anpassad identifierare har angetts `nil` returneras. Standardvärdet är `nil`.

   >[!TIP]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas det tidigare anpassade eller automatiskt genererade besökar-ID:t och lagras som en anpassad användaridentifierare. Detta bevarar besöksdata mellan uppgraderingar av SDK.

   För nya installationer på 4.x SDK är användaridentifieraren `nil` till.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(NSString *) userIdentifier;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *uid = [ADBMobileuserIdentifier];
      ```

* **setUserIdentifier**

   Anger användaridentifieraren till `identifier`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(void)setUserIdentifier:(NSString*)identifier;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile setUserIdentifier:@"billybob"]; 
      ```

* **debugLogging**

   Returnerar den aktuella inställningen för felsökningsloggning. Standardvärdet är `NO`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (BOOL) debugLogging;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      BOOL debugging = [ADBMobile debugLogging];
      ```

* **setDebugLogging**

   Anger loggningsinställningar för felsökning till `debug`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) setDebugLogging:(BOOL)debug;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile setDebugLogging:YES];
      ```

* **keepLifecycleSessionAlive**

   Anger för SDK att nästa återupptagning från bakgrunden inte ska starta en ny session, oavsett värdet på tidsgränsen för livscykelsessionen i konfigurationsfilen.

   >[!TIP]
   >
   >Den här metoden är avsedd att användas för program som registrerar sig för meddelanden i bakgrunden och ska endast anropas från koden som körs medan programmet körs i bakgrunden.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) keepLifecycleSessionAlive;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile keepLifecycleSessionAlive]; 
      ```

* **collectLifecycleData**

   Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/ios/metrics.md).

   >[!TIP]
   >
   >Den rekommenderade platsen att anropa den här metoden finns på `application:didFinishLaunchingWithOptions:`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) collectLifecycleData;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile collectLifecycleData];
      ```

* **collectLifecycleDataWithAdditionalData:**

   Gör att ni kan skicka in ytterligare data när ni samlar in livscykelvärden.

   Den här metoden måste anropas från appens startpunkt. I tillämpliga fall kan detta omfatta en eller båda metoderna `application:didFinishLaunchingWithOptions:` och/eller `applicationWillEnterForeground:` i klassen AppDelegate.

   >[!IMPORTANT]
   >
   >Data som skickas till SDK via `collectLifecycleDataWithAdditionalData:` kommer att sparas av SDK i `NSUserDefaults`. SDK:n kommer att ta bort värden i `NSDictionary` parameter som inte är av typen `NSString` eller `NSNumber`. Används  `collectLifecycleDataWithAdditionalData:`måste du ha SDK **version 4.4** eller senare.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) collectLifecycleDataWithAdditionalData:(nullableNSDictionary*)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile collectLifecycleDataWithAdditionalData:@{@"entryType":@"appShortcutIcon"}]; 
      ```

* **pauseCollectingLifecycleData**

   Använd detta API för att pausa insamlingen av livscykeldata. Mer information finns i [Livscykelvärden](/help/ios/metrics.md).

   >[!IMPORTANT]
   >
   >I `applicationDidEnterBackground` delegeringsmetod måste du först anropa `pauseCollectingLifecycleData` -metod.
   >
   >API:t tillhandahålls för att åtgärda problemet på iPhone7/7s eller äldre enheter med iOS 13, där sessionslängdsmåttet blev onormalt. Detta berodde på några okända ändringar som gjorts i iOS 13, där iOS inte lämnar tillräckligt med tid för att bakgrundsaktiviteten ska slutföras när du säkerhetskopierar programmet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) pauseCollectingLifecycleData;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      - (void)applicationDidEnterBackground:(UIApplication *)application{
          // manually stop the lifecycle of SDK
          // important: do NOT call any track state or track action after this line
          [ADBMobile pauseCollectingLifecycleData];   
      
      
          // the following code is optional, may help to mitigate the issue a bit more. If you have other logic to run here that probably takes more than 10ms, then there is no need to add this line of code.
          [NSThread sleepForTimeInterval:0.01];
      
      
          // app's code to handle applicationDidEnterBackground
      }
      ```


* **overrideConfigPath**

   Gör att du kan läsa in en annan ADBMomobile JSON-konfigurationsfil när programmet startas. Den olika konfigurationen används tills programmet stängs.

   >[!IMPORTANT]
   >
   >Används `overrideConfigPath`måste du ha SDK version 4.2 eller senare.

   * Här är syntaxen för den här metoden:

      ```objective-c
       + (void) overrideConfigPath: (nullableNSString *) path;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *filePath = [[NSBundle mainBundle] pathForResource:@"ExampleJSONFile" ofType:@"json"]; 
      [ADBMobile overrideConfigPath:filePath];
      ```

* **setPushIdentifier**

   Anger enhetstoken för push-meddelanden.

   >[!IMPORTANT]
   >
   >Den här metoden bör endast användas i  `application:didRegisterForRemoteNotificationsWithDeviceToken:` -metod.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) setPushIdentifier:(NSData *)deviceToken;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      - (void) application:(UIApplication *) application  didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken { 
      [ADBMobile setPushIdentifier:deviceToken];  
      }
      ```

* **setAdvertisingIdentifier**

   Anger IDFA i SDK. Om IDFA har angetts i SDK skickas IDFA i livscykeln. Den kan också nås i Signals (Postback).

   >[!TIP]
   >
   >Hämta IDFA från Apple API:er **endast** om du använder en annonstjänst. Om du hämtar IDFA, och inte använder det på rätt sätt, kan din app refuseras.
   >
   >Om ditt program kräver IDFA ska du kontrollera [Apple dokumentation](https://developer.apple.com/documentation/adsupport) om du vill fråga användaren om annonsspårning och hämta IDFA-värdet.
   >
   >För iOS 14+ nya [App Tracking Transparency Framework](https://developer.apple.com/documentation/apptrackingtransparency) måste implementeras för att IDFA-värdet ska kunna hämtas.
   * Här är syntaxen för den här metoden:

      ```objective-c
      +(void) setAdvertisingIdentifier:(NSString*)identifier;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *idfa = // retrieve IDFA using AdSupport (before iOS 14.0) and/or AppTrackingTransparency (iOS 14.0+)
      [ADBMobile setAdvertisingIdentifier:idfa]; 
      ```

## ADBMobleAppExtensionType enum {#section_18DB491D0ABC4765BB5A467D8FEF4F1B}

```objective-c
/** 
 * @brief An enum type. 
 * The possible types of app extension you might use 
 * @see setAppExtensionType 
 */ 
typedef NS_ENUM(NSUInteger, ADBMobileAppExtensionType) { 
    ADBMobileAppExtensionTypeRegular = 0, /*!< Enum value ADBMobileAppExtensionTypeRegular. */ 
    ADBMobileAppExtensionTypeStandAlone = 1 /*!< Enum value ADBMobileAppExtensionTypeStandAlone. */ 
};
```
