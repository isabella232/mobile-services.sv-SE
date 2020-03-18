---
description: Klasser och metoder från BlackBerry-biblioteket.
seo-description: Klasser och metoder från BlackBerry-biblioteket.
seo-title: Adobe Mobile, klass- och metodreferens
title: Adobe Mobile, klass- och metodreferens
uuid: 1e42d759-be43-4bb3-ac1a-c7d64133d61c
translation-type: tm+mt
source-git-commit: 68bc21f1c6dba2faeed332495592114af90c8f61

---


# Adobe Mobile, klass- och metodreferens {#adobe-mobile-class-and-method-reference}

Klasser och metoder från BlackBerry-biblioteket.

SDK har för närvarande stöd för Adobe Analytics, och metoderna finns i separata klasser baserade på lösningen.

## SDK-inställningar {#section_C1EB977043C04D2B93E5A63DB72828B6}

* **getPrivacyStatus**

   Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus.

   * ADBMoblePrivacyStatusOptIn - träffar skickas omedelbart.
   * ADBMoblePrivacyStatusOptOut - träffar ignoreras.
   * ADBMoblePrivacyStatusUnknown - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

      Standardvärdet anges i `ADBMobileConfig.json` filen.

   * Här är syntaxen för den här metoden:

      ```cpp
      static ADBMobilePrivacyStatus getPrivacyStatus();
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMobilePrivacyStatus privacyStatus = ADBMobile::getPrivacyStatus();
      ```

* **setPrivacyStatus**

   Anger sekretessstatus för den aktuella användaren till `status`. Ange något av följande värden:

   * `ADBMobilePrivacyStatusOptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut` - träffar tas bort.
   * `ADBMobilePrivacyStatusUnknown` - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

   * Här är syntaxen för den här metoden:

      ```cpp
      static void setPrivacyStatus(ADBMobilePrivacyStatus status);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMobile::setPrivacyStatus(ADBMobilePrivacyStatusOptIn);
      ```

* **getUserIdentifier**

   Returnerar användaridentifieraren om en anpassad identifierare har angetts. Returnerar `null` om ingen anpassad identifierare har angetts. Standardvärdet är `null`.

   * Här är syntaxen för den här metoden:

      ```cpp
      static QString getUserIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      QString userId = ADBMobile::getUserIdentifier(); 
      ```

* **setUserIdentifier**

   Anger användaridentifieraren till `identifier`.

   * Här är syntaxen för den här metoden:

      ```cpp
      static void setUserIdentifier(QString identifier);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMobile::setUserIdentifier("billybob");
      ```

* **getDebugLogging**

   Returnerar den aktuella inställningen för felsökningsloggning. Standardvärdet är `false`.

   * Här är syntaxen för den här metoden:

      ```cpp
      static bool getDebugLogging();
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
       bool debugging = ADBMobile::getDebugLogging(); 
      ```

* **setDebugLogging**

   Anger loggningsinställningar för felsökning till `debugLogging`.

   * Här är syntaxen för den här metoden:

      ```cpp
      static void setDebugLogging(bool debugLogging);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
        ADBMobile::setDebugLogging(true); 
      ```

* **collectLifecycleData**

   Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/blackberry/metrics.md).

   * Här är syntaxen för den här metoden:

      ```cpp
      static void collectLifecycleData();
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ApplicationUI::ApplicationUI(bb::cascades::Application *app):  QObject(app)  { 
      //... 
      ADBMobile::collectLifecycleData(); 
      }
      ```

## Analysmetoder {#section_91F4AD0A045D4E4E8F9A93450503E49E}

Var och en av dessa metoder används för att skicka data till rapportsviten för Adobe Analytics.

* **trackState**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel&quot;heminstrumentpanel&quot;,&quot;appinställningar&quot;,&quot;kundvagn&quot; och så vidare. Dessa lägen liknar sidor på en webbplats och anropar `trackState` stegvisa sidvyer.

   >[!TIP]
   >
   >Det här är det enda spårningsanropet som ökar sidvisningen.

   * Här är syntaxen för den här metoden:

      ```cpp
      static void trackState(QString state, QHash<QString, QString> contextData = QHash<QString, QString>()); 
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
         ADBMobile::trackState("loginScreen", null);
      ```

