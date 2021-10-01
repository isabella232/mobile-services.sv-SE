---
description: Den här informationen hjälper dig att migrera från 3.x- eller 2.x-versionen av Android-biblioteket till version 4.x.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Migrera till Android 4.x-biblioteket
topic-fix: Developer and implementation
uuid: 906e83bb-2faf-4aa2-ac9b-3fba6b833c7e
exl-id: 8061c1ab-aaaf-4d4c-9bd5-b2f80b6b06a3
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 2%

---

# Migrera till Android 4.x-biblioteket {#migrating-to-the-android-x-library}

Den här informationen hjälper dig att migrera från 3.x- eller 2.x-versionen av Android-biblioteket till version 4.x.

>[!IMPORTANT]
>
>SDK använder `SharedPreferences` för att lagra data som behövs för att beräkna unika användare, livscykelvärden och andra data relaterade till SDK-funktionaliteten.  Om du ändrar eller tar bort de värden i `SharedPreferences` som förväntas av SDK kan oväntade beteenden resultera i inkonsekvenser i data.

I version 4.x-biblioteket konsolideras de publika metoderna i en rubrik. Dessutom är alla funktioner nu tillgängliga via metoder på klassnivå, så du behöver inte hålla reda på pekare, instanser eller singletoner.

## Event, props och eVars {#section_76EA6F5611184C5CAE6E62956D84D7B6}

I version 4 kan du inte längre tilldela variabler som händelser, eVars, props, heirs och lists i din app. I stället använder SDK kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna har följande fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till App Store.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data.

   Dessa värden visas inte i rapporter förrän de mappas med bearbetningsregler.

>[!TIP]
>
>Värden som du tilldelade direkt till variabler ska läggas till i HashMap-filen `data`.

## Ta bort oanvända egenskaper {#section_145222EAA20F4CC2977DD883FDDBBFC5}

Den nya `ADBMobileConfig.json`-filen innehåller programspecifika, globala inställningar och ersätter de flesta konfigurationsvariabler som användes i tidigare versioner. Här är ett exempel på en `ADBMobileConfig.json`-fil:

```js
{
    "version" : "1.0",
    "analytics" : {
        "rsids" : "coolApp",
        "server" : "my.CoolApp.com",
        "charset" : "UTF-8",
        "ssl" : true,
        "offlineEnabled" : true,
        "lifecycleTimeout" : 5,
        "privacyDefault" : "optedin",
        "poi" : [
                    ["san francisco",37.757144,-122.44812,7000],
                    ["santa cruz",36.972935,-122.01725,600]
                ]
    },
 "target" : {
  "clientCode" : "myTargetClientCode",
  "timeout" : 5
 },
 "audienceManager" : {
  "server" : "myServer.demdex.com"
 }
}
```

## Flytta konfigurationsfilen och migrera till version 4 {#section_0B844235E0B04DD4B36976A73DB28FB5}

I följande tabeller visas de konfigurationsvariabler som du behöver flytta till konfigurationsfilen.

### Flytta konfigurationsfilen

1. Flytta värdet som är angivet för variabeln i den första kolumnen till variabeln i den andra kolumnen.
1. Ta bort den gamla konfigurationsvariabeln från koden.

### Migrerar från version 3.x

Flytta konfigurationsvariabeln/metodvärdet till variabeln `ADBMobileConfig.json` om du vill migrera från version 3.x till 4.

| Konfigurationsvariabel eller -metod | Variabel i `ADBMobileConfig.json`-filen |
|--- |--- |
| setOfflineTrackingEnabled | &quot;offlineEnabled&quot; |
| setOfflineHitLimit | &quot;batchLimit&quot; |
| reportSuiteIDs | &quot;rsids&quot; |
| trackingServer | &quot;server&quot; |
| charSet | &quot;charset&quot; |
| currencyCode | &quot;currency&quot; |
| ssl | &quot;ssl&quot; |
| linkTrackVars | Ta bort, används inte längre. |
| linkTrackEvents | Ta bort, används inte längre. |

### Migrerar från version 2.x

Om du vill migrera från version 2.x till version 4 flyttar du värdet från den första kolumnen till variabeln i den andra kolumnen.

