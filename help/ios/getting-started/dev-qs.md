---
description: Den här informationen hjälper dig att implementera iOS-biblioteket och samla in livscykelvärden som starter, uppgraderingar, sessioner, engagerade användare och så vidare.
solution: Experience Cloud,Analytics
title: Kärnimplementering och livscykel
topic-fix: Developer and implementation
uuid: 96d06325-e424-4770-8659-4b5431318ee3
exl-id: 5fb2d534-c2e8-480a-aaee-0e71dd55feb6
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Kärnimplementering och livscykel {#core-implementation-and-lifecycle}

Den här informationen hjälper dig att implementera iOS-biblioteket och samla in livscykelvärden som starter, uppgraderingar, sessioner, engagerade användare och så vidare.

## Ladda ned SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

>[!IMPORTANT]
>
>SDK kräver iOS 8 eller senare.

**Förutsättning**

Innan du hämtar SDK slutför du stegen i *Skapa en Report Suite* i [Core implementation and lifecycle](/help/ios/getting-started/requirements.md) för att konfigurera en utvecklingsrapportsvit och hämta en förifylld version av konfigurationsfilen.

Så här hämtar du SDK:

>[!IMPORTANT]
>
>Från och med version 4.21.0 distribueras SDK via XCFrameworks. Följ stegen nedan om du använder 4.21.0 eller senare.
>
>Version 4.21.0 av SDK kräver Xcode 12.0 eller senare och, om tillämpligt, Cocoapods 1.10.0 eller senare.

1. Ladda ned, zippa upp filen `[Your_App_Name_]AdobeMobileLibrary-4.*-iOS.zip` och kontrollera att du har följande programvarukomponenter i katalogen `AdobeMobileLibrary`:

   * `ADBMobile.h` - Objective-C-huvudfilen som används för iOS SDK.
   * `ADBMobileConfig.json` - SDK-konfigurationsfilen som är anpassad för din app.
   * `AdobeMobile.xcframework` - innehåller två binära fetter, en för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64, arm64).

      Denna XCFramwork ska vara länkad när en iOS-app används.

   * `AdobeMobileExtension.xcframework` - innehåller två binära fetter, en för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64, arm64).

      Denna XCFramwork ska vara länkad när den har ett iOS-tillägg som mål.

   * `AdobeMobileWatch.xcframework` - innehåller två binära fetter, en för watchOS-enheter (arm64_32, armv7k) och simulatorer (i386, x86_64, arm64).

      Denna XCFramwork ska vara länkad när en Apple Watch-app (watchOS) används som mål.

   * `AdobeMobileTV.xcframework` - innehåller två binära fetter, en för tvOS-enheter (arm64) och simulatorer (x86_64, arm64).

      Denna XCFramwork ska vara länkad när en Apple TV-app (tvOS) används som mål.

>[!IMPORTANT]
>
>I versioner som är äldre än 4.21.0 distribueras SDK via binärfiler. Om du använder en version som är äldre än 4.21.0 följer du stegen nedan.