* **trackAction**

   Spårar en åtgärd i din app. Åtgärder är det som händer i appen som du vill mäta, till exempel&quot;inloggningar&quot;,&quot;banderollknappar&quot;,&quot;flödesprenumerationer&quot; och andra mätvärden.

   * Här är syntaxen för den här metoden:

      ```cpp
      static void trackAction(QString action, QHash<QString, QString> contextData = QHash<QString, QString>()); 
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
        ADBMobile::trackAction("heroBannerTouched", null); 
      ```

* **trackLocation**

   Skickar de aktuella x y-koordinaterna. Ersätt händelse med händelse som tas emot från prenumeranten på BPS.

   * Här är syntaxen för den här metoden:

      ```cpp
      static void trackLocation(bps_event_t *geoEvent, QHash<QString, QString> contextData = QHash<QString, QString> ());
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
        ADBMobile::trackLocation(event, null);
      ```

## `ADBMobileConfig.json` config file reference {#section_5AD4EDF87E304980B4AC4A5657FDA8B9}

Filen måste `ADBMobileConfig.json` placeras i *resursmappen* .

* **rsids**

   (Obligatoriskt) En eller flera rapportsviter för att ta emot analysdata. Flera rapportpaket-ID:n ska vara kommaavgränsade utan mellanrum.

   Här är kodexemplet för den här variabeln:

   ```js
   "rsids" : "rsid"
   ```

   ```js
   "rsids" : "rsid1,rsid2"
   ```

* **server**

   (Obligatoriskt). Analysserver. Den här variabeln ska fyllas i med serverdomänen, utan ett `https://` - eller `https://` protokollprefix. Protokollprefixet hanteras automatiskt av biblioteket baserat på `ssl` variabeln. Om `ssl` så är `true`fallet skapas en säker anslutning till den här servern. Om `ssl` så är `false`fallet skapas en osäker anslutning till den här servern.

* **charset**

   Definierar den teckenuppsättning som du använder för data som skickas till Analytics. Teckenuppsättningen används för att konvertera inkommande data till UTF-8 för lagring och rapportering.

* **ssl**

   Aktiverar (`true`) eller inaktiverar (`false`) sändning av mätdata via SSL (HTTPS). Standardvärdet är `false`.

* **offlineEnabled**

   När det är aktiverat (`true`) köas träffar när enheten är offline och skickas senare när enheten är online. Din rapportsvit måste vara tidsstämpelaktiverad för att du ska kunna använda offline-spårning.

   >[!TIP]
   >
   >Om tidsstämplar är aktiverade i rapportsviten `offlineEnabled` måste *konfigurationsegenskapen vara* `true`. Om rapportsviten inte är tidsstämpelaktiverad `offlineEnabled` måste ** konfigurationsegenskapen vara false. Om detta inte är korrekt konfigurerat går data förlorade. Om du är osäker på om en rapportsserie är tidsstämplad, kontaktar du [Enterprise Support](https://helpx.adobe.com/contact/enterprise-support.ec.html).

   Om du för närvarande rapporterar AppMeasurement-data till en rapportserie som även samlar in data från JavaScript, kan du behöva skapa en separat rapportserie för mobildata, eller inkludera en anpassad tidsstämpel för alla JavaScript-träffar med hjälp av `s.timestamp` variabeln.

   Standardvärdet är `false`.

* **lifecycleTimeout**

   Anger hur lång tid (i sekunder) som måste gå mellan det att programmet startas innan det betraktas som en ny session. Den här tidsgränsen gäller även när programmet skickas till bakgrunden och återaktiveras. Den tid som programmet lägger i bakgrunden inkluderas inte i sessionslängden.

   Standardvärdet är 300 sekunder.

* **batchLimit**

   Maximalt antal offlineträffar som lagras i kön. Standardvärdet är 0 (ingen gräns).

* **privacyDefault**

   * `optedin` - träffar skickas omedelbart.
   * `optedout` - träffar tas bort.
   * `optunknown` - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras).

      Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.
   Den här variabeln anger bara startvärdet. Om det här värdet någonsin anges eller ändras i koden används det nya värdet tills det ändras, eller så avinstalleras programmet och installeras sedan om.

   Standardvärdet är `optedin`.

Följande är ett exempel på en `ADBMobileConfig.json` fil:

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
    } 
}
```
