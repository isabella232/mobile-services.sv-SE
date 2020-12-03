---
description: När du har lagt till biblioteket i ditt projekt kan du göra alla anrop till analysmetoden var som helst i din app (se till att du importerar ADBMomobile.h till din klass).
seo-description: När du har lagt till biblioteket i ditt projekt kan du göra alla anrop till analysmetoden var som helst i din app (se till att du importerar ADBMomobile.h till din klass).
seo-title: 'Analytics '
title: 'Analytics '
uuid: de018eda-b37d-4afe-83a0-8011381d7aff
translation-type: tm+mt
source-git-commit: 7ae626be4d71641c6efb127cf5b1d3e18fccb907
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 3%

---


# Analytics{#analytics} 

När du har lagt till biblioteket i ditt projekt kan du göra alla anrop till analysmetoden var som helst i din app (se till att du importerar ADBMomobile.h till din klass).

## Aktivera mobilappsrapporter i Analytics {#task_3DA1354942CF4BF4B11B9CC97588A9ED}

Innan du lägger till kod bör du be Analytics Administrator att slutföra följande för att aktivera livscykelspårning för mobilappar. Detta garanterar att rapportsviten är redo att samla in mätvärden när ni börjar utveckla.


1. Öppna **[!UICONTROL Admin Tools]** > **[!UICONTROL Report Suites]** och välj en eller flera mobila rapportsviter.
1. Klicka på **[!UICONTROL Edit Settings]** > **[!UICONTROL Mobile Management]** > **[!UICONTROL Mobile Application Reporting]**.

   ![](assets/mobile-settings.png)

1. Klicka på **[!UICONTROL Enable Latest App Reports]**.

   Du kan också klicka **[!UICONTROL Enable Mobile Location Tracking]** och **[!UICONTROL Enable Legacy Reporting and Attribution for background hits]**.

   ![](assets/enable-lifecycle.png)

Livscykelmätvärden är nu klara att hämtas och Mobile Application Reports visas på **[!UICONTROL Reports]** menyn i gränssnittet för marknadsföringsrapporter.

## Samla in livscykelvärden {#task_25D469C62DF84573AEB5E8E950B96205}

1. Om du vill samla in livscykelvärden i appen anropar du `collectLifecycleData()` i `ApplicationUI` konstruktorn.

   Exempel:

   ```java
   ApplicationUI::ApplicationUI(bb::cascades::Application *app): QObject(app) { 
   //... 
   ADBMobile::collectLifecycleData(); 
   } 
   ```

   Om `collectLifecycleData()` anropas två gånger under samma session kommer programmet att rapportera en krasch vid varje samtal efter det första. SDK anger en flagga när programmet stängs som anger att det har avslutats. Om flaggan inte är inställd rapporterar en krasch `collectLifecyleData()` .

## Event, props och eVars {#concept_B885D5A71A5D45129CE7C1C3426A7D28}


Om du har tittat på [ADBMomobile Class och Method Reference](/help/blackberry/methods.md)undrar du antagligen var du ska ange händelser, eVars, props, heirs och lists. I version 4 kan du inte längre tilldela dessa typer av variabler direkt i appen. I stället använder SDK kontextdata och bearbetningsregler för att mappa appdata till Analytics-variabler för rapportering.

Bearbetningsreglerna ger dig flera fördelar:

* Du kan ändra datamappningen utan att skicka en uppdatering till App Store.
* Du kan använda beskrivande namn för data i stället för att ange variabler som är specifika för en rapportserie.
* Det har liten inverkan på att skicka in extra data. Dessa värden visas inte i rapporter förrän de mappas med bearbetningsregler.

Alla värden som du tilldelade direkt till variabler ska i stället läggas till i `data` HashMap.

## Behandlingsregler {#concept_3EA4CD602AF4488A896B0EDD3BA2D969}

Bearbetningsregler används för att kopiera data som du skickar i kontextdatavariabler till variabler, props och andra variabler för rapportering.

[Utbildning](https://tv.adobe.com/embed/1181/16506/) i bearbetningsregler på Summit 2013

[Bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html)

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

Kontextvariabler som definierar räknarhändelser kan ha samma nyckel och värde:

```js
"logon":"logon"
```

Sammanhangsdatavariabler som definierar stegvisa händelser kan ha händelsen som nyckel och mängden som ska ökas som värde:

```js
"levels completed":"6"
```

>[!TIP]
>
>Adobe reserverar namnutrymmet `a.`. Förutom den här lilla begränsningen behöver kontextdatavariabler bara vara unika i ditt inloggningsföretag för att undvika kollisioner.

## Aktivera spårning offline {#concept_402F4ECE240B4CA1B779322A7BFCB8DE}

Om du vill lagra träffar när enheten är offline kan du aktivera spårning offline i `ADBMobileConfig.json` filen.

Var mycket noggrann med de tidsstämpelkrav som beskrivs i konfigurationsfilreferensen innan du aktiverar spårning offline.

## Analysmetoder

En lista över de analysmetoder som är tillgängliga för BlackBerry finns i *Analysmetoder* i [Adobe Mobile Class och Method Reference](/help/blackberry/methods.md).