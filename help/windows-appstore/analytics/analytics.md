---
description: 'null'
seo-description: 'null'
seo-title: Analyser
solution: Marketing Cloud,Analytics
title: Analyser
topic: Developer and implementation
uuid: fa0ef6c4-c04d-4695-9eb4-ada4e9920e6c
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Analyser {#analytics}

När du har lagt till biblioteket i ditt projekt kan du göra alla anrop till Analytics-metoden var som helst i din app.

>[!TIP]
>
>Se till att du importerar `ADBMobile.h` till klassen.

## Aktivera mobilappsrapporter i Analytics {#section_F2F9234009184F20BA36B5CDE872B424}

Innan du lägger till kod bör du be Analytics Administrator att slutföra följande för att aktivera livscykelspårning för mobilappar. Detta garanterar att rapportsviten är redo att samla in mätvärden när ni börjar utveckla.

1. Öppna **[!UICONTROL Admin Tools]** > **[!UICONTROL Report Suites]** och välj en eller flera mobila rapportsviter.
1. Klicka på **[!UICONTROL Edit Settings]** > **[!UICONTROL Mobile Management]** > **[!UICONTROL Mobile Application Reporting]**.

   ![](assets/mobile-settings.png)

1. Klicka på **[!UICONTROL Enable Latest App Reports]**.

   Du kan också klicka **[!UICONTROL Enable Mobile Location Tracking]** och **[!UICONTROL Enable Legacy Reporting and Attribution for background hits]**.

   ![](assets/enable-lifecycle.png)

Livscykelmätvärden är nu klara att hämtas och Mobile Application Reports visas på **[!UICONTROL Reports]** menyn i gränssnittet för marknadsföringsrapporter.


### Nya versioner

Nya versioner av rapporter om mobilapplikationer släpps regelbundet. Nya versioner används inte automatiskt i din rapportsserie. Du måste upprepa de här stegen för att kunna genomföra uppgraderingen. Varje gång du lägger till nya Experience Cloud-funktioner i ditt program rekommenderar vi att du upprepar de här stegen för att se till att du har den senaste konfigurationen.


## Livscykelstatistik {#section_532702562A7A43809407C9A2CBA80E1E}

Om du vill samla in livscykelvärden i din app lägger du till anrop till när programmet aktiveras, vilket visas i följande exempel.


### WinJS i default.js


```js
app.onactivated = function (args) { 
  if (args.detail.kind === activation.ActivationKind.launch) { 
   ... 
   // launched and resumed stuff  
   ADBMobile.Config.collectLifecycleData(); 
  } 
}; 
app.oncheckpoint = function (args) { 
  ADBMobile.Config.pauseCollectingLifecycleData(); 
}
```

### C# i App.xaml.cs

```js
public App() 
{ 
    this.InitializeComponent(); 
    this.Resuming *= OnResuming; 
    this.Suspending *= OnSuspending; 
} 
protected override void OnLaunched(LaunchActivatedEventArgs e) 
{ 
    ... 
    ADBMobile.Config.CollectLifecycleData(); 
    ... 
} 
private void OnResuming(object sender, object e) 
{ 
    ... 
    ADBMobile.Config.CollectLifecycleData(); 
    ... 
} 
private void OnSuspending(object sender, SuspendingEventArgs e) 
{ 
    ... 
    ADBMobile.Config.PauseCollectingLifecycleData(); 
    ... 
}
```

### C/CX i App.xaml.cpp

```js
App::App() 
{ 
 InitializeComponent(); 
 Resuming *= ref new EventHandler<Object ^>(this, &App::OnResuming); 
 Suspending *= ref new SuspendingEventHandler(this, &App::OnSuspending); 
} 
void App::OnResuming(Object ^sender, Object ^args) 
{ 
 ... 
 ADBMobile::Config::CollectLifecycleData(); 
 ... 
} 
void App::OnSuspending(Object^ sender, SuspendingEventArgs^ e) 
{ 
 ... 
 ADBMobile::Config::PauseCollectingLifecycleData(); 
 ... 
} 
void App::OnLaunched(Windows::ApplicationModel::Activation::LaunchActivatedEventArgs^ e) 
{ 
 ... 
 ADBMobile::Config::CollectLifecycleData(); 
 ... 
}
```

Om `CollectLifecycleData()` anropas två gånger under samma session kommer programmet att rapportera en krasch vid varje samtal efter det första. SDK anger en flagga när programmet stängs som anger att det har avslutats. Om flaggan inte är inställd rapporterar en krasch `CollectLifecyleData()` .


## Event, props och eVars {#section_76EA6F5611184C5CAE6E62956D84D7B6}


Om du har tittat på [ADBMomobile Class och Method Reference](/help/windows-appstore/c-configuration/methods.md)undrar du antagligen var du ska ange händelser, eVars, props, heirs och lists. I version 4 kan du inte längre tilldela dessa typer av variabler direkt i appen. I stället använder SDK kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna ger dig flera fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till App Store.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data. Dessa värden visas inte i rapporter förrän de mappas med bearbetningsregler.

Alla värden som du tilldelade direkt till variabler bör läggas till i kontextdata i stället.


## Bearbetar regler {#section_66EE762EEA5E4728864166201617DEBF}

Bearbetningsregler används för att kopiera data som du skickar i kontextdatavariabler till variabler, props och andra variabler för rapportering.

[Utbildning](https://tv.adobe.com/embed/1181/16506/) i bearbetningsregler på Summit 2013

[Översikt över bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html)

[Bli behörig att använda bearbetningsregler](https://helpx.adobe.com/analytics/kb/processing-rules-authorization.html)

Vi rekommenderar att du grupperar dina kontextdatavariabler med&quot;namnutrymmen&quot;, eftersom det hjälper dig att behålla den logiska ordningen. Om du till exempel vill samla in information om en produkt kan du definiera följande variabler:

```js
"product.type":"hat" 
"product.team":"mariners" 
"product.color":"blue"
```

Sammanhangsdatavariabler sorteras i bokstavsordning i bearbetningsregelgränssnittet, så med namnutrymmen kan du snabbt se variabler som finns i samma namnutrymme.

Vi har också hört att några av er namnger kontextdatanycklar med evar- eller prop-numret:

```js
"eVar1":"jimbo"
```

Detta kan göra det *lite* enklare när du utför en engångsmappning i bearbetningsregler, men du förlorar läsbarheten under felsökning och framtida koduppdateringar kan vara svårare. Vi rekommenderar i stället att du använder beskrivande namn för nycklar och värden:

```js
"username":"jimbo"
```

Ange kontextvariabler som definierar räknarhändelser till värdet &quot;1&quot;:

```js
"logon":"1"
```

Kontextdatavariabler som definierar inkrementer eller händelser kan ha värdet som ska ökas:

```js
"levels completed":"6"
```

>[!NOTE]
>
>Adobe reserverar namnutrymmet `a.`. Förutom den här lilla begränsningen behöver kontextdatavariabler bara vara unika i ditt inloggningsföretag för att undvika kollisioner.

## Variabeln Produkter {#section_AFBA36F3718C44D29AF81B9E1056A1B4}

Om du vill ange *`products`* i mobil-SDK måste du använda en speciell syntax. Se [Produktvariabel](/help/windows-appstore/analytics/products/products.md).

## (Valfritt) Aktivera spårning offline {#section_955B2A03EB854742BDFC4A0A3C287009}

Om du vill lagra träffar när enheten är offline kan du aktivera offlinespårning i [ADBMomobileConfig.json-konfigurationen](/help/windows-appstore/c-configuration/methods.md). Innan du aktiverar spårning offline bör du vara uppmärksam på de tidsstämpelkrav som beskrivs i config-filreferensen.

## Geografisk placering och intressepunkter {#section_BAD34A8DD013454DB355121316BD7FD4}

Med geopositionering kan du mäta positionsdata (latitud/longitud) och fördefinierade intressepunkter. Varje `TrackLocation` samtal skickar:

* Latitud/longitud och POI (om det finns i en POI definierad i `ADBMobileConfig.json` konfigurationsfilen). Dessa skickas till mobillösningsvariabler för automatisk rapportering.
* Avståndet från mitten och noggrannheten skickas som kontextdata. Hämta med en bearbetningsregel.

Så här spårar du en plats:

```js
var ADB = ADBMobile; 
ADB.Analytics.trackLocation(37.75345, -122.33207, null);
```

Om följande POI definieras i `ADBMobileConfig.json` konfigurationsfilen:

```js
"poi" : [ 
            ["San Francisco",37.757144,-122.44812,7000], 
        ]
```

När enhetsplatsen är inom en radie på 7 000 meter från den definierade punkten skickas en `a.loc.poi` kontextdatavariabel med värdet &quot;San Francisco&quot; med `TrackLocation` träffen. En `a.loc.dist` kontextvariabel skickas med avståndet i meter från de definierade koordinaterna.

## Livstid {#section_D2C6971545BA4D639FBE07F13EF08895}

Livstidsvärdet gör att du kan mäta och inrikta dig på ett livstidsvärde för varje användare. Varje gång du skickar ett värde med `TrackLifetimeValueIncrease`läggs värdet till det befintliga värdet. Livstidsvärdet lagras på enheten och kan hämtas när som helst genom att anropa `GetLifetimeValue`. Detta kan användas för att lagra livstidsinköp, annonsvisningar, videokompletteringar, sociala resurser, fotoöverföringar och så vidare.

```js
// Lifetime Value Example 
var ADB = ADBMobile; 
var purchasePrice = 39.95; 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
cdata["ItemPurchaseEvent"] = "ItemPurchaseEvent"; 
cdata["PurchaseItem"] = "Item453"; 
cdata["PurchasePrice"] = purchasePrice; 
ADB.Analytics.trackLifetimeValueIncrease(purchasePrice, cdata);
```

## Tidsbestämda åtgärder {#section_7FF8B6A913A0460EAA4CAE835E32D8C1}

Med tidsbestämda åtgärder kan du mäta tiden i appen och den totala tiden mellan åtgärdens början och slut. SDK beräknar hur lång tid i sessionen och den totala tid (korssession) det tar för åtgärden att slutföras. Detta kan användas för att definiera segment som ska jämföras i tid för inköp, passeringsnivå, utcheckningsflöde och så vidare.

* Totalt antal sekunder i programmet mellan start och slut - tvärsessioner
* Totalt antal sekunder mellan start och slut (klocktid)

```js
// Timed Action Start Example 
var ADB = ADBMobile; 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
cdata["ExperienceName"] = experience; 
ADB.Analytics.trackTimedActionStart("TimeUntilPurchase", cdata);
```

```js
// Timed Action Update Example 
var ADB = ADBMobile; 
var cdataUpdate = new Windows.Foundation.Collections.PropertySet(); 
cdataUpdate["ImageLiked"] = imageName; 
ADB.Analytics.trackTimedActionStart("TimeUntilPurchase", cdata); 
```

```js
// Timed Action End Example 
var ADB = ADBMobile; 
ADB.Analytics.trackTimedActionEnd("TimeUntilPurchase");
```
