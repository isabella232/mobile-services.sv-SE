---
description: Den här informationen hjälper dig att migrera från version 3.x eller 2.x av iOS-biblioteket till version 4.x.
solution: Experience Cloud Services,Analytics
title: Migrera till iOS 4.x-biblioteket
topic-fix: Developer and implementation
uuid: 5668972b-f355-4e03-9df0-8c82ddf6809b
exl-id: a58067e0-b6f4-4900-ba3f-7256d9259420
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 2%

---

# Migrera till iOS 4.x-biblioteket{#migrating-to-the-x-ios-library}

Den här informationen hjälper dig att migrera från version 3.x eller 2.x av iOS-biblioteket till version 4.x.

>[!IMPORTANT]
>
>SDK använder `NSUserDefaults` lagra data som behövs för att beräkna unika användare, livscykelvärden och andra data som rör SDK-funktionaliteten.  Om du ändrar eller tar bort värdena i `NSUserDefaults` som förväntas av SDK kan oväntade beteenden resultera i inkonsekvenser i data.

I version 4.x av iOS SDK-biblioteket konsolideras de publika metoderna till en rubrik. Funktionen är nu även tillgänglig via metoder på klassnivå, så du behöver inte hålla reda på pekare, instanser eller singletoner.

## Event, props och eVars {#section_76EA6F5611184C5CAE6E62956D84D7B6}

I version 4 kan du inte längre tilldela variabler som händelser, eVars, props, heirs och lists direkt i appen. I stället använder SDK kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna har följande fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till App Store.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data.

   Dessa värden visas inte i rapporter förrän de mappas med bearbetningsregler.

>[!TIP]
>
>Värden som du tilldelade direkt till variabler bör nu läggas till i `data` NSDictionary.

## Ta bort oanvända egenskaper {#section_145222EAA20F4CC2977DD883FDDBBFC5}

Den nya `ADBMobileConfig.json` filen innehåller programspecifika, globala inställningar och ersätter de flesta konfigurationsvariabler som användes i tidigare versioner. Här är ett exempel på en `ADBMobileConfig.json` fil:

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


### Flytta konfigurationsfilen

Så här flyttar du konfigurationsfilen:

1. Flytta värdet som är angivet för variabeln i den första kolumnen till variabeln i den andra kolumnen.
1. Ta bort den gamla konfigurationsvariabeln från koden.

### Migreringsinformation

I följande tabeller visas de konfigurationsvariabler som du behöver flytta till konfigurationsfilen.

#### Migrerar från version 3.x

Flytta värdet från den första kolumnen till variabeln i den andra kolumnen.

| Konfigurationsvariabel | Variabel i `ADBMobileConfig.json` fil |
|--- |--- |
| offlineTrackingEnabled | &quot;offlineEnabled&quot; |
| offlineHitLimit | &quot;batchLimit&quot; |
| reportSuiteIDs | &quot;rsids&quot; |
| trackingServer | &quot;server&quot; |
| charSet | &quot;charset&quot; |
| currencyCode | &quot;currency&quot; |
| ssl | &quot;ssl&quot; |
| linkTrackVars | Ta bort, används inte längre. |
| linkTrackEvents | Ta bort, används inte längre. |


#### Migrerar från version 2.x

Flytta värdet från den första kolumnen till variabeln i den andra kolumnen.

| Konfigurationsvariabel | Variabel i `ADBMobileConfig.json` fil |
|--- |--- |
| trackOffline | &quot;offlineEnabled&quot; |
| offlineLimit | &quot;batchLimit&quot; |
| konto | &quot;rsids&quot; |
| trackingServer | &quot;server&quot;, ta bort `"https://"` prefix. Protokollprefixet läggs till automatiskt baserat på inställningen &quot;ssl&quot;. |
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
| useBestPractices alla anrop för att ändra mått ( getChurnInstance ) | Ta bort, ersätt med livscykelvärden. Mer information finns i [Livscykelvärden](/help/ios/metrics.md). |


## Uppdatera spårningsanrop och spårningsvariabler {#section_96E7D9B3CDAC444789503B7E7F139AB9}

Istället för att använda det webbfokuserade `track` och `trackLink` anrop använder version 4 SDK följande metoder:

* `trackState:data:` är de vyer som är tillgängliga i din app, till exempel `home dashboard`, `app settings`, `cart`och så vidare.

   Dessa lägen liknar sidor på en webbplats, och `trackState` anropar stegvisa sidvyer.

* `trackAction:data:` åtgärder, till exempel `logons`, `banner taps`, `feed subscriptions`och andra mätvärden som finns i appen och som du vill mäta.

The `data` parametern för båda dessa metoder är en `NSDictionary` som innehåller namnvärdespar som skickas som kontextdata.

### Event, props, eVars

I version 4 kan du inte längre tilldela variabler som händelser, eVars, props, heirs och lists direkt i appen. SDK använder nu kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna har följande fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till App Store.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data.

   Dessa värden visas inte i rapporter förrän de har mappats med bearbetningsregler. Mer information finns i [Bearbetar regler och kontextdata](/help/ios/getting-started/proc-rules.md).

Värden som du tilldelade direkt till variabler ska läggas till i `data` `NSDictionary` i stället. Detta innebär att anropar `setProp`, `setEvar`och tilldelningar till beständiga kontextdata ska tas bort och värdena läggas till i `data` parameter.

### AppSection/Server, GeoZip, transaktions-ID, Campaign och andra standardvariabler

Data som du angav för måttobjektet, inklusive variablerna ovan, ska läggas till i `data` `NSDictionary` i stället. De enda data som skickas med en `trackState` eller `trackAction` anropet är nyttolasten i `data` parameter.

### Ersätt spårningsanrop

Ersätt följande metoder i koden med ett anrop till `trackState` eller `trackAction`:

#### Migrerar från version 3.x

* `trackAppState (trackState)`
* `trackEvents (trackAction)`
* `track (trackAction)`
* `trackWithContextData (trackAction)`
* `trackLinkURL (trackAction)`

#### Migrerar från version 2.x

* `track (trackState)`
* `trackLink (trackAction)`

## Anpassat besökar-ID {#section_2CF930C13BA64F04959846E578B608F3}

Ersätt `visitorID` variabel med ett anrop till `setUserIdentifier:`.

## Spårning offline {#section_5D4CD8CD1BE041A79A8657E31C0D24C6}

Spårning offline är aktiverat i `ADBMobileConfig.json` och all annan offlinekonfiguration görs automatiskt.

Ta bort anrop till följande metoder i koden:

### Version 3.x

* `setOnline`
* `setOffline`

### Version 2.x

* `forceOffline`
* `forceOnline`

## Variabeln Produkter {#section_AFBA36F3718C44D29AF81B9E1056A1B4}

Eftersom variabeln products inte är tillgänglig i bearbetningsregler kan du använda följande syntax för att ange `products`:

```objective-c
//create a processing rule to set the corresponding product event. 
// for example, set prodView event when context data a.action = "product view" 
[ADBMobile trackAction:@"LikeButtonClicked"  
                  data:@{@"&&products" : @";Cool Shoe"}];
```

![](assets/prod-view.png)