1. Ladda ned, zippa upp `[Your_App_Name_]AdobeMobileLibrary-4.*-iOS.zip`-filen och kontrollera att du har följande programvarukomponenter:

   * `ADBMobile.h`, målfil C-huvudfilen som används för iOS AppMeasurement.
   * `ADBMobileConfig.json`, som är SDK-konfigurationsfilen som är anpassad för ditt program.
   * `AdobeMobileLibrary.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64).

      Denna feta binärfil bör länkas när målet är avsett för en iOS-app.

   * `AdobeMobileLibrary_Extension.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64).

      Denna binära fetthalt bör länkas när målet är avsett för ett iOS-tillägg.

   * `AdobeMobileLibrary_Watch.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för Apple Watch-enheter (armv7k) och simulatorer (i386, x86_64).

      Denna feta binärfil bör länkas när målet är avsett för en Apple Watch-tilläggsapp (watchOS 2).

   * `AdobeMobileLibrary_TV.a`, en bitkodsaktiverad binär fetthalt som innehåller biblioteksbyggen för nya Apple TV-enheter (arm64) och simulator (x86_64).

      Den här feta binärfilen ska länkas när målet är avsett för en Apple TV-app (tvOS).

>[!IMPORTANT]
>
>Om du hämtar SDK-filen utanför användargränssnittet för Adobe Mobile Services måste filen `ADBMobileConfig.json` konfigureras manuellt. Om du inte har använt Analytics tidigare och Mobile SDK tidigare läser du [Innan du börjar](/help/ios/getting-started/requirements.md) för att konfigurera en utvecklingsrapportsserie och hämta en förifylld version av konfigurationsfilen.

## Lägg till SDK och konfigurationsfilen i ditt projekt {#section_93C25D893B4A4CD3B996CF3C5590C8DC}

1. Starta Xcode IDE och öppna appen.
1. I projektnavigeraren drar du mappen `AdobeMobileLibrary` och släpper den under projektet.
1. Kontrollera följande:

   * Kryssrutan **[!UICONTROL Copy Items if needed]** är markerad.
   * **[!UICONTROL Create groups]** är markerat.
   * Ingen av kryssrutorna i avsnittet **[!UICONTROL Add to targets]** är markerad.

   ![](assets/step_3.png)

1. Klicka på **[!UICONTROL Finish]**.
1. I **[!UICONTROL Project Navigator]** väljer du **`ADBMobileConfig.json`**.
1. I **[!UICONTROL File Inspector]** lägger du till JSON-filen i alla mål i projektet som ska använda Adobe SDK.

   ![](assets/step_4.png)

1. Utför följande steg i **[!UICONTROL Project Navigator]**:

   1. Klicka på din app.
   1. På fliken **[!UICONTROL General]** väljer du dina mål och länkar de nödvändiga ramverken och biblioteken i avsnitten **[!UICONTROL Linked Frameworks]** och **[!UICONTROL Libraries]**.
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
   > Länkning av mer än en `AdobeMobileLibrary*.a`-fil i samma mål resulterar i oväntat beteende eller oförmåga att bygga.

   >[!IMPORTANT]
   >
   > Om du använder version 4.21.0 eller senare ska du se till att Adobe XCFrameworks inte bäddas in.

   ![](assets/no-embed.png)

1. Bekräfta att appen byggs utan fel.

## Implementera livscykelvärden {#section_532702562A7A43809407C9A2CBA80E1E}

>[!IMPORTANT]
>
>iOS skickar livscykelinformation med eller utan att anropa `collectlifecycledata`, och `collectlifecycledata` är bara ett sätt att initiera livscykeln tidigare i programmets startsekvens.

När du har aktiverat livscykeln skickas en träff varje gång appen startas för att mäta öppningar, uppgraderingar, sessioner, engagerade användare och andra [livscykelvärden](/help/ios/metrics.md).

Lägg till ett `collectLifecycleData`/ `collectLifecycleDataWithAdditionalData`-samtal i `application:didFinishLaunchingWithOptions`:

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
 [ADBMobile collectLifecycleData];
    return YES;
}
```

### Inkludera ytterligare data vid livscykelanrop

Använd `collectLifecycleDataWithAdditionalData` om du vill inkludera ytterligare data med livscykelmätanrop:

>[!IMPORTANT]
>
>Alla data som skickas till SDK via `collectLifecycleDataWithAdditionalData:` sparas i `NSUserDefaults` av SDK:n. SDK:n tar bort de värden i parametern `NSDictionary` som inte är av typen `NSString` eller `NSNumber`.

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSMutableDictionary *contextData = [NSMutableDictionary dictionary];
    [contextData setObject:@"Game" forKey:@"myapp.category"];
    [ADBMobile collectLifecycleDataWithAdditionalData:contextData];
    return YES;
}
```

Ytterligare kontextdatavärden som skickas med `collectLifecycleDataWithAdditionalData` måste mappas till anpassade variabler i Adobe Mobile-tjänster:

![](assets/map-variable-lifecycle.png)

Andra livscykelvärden samlas in automatiskt. Mer information finns i [Livscykelvärden](/help/ios/metrics.md).

## Vad ska du göra härnäst? {#section_A24DC703359D4B5C8F493D6421306FD3}

Utför följande uppgifter:

* [Spåra applägen](/help/ios/analytics-main/states.md)
* [Spåra appåtgärder](/help/ios/analytics-main/actions.md)
