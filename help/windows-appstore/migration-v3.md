---
description: I det här avsnittet beskrivs hur du migrerar från 3.x-versionen av en tidigare Windows Mobile SDK till Windows 8.1 Universal App Store 4.x SDK för Experience Cloud-lösningar.
seo-description: I det här avsnittet beskrivs hur du migrerar från 3.x-versionen av en tidigare Windows Mobile SDK till Windows 8.1 Universal App Store 4.x SDK för Experience Cloud-lösningar.
seo-title: Migrera till 4.x SDK:er
solution: Experience Cloud,Analytics
title: Migrera till 4.x SDK:er
topic: Developer and implementation
uuid: e0fe3b7b-cda5-4a91-834c-2c7e17a501a3
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---


# Migrera till 4.x SDK:er {#migrate-to-the-x-sdks}

I det här avsnittet beskrivs hur du migrerar från 3.x-versionen av en tidigare Windows Mobile SDK till Windows 8.1 Universal App Store 4.x SDK för Experience Cloud-lösningar.

I och med övergången till version 4.x är alla funktioner nu tillgängliga via statiska metoder, så att du slipper hålla reda på dina egna objekt.

I följande avsnitt får du hjälp med att migrera från version 3.x till version 4.x.

## Ta bort oanvända egenskaper {#section_145222EAA20F4CC2977DD883FDDBBFC5}

En ny `ADBMobileConfig.json` fil finns förmodligen med i nedladdningen. Den här filen innehåller programspecifika, globala inställningar och ersätter de flesta konfigurationsvariabler som användes i tidigare versioner. Här är ett exempel på en `ADBMobileConfig.json` fil:

```js
{ 
    "version" : "1.0", 
    "analytics" : { 
        "rsids" : "coolApp", 
        "server" : "my.CoolApp.com", 
        "charset" : "UTF-8", 
        "ssl" : true, 
        "offlineEnabled" : true, 
        "lifecycleTimeout" : 300, 
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

I följande tabeller visas de konfigurationsvariabler som du behöver flytta till konfigurationsfilen. Flytta värdeuppsättningen för variabeln i den första kolumnen till variabeln i den andra kolumnen och ta sedan bort den gamla variabeln från koden.

## Migrerar från 3.x

| Konfigurationsvariabel/metod | Variabel i `ADBMobileConfig.json` filen. |
|--- |--- |
| offlineTrackingEnabled | &quot;offlineEnabled&quot; |
| reportSuiteIDs | &quot;rsids&quot; |
| trackingServer | &quot;server&quot; |
| charSet | &quot;charset&quot; |
| currencyCode | &quot;currency&quot; |
| ssl | &quot;ssl&quot; |
| setOfflineHitLimit | Ta bort, används inte längre. |
| linkTrackVars | Ta bort, används inte längre. |
| linkTrackEvents | Ta bort, används inte längre. |

## Uppdatera spårningsanrop och spårningsvariabler {#section_96E7D9B3CDAC444789503B7E7F139AB9}

I stället för att använda det webbfokuserade `Track` och `TrackLink` anropet använder version 4 SDK två metoder som är lite mer användbara i mobilvärlden:

* `TrackState` Lägen är de vyer som är tillgängliga i din app, till exempel&quot;heminstrumentpanel&quot;,&quot;appinställningar&quot;,&quot;kundvagn&quot; och så vidare. Dessa lägen liknar sidor på en webbplats och anropar `trackState` stegvisa sidvyer.

* `TrackAction` Åtgärder är det som händer i appen som du vill mäta, till exempel&quot;inloggningar&quot;,&quot;banderollknappar&quot;,&quot;flödesprenumerationer&quot; och andra mätvärden. Dessa anrop ökar inte sidvyerna.

Parametern `contextData` för båda dessa metoder innehåller namnvärdespar som skickas som kontextdata.

## Evenemang, utkast, eVars

Om du har tittat på [SDK-metoderna](/help/windows-appstore/c-configuration/methods.md)undrar du antagligen var du ska sätta händelser, eVars, props, heirs och lists. I version 4 kan du inte längre tilldela dessa typer av variabler direkt i appen. I stället använder SDK kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna ger dig flera fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till App Store.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data. Dessa värden visas inte i rapporter förrän de mappas med bearbetningsregler.

Mer information finns i *Bearbetningsregler* i [Analytics](/help/windows-appstore/analytics/analytics.md).

Alla värden som du tilldelade direkt till variabler bör läggas till i kontextdata i stället. Detta innebär att anrop till `SetProp`, `SetEvar`och tilldelningar till beständiga kontextdata ska tas bort och värdena läggas till i kontextdata.

**AppSection/Server, GeoZip, Transaction ID, Campaign och andra standardvariabler**

Alla andra data som du angav för mätningsobjektet, inklusive variablerna ovan, ska läggas till i kontextdata i stället.

Enkelt uttryckt är den enda data som skickas in med ett `TrackState` eller `TrackAction` anrop nyttolasten i `data` parametern.

### Ersätt spårningsanrop

Ersätt följande metoder i hela koden med ett anrop till `trackState` eller `trackAction`:

### Migrerar från 3.x

* `TrackAppState` (TrackState)
* `TrackEvents` (TrackAction)
* `Track` (TrackAction)
* `TrackLinkURL` (TrackAction)

## Custom visitor ID {#section_2CF930C13BA64F04959846E578B608F3}

Ersätt `visitorID` variabeln med ett anrop till `setUserIdentifier`.

## Spårning offline {#section_5D4CD8CD1BE041A79A8657E31C0D24C6}

Spårning offline är aktiverat i `ADBMobileConfig.json` filen. All annan offlinekonfiguration görs automatiskt.

Ta bort anrop till följande metoder i hela koden:

### Migrerar från 3.x

* `SetOnline`
* `SetOffline`

## Variabeln Produkter {#section_AFBA36F3718C44D29AF81B9E1056A1B4}

Eftersom variabeln products inte är tillgänglig i bearbetningsregler kan du använda följande syntax för att ange `products`:

```js
// create a processing rule to set the corresponding product event. 
// for example, set the Product Views event when context data a.action = "product view" 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
cdata["&&products"] = ";Cool Shoe"; 
ADB.Analytics.trackAction("product view", cdata);
```

![](assets/prod-view.png)

I det här exemplet `"&&products"` är värdet `";Cool Shoe`&quot; och ska följa produktsträngssyntaxen för den typ av händelse som du spårar.