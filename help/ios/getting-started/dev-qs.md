---
description: Denna information hjälper er att implementera iOS-biblioteket och samla in livscykeldata som starter, uppgraderingar, sessioner, engagerade användare osv.
solution: Experience Cloud Services,Analytics
title: Kärnimplementering och livscykel
topic-fix: Developer and implementation
uuid: 96d06325-e424-4770-8659-4b5431318ee3
exl-id: 5fb2d534-c2e8-480a-aaee-0e71dd55feb6
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Kärnimplementering och livscykel {#core-implementation-and-lifecycle}

Denna information hjälper er att implementera iOS-biblioteket och samla in livscykeldata som starter, uppgraderingar, sessioner, engagerade användare osv.

## Ladda ned SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

>[!IMPORTANT]
>
>SDK kräver iOS 8 eller senare.

**Förutsättning**

Innan du laddar ned SDK, slutför du stegen i *Skapa en rapportsvit* in [Kärnimplementering och livscykel](/help/ios/getting-started/requirements.md) för att konfigurera en utvecklingsrapportsserie och hämta en förifylld version av konfigurationsfilen.

Så här hämtar du SDK:

>[!IMPORTANT]
>
>Från och med version 4.21.0 distribueras SDK via XCFrameworks. Följ stegen nedan om du använder 4.21.0 eller senare.
>
>Version 4.21.0 av SDK kräver Xcode 12.0 eller senare och, om tillämpligt, Cocoapods 1.10.0 eller senare.

1. Ladda ned, zippa upp `[Your_App_Name_]AdobeMobileLibrary-4.*-iOS.zip` och verifiera att du har följande programkomponenter i `AdobeMobileLibrary` katalog:

   * `ADBMobile.h` - målfil C som används för iOS SDK.
   * `ADBMobileConfig.json` - SDK-konfigurationsfilen som är anpassad för din app.
   * `AdobeMobile.xcframework` - innehåller två binära fetter, en för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64, arm64).

      Denna XCFramwork ska vara länkad när en iOS-app används.

   * `AdobeMobileExtension.xcframework` - innehåller två binära fetter, en för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64, arm64).

      Denna XCFramwork ska vara länkad när den riktar sig mot ett iOS-tillägg.

   * `AdobeMobileWatch.xcframework` - innehåller två binära fetter, en för watchOS-enheter (arm64_32, armv7k) och simulatorer (i386, x86_64, arm64).

      Denna XCFramwork ska vara länkad när en Apple Watch-app (watchOS) används.

   * `AdobeMobileTV.xcframework` - innehåller två binära fetter, en för tvOS-enheter (arm64) och simulatorer (x86_64, arm64).

      Denna XCFramwork ska vara länkad när en Apple TV-app (tvOS) används som mål.

>[!IMPORTANT]
>
>I versioner som är äldre än 4.21.0 distribueras SDK via binärfiler. Om du använder en version som är äldre än 4.21.0 följer du stegen nedan.

1. Ladda ned, zippa upp `[Your_App_Name_]AdobeMobileLibrary-4.*-iOS.zip` och verifiera att du har följande programvarukomponenter:

   * `ADBMobile.h`, målfil C-huvudfilen som används för iOS AppMeasurement.
   * `ADBMobileConfig.json`, som är SDK-konfigurationsfilen som är anpassad för ditt program.
   * `AdobeMobileLibrary.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64).

      Denna feta binärfil bör länkas när målet är avsett för en iOS-app.

   * `AdobeMobileLibrary_Extension.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386, x86_64).

      Denna binära fetthalt skall kopplas när målet är avsett för en iOS- förlängning.

   * `AdobeMobileLibrary_Watch.a`, en bitkodsaktiverad binärfil som innehåller biblioteksbyggen för Apple Watch-enheter (armv7k) och simulatorer (i386, x86_64).

      Denna feta binärfil bör länkas när målet är avsett för en tilläggsapp för Apple Watch (watchOS 2).

   * `AdobeMobileLibrary_TV.a`, en bitkodsaktiverad binär fetthalt som innehåller biblioteket för nya Apple TV-enheter (arm64) och simulator (x86_64).

      Den här feta binärfilen ska länkas när målet är avsett för en app i Apple TV (tvOS).

>[!IMPORTANT]
>
>Om du laddar ned SDK utanför användargränssnittet för Mobile-tjänster i Adobe, `ADBMobileConfig.json` filen måste konfigureras manuellt. Om du inte har använt Analytics tidigare eller Mobile SDK tidigare kan du läsa [Innan du börjar](/help/ios/getting-started/requirements.md) för att konfigurera en utvecklingsrapportsserie och hämta en förifylld version av konfigurationsfilen.

## Lägg till SDK och konfigurationsfilen i ditt projekt {#section_93C25D893B4A4CD3B996CF3C5590C8DC}

1. Starta Xcode IDE och öppna appen.
1. Dra i projektnavigeraren `AdobeMobileLibrary` och släpp den under projektet.
1. Kontrollera följande:

   * The **[!UICONTROL Copy Items if needed]** är markerad.
   * **[!UICONTROL Create groups]** är markerat.
   * Ingen av kryssrutorna i **[!UICONTROL Add to targets]** -avsnittet är markerat.

   ![](assets/step_3.png)

1. Klicka på **[!UICONTROL Finish]**.
1. I **[!UICONTROL Project Navigator]** väljer du **`ADBMobileConfig.json`**.
1. I **[!UICONTROL File Inspector]** lägger du till JSON-filen i alla mål i projektet som ska använda Adobe SDK.

   ![](assets/step_4.png)

1. I **[!UICONTROL Project Navigator]** utför du följande steg:

   1. Klicka på din app.
   1. På **[!UICONTROL General]** väljer du dina mål och länkar de nödvändiga ramverken och biblioteken i **[!UICONTROL Linked Frameworks]** och **[!UICONTROL Libraries]** -avsnitt.
   * **iOS App Targets**
      * `SystemConfiguration.framework`
      * `WebKit.framework`
      * `libsqlite3.0.tbd`
      * `AdobeMobileLibrary.a`
      * `CoreLocation.framework` (valfritt, men krävs för geospårning)
   * **iOS Extension Target**

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
   > Länka mer än en `AdobeMobileLibrary*.a` -filen i samma mål kommer att resultera i oväntat beteende eller oförmåga att bygga.

   >[!IMPORTANT]
   >
   > Om du använder version 4.21.0 eller senare ska du se till att Adobe XCFrameworks inte bäddas in.

   ![](assets/no-embed.png)

1. Bekräfta att appen byggs utan fel.

## Implementera livscykelvärden {#section_532702562A7A43809407C9A2CBA80E1E}

>[!IMPORTANT]
>
>iOS skickar livscykelinformation med eller utan att ringa `collectlifecycledata`och `collectlifecycledata` är bara ett sätt att initiera livscykeln tidigare i programmets startsekvens.

När du har aktiverat livscykeln skickas en träff varje gång appen startas för att mäta öppningar, uppgraderingar, sessioner, engagerade användare och andra [Livscykelvärden](/help/ios/metrics.md).

Lägg till en `collectLifecycleData`/ `collectLifecycleDataWithAdditionalData` ring in `application:didFinishLaunchingWithOptions`:

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
>Alla data som skickas till SDK via `collectLifecycleDataWithAdditionalData:` bevaras i `NSUserDefaults` av SDK. SDK:n rensar värdena i `NSDictionary` parameter som inte är `NSString` eller `NSNumber` typer.

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
