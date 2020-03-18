---
description: Den här informationen hjälper dig att implementera iOS-biblioteket och samla in livscykelvärden som starter, uppgraderingar, sessioner, engagerade användare och så vidare.
seo-description: Den här informationen hjälper dig att implementera iOS-biblioteket och samla in livscykelvärden som starter, uppgraderingar, sessioner, engagerade användare och så vidare.
seo-title: Kärnimplementering och livscykel
solution: Marketing Cloud,Analytics
title: Kärnimplementering och livscykel
topic: Developer and implementation
uuid: 96d06325-e424-4770-8659-4b5431318ee3
translation-type: tm+mt
source-git-commit: bd8aa0c7ff58e4cf28a67b8a107db52fb30cd3dc

---


# Kärnimplementering och livscykel {#core-implementation-and-lifecycle}

Den här informationen hjälper dig att implementera iOS-biblioteket och samla in livscykelvärden som starter, uppgraderingar, sessioner, engagerade användare och så vidare.

## Ladda ned SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

>[!IMPORTANT]
>
>Om du vill hämta SDK:er **måste** du använda iOS 6 eller senare.

**Förutsättning**

Innan du hämtar SDK slutför du stegen i *Skapa en rapportsvit* i [Core-implementering och livscykel](/help/ios/getting-started/requirements.md) för att konfigurera en utvecklingsrapportsvit och hämta en förifylld version av konfigurationsfilen.

Så här hämtar du SDK:

1. Ladda ned, zippa upp `[Your_App_Name_]AdobeMobileLibrary-4.*-iOS.zip` filen och kontrollera att du har följande programvarukomponenter:

   * `ADBMobile.h`, målfil C-huvudfilen som används för iOS AppMeasurement.
   * `ADBMobileConfig.json`, som är SDK-konfigurationsfilen som är anpassad för ditt program.
   * `AdobeMobileLibrary.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64).

      Den här feta binärfilen bör länkas när målet är avsett för en iOS-app.

   * `AdobeMobileLibrary_Extension.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64).

      Denna binära fetthalt bör länkas när målet är avsett för ett iOS-tillägg.

   * `AdobeMobileLibrary_Watch.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för Apple Watch-enheter (armv7k) och simulatorer (i386, x86_64).

      Denna feta binärfil bör länkas när målet är avsett för en Apple Watch-tilläggsapp (watchOS 2).

   * `AdobeMobileLibrary_TV.a`, en bitkodsaktiverad binär fetthalt som innehåller biblioteksbyggen för nya Apple TV-enheter (arm64) och simulator (x86_64).

      Den här feta binärfilen ska länkas när målet är avsett för en Apple TV-app (tvOS).

>[!IMPORTANT]
>
>Om du hämtar SDK utanför Adobe Mobile Services-gränssnittet måste filen konfigureras manuellt `ADBMobileConfig.json` . Om du inte har använt Analytics tidigare och Mobile SDK tidigare läser du [Innan du börjar](/help/ios/getting-started/requirements.md) för att konfigurera en utvecklingsrapportsvit och hämta en förifylld version av konfigurationsfilen.

## Lägg till SDK och konfigurationsfilen i ditt projekt {#section_93C25D893B4A4CD3B996CF3C5590C8DC}

1. Starta Xcode IDE och öppna appen.
1. Dra mappen till projektnavigeraren och släpp den `AdobeMobileLibrary` under projektet.
1. Kontrollera följande:

   * Kryssrutan är markerad **[!UICONTROL Copy Items if needed]** .
   * **[!UICONTROL Create groups]** är markerat.
   * Ingen av kryssrutorna i **[!UICONTROL Add to targets]** avsnittet är markerad.
   ![](assets/step_3.png)

1. Klicka på **[!UICONTROL Finish]**.
1. I **[!UICONTROL Project Navigator]** väljer du **`ADBMobileConfig.json`**.
1. I **[!UICONTROL File Inspector]** lägger du till JSON-filen i alla mål i projektet som ska använda Adobe SDK.

   ![](assets/step_4.png)

1. I **[!UICONTROL Project Navigator]** utför du följande steg:

   1. Klicka på din app.
   1. Välj dina mål på **[!UICONTROL General]** fliken och länka de nödvändiga ramverken och biblioteken i **[!UICONTROL Linked Frameworks]** - och **[!UICONTROL Libraries]** -avsnitten.
   * **iOS-appmål**
      * `SystemConfiguration.framework`
      * `WebKit.framework`
      * `libsqlite3.0.tbd`
      * `AdobeMobileLibrary.a`
      * `CoreLocation.framework` (valfritt, men krävs för geospårning)
   * **iOS-tilläggsmål**

      * `SystemConfiguration.framework`
      * `libsqlite3.0.tbd`
      * `AdobeMobileLibrary\_Extension.a`
   * **Apple Watch (watchOS 2) Target**

      * `libsqlite3.0.tbd`
      * `AdobeMobileLibrary\_Watch.a`
   * **Apple TV-mål (tvOS)**

      * `SystemConfiguration.framework`
      * `libsqlite3.0.tbd`
      * `AdobeMobileLibrary\_TV.a`
   >[!CAUTION]
   >
   > Länkning av mer än en `AdobeMobileLibrary*.a` fil i samma mål resulterar i oväntat beteende eller oförmåga att bygga.

1. Bekräfta att appen byggs utan fel.

## Implementera livscykelvärden {#section_532702562A7A43809407C9A2CBA80E1E}

>[!IMPORTANT]
>
>iOS skickar livscykelinformation med eller utan anrop `collectlifecycledata`och `collectlifecycledata` är bara ett sätt att initiera livscykeln tidigare i programmets startsekvens.

När du har aktiverat livscykeln skickas en träff varje gång appen startas för att mäta öppningar, uppgraderingar, sessioner, engagerade användare och andra [livscykelvärden](/help/ios/metrics.md).

Lägg till ett `collectLifecycleData`/- `collectLifecycleDataWithAdditionalData` samtal i `application:didFinishLaunchingWithOptions`:

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
 [ADBMobile collectLifecycleData]; 
    return YES; 
}
```

### Inkludera ytterligare data vid livscykelanrop

Om du vill inkludera ytterligare data med livscykelmätanrop använder du `collectLifecycleDataWithAdditionalData`:

>[!IMPORTANT]
>
>Alla data som skickas till SDK via `collectLifecycleDataWithAdditionalData:` bevaras i `NSUserDefaults` av SDK. SDK:n tar bort de värden i `NSDictionary` parametern som inte är av `NSString` - eller `NSNumber` typen.

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
    NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
    [contextData setObject:@"Game" forKey:@"myapp.category"]; 
    [ADBMobile collectLifecycleDataWithAdditionalData:contextData]; 
    return YES; 
}
```

Ytterligare kontextdatavärden som skickas med `collectLifecycleDataWithAdditionalData` måste mappas till anpassade variabler i Adobe Mobile Services:

![](assets/map-variable-lifecycle.png)

Andra livscykelvärden samlas in automatiskt. Mer information finns i [Livscykelvärden](/help/ios/metrics.md).

## Vad ska du göra härnäst? {#section_A24DC703359D4B5C8F493D6421306FD3}

Utför följande uppgifter:

* [Spåra applägen](/help/ios/analytics-main/states.md)
* [Spåra programåtgärder](/help/ios/analytics-main/actions.md)