| Konfigurationsvariabel | Variabel i `ADBMobileConfig.json`-filen |
| --- |--- |
| trackOffline | &quot;offlineEnabled&quot; |
| offlineLimit | &quot;batchLimit&quot; |
| konto | &quot;rsids&quot; |
| trackingServer | &quot;server&quot; tar du bort prefixet `"https://"`. Protokollprefixet läggs till automatiskt baserat på inställningen &quot;ssl&quot;. |
| trackingServerSecure | Ta bort. För säkra anslutningar definierar du&quot;server&quot; och aktiverar sedan&quot;ssl&quot;. |
| charSet | &quot;charset&quot; |
| currencyCode | &quot;currency&quot; |
| ssl | &quot;ssl&quot; |
| linkTrackVars | Ta bort, används inte längre. |
| linkTrackEvents | Ta bort, används inte längre. |
| tidsstämpel | Ta bort, inte längre konfigurerbar. |
| dc | Ta bort, används inte längre. |
| userAgent | Ta bort, inte längre konfigurerbar. |
| dynamicVariablePrefix | Ta bort, används inte längre. |
| visitorNamespace | Ta bort, används inte längre. |
| usePlugins | Ta bort, används inte längre. |
| useBestPractices alla anrop för att ändra mått (getChurnInstance) | Ta bort, ersätt med Lifecycle Metrics. |

## Uppdatera spårningsanrop och spårningsvariabler {#section_96E7D9B3CDAC444789503B7E7F139AB9}

I stället för att använda de webbfokuserade `track`- och `trackLink`-anropen använder version 4 SDK följande metoder:

* `trackState`, som är de vyer som är tillgängliga i din app, till exempel  `home dashboard`,  `app settings`,  `cart`och så vidare.

   Dessa lägen liknar sidor på en webbplats och `trackState` anropar stegvisa sidvyer.

* `trackAction` åtgärder, som  `logons`,  `banner taps`,  `feed subscriptions`och så vidare, som inträffar i appen och som du vill mäta.

Parametern `contextData` för båda dessa metoder är `HashMap<String, Object>`, som innehåller namnvärdespar som skickas som kontextdata.

## Event, props och eVars

I version 4 kan du inte längre tilldela variabler som händelser, eVars, props, heirs och lists direkt i appen. SDK använder nu kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna har följande fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till appbutiken.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data.

   Dessa värden visas inte i rapporter förrän de mappas med bearbetningsregler. Mer information finns i [Bearbetningsregler och kontextdata](/help/android/getting-started/proc-rules.md).

Värden som du tilldelade direkt till variabler ska läggas till i HashMap-filen `data`. Det innebär att anrop till `setProp`, `setEvar` och tilldelningar till beständiga kontextdata ska tas bort och värdena läggas till i parametern `data`.

## AppSection/server, GeoZip, transaktions-ID, Campaign och andra standardvariabler

Data som du angav för måttobjektet, inklusive variablerna ovan, ska läggas till i HashMap-filen `data`. De enda data som skickas med ett `trackState`- eller `trackAction`-anrop är nyttolasten i parametern `data`.

### Ersätt spårningsanrop

Ersätt följande metoder med ett anrop till `trackState` eller `trackAction`:

* **Migrerar från version 3.x**

   * `trackAppState (trackState)`
   * `trackEvents (trackAction)`
   * `track (trackAction)`
   * `trackLinkURL (trackAction)`

* **Migrerar från version 2.x**

   * `track (trackState)`
   * `trackLink (trackAction)`

## Anpassat besökar-ID {#section_2CF930C13BA64F04959846E578B608F3}

Ersätt variabeln `visitorID` med ett anrop till `setUserIdentifier`.

## Spårning offline {#section_5D4CD8CD1BE041A79A8657E31C0D24C6}

Spårning offline är aktiverat i `ADBMobileConfig.json`-filen och all annan offlinekonfiguration görs automatiskt.

Ta bort anrop till följande metoder:

**Version 3.x**

* `setOnline`
* `setOffline`

**Version 2.x**

* `forceOffline`
* `forceOnline`

## Variabeln Produkter {#section_AFBA36F3718C44D29AF81B9E1056A1B4}

Mer information om variabeln products finns i [Produktvariabeln](/help/android/analytics-main/products/products.md).
