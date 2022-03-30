---
description: I det här avsnittet beskrivs hur du migrerar från 3.x-versionen av en tidigare Windows Mobile SDK till Universal Windows Platform 4.x SDK för Experience Cloud-lösningar.
solution: Experience Cloud Services,Analytics
title: Migrera till 4.x
topic-fix: Developer and implementation
uuid: bdd6c5cd-3892-4e99-b69e-77105ad66e25
exl-id: 68de505b-dcff-4a78-9f01-b1d103846281
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Migrera till 4.x SDK:er{#migrate-to-x}

I det här avsnittet beskrivs hur du migrerar från 3.x-versionen av Windows Mobile SDK till Universal Windows Platform 4.x SDK för Experience Cloud-lösningar.

I och med övergången till version 4.x är alla funktioner nu tillgängliga via statiska metoder. Du behöver inte längre hålla reda på dina egna objekt.

I följande avsnitt får du hjälp med att migrera från version 3.x till version 4.x.

## Ta bort oanvända egenskaper {#section_145222EAA20F4CC2977DD883FDDBBFC5}

Du märkte antagligen en ny `ADBMobileConfig.json` som ingår i nedladdningen. Den här filen innehåller programspecifika, globala inställningar och ersätter de flesta konfigurationsvariabler som användes i tidigare versioner.

Här är ett exempel på en `ADBMobileConfig.json` fil:

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

### Migrerar från 3.x

Följande tabell innehåller en lista med variabler i SDK:erna för 3.x och det nya namnet i SDK:erna för 4.x:

| Konfigurationsvariabel/metod | Variabel i `ADBMobileConfig.json` -fil. |
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

Istället för att använda det webbfokuserade `Track` och `TrackLink` anropar, version 4 SDK använder två metoder som är lite mer logiska i mobilvärlden:

* `TrackState` Lägen är de vyer som är tillgängliga i din app, till exempel&quot;heminstrumentpanel&quot;,&quot;appinställningar&quot;,&quot;kundvagn&quot; och så vidare. Dessa lägen liknar sidor på en webbplats, och `trackState` anropar stegvisa sidvyer.

* `TrackAction` Åtgärder är det som händer i appen som du vill mäta, till exempel&quot;inloggningar&quot;,&quot;banderollknappar&quot;,&quot;flödesprenumerationer&quot; och andra mätvärden. Dessa anrop ökar inte sidvyerna.

The `contextData` parametern för båda dessa metoder innehåller namnvärdespar som skickas som kontextdata.

### Event, props, eVars

Om du har tittat på [SDK-metoder](/help/universal-windows/c-configuration/methods.md), undrar du antagligen var du ska sätta händelser, eVars, props, heirs och lists. I version 4 kan du inte längre tilldela dessa typer av variabler direkt i appen. I stället använder SDK kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna har följande fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till App Store.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data. Dessa värden visas inte i rapporter förrän de mappas med bearbetningsregler.

Mer information finns i *Bearbetar regler* avsnitt i [Analytics - översikt](/help/universal-windows/analytics/analytics.md).

Alla värden som du tilldelade direkt till variabler bör läggas till i kontextdata i stället. Detta innebär att anropar `SetProp`, `SetEvar`och tilldelningar till beständiga kontextdata ska tas bort och värdena läggas till i kontextdata.

### AppSection/Server, GeoZip, transaktions-ID, Campaign och andra standardvariabler

Alla andra data som du angav för mätningsobjektet, inklusive variablerna ovan, ska läggas till i kontextdata i stället. Det vill säga, den enda informationen som skickas in med `TrackState` eller `TrackAction` anropet är nyttolasten i `data` parameter.

**Ersätt spårningsanrop**

Ersätt följande metoder i hela koden med ett anrop till `trackState` eller `trackAction`:

**Migrerar från 3.x:**

* TrackAppState (TrackState)
* TrackEvents (TrackAction)
* Track (TrackAction)
* TrackLinkURL (TrackAction)

## Tjänst för anpassat ID {#section_2CF930C13BA64F04959846E578B608F3}

Ersätt `visitorID` variabel med ett anrop till `setUserIdentifier`.

## Spårning offline {#section_5D4CD8CD1BE041A79A8657E31C0D24C6}

Spårning offline är aktiverat i `ADBMobileConfig.json` -fil. All annan offlinekonfiguration görs automatiskt.

Ta bort anrop till följande metoder i hela koden:

**Migrerar från 3.x:**

* SetOnline
* SetOffline

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

Värdet för `"&&products"` (i det här exemplet är värdet `";Cool Shoe`&quot;) ska följa produktsträngssyntaxen för den typ av händelse som du spårar.
