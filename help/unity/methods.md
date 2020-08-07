---
description: 'null'
keywords: Unity
seo-description: 'null'
seo-title: ADBMoble.cs-metoder
solution: Marketing Cloud,Developer
title: ADBMoble.cs-metoder
uuid: af504934-febd-45d9-81e2-2a310f4c65dc
translation-type: tm+mt
source-git-commit: c198ae57b05f8965a8e27191443ee2cd552d6c50
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 35%

---


# ADBMoble.cs-metoder {#adbmobile-cs-methods}

## Konfigurationsmetoder

* **CollectLifecycleData**

   Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/ios/metrics.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void CollectLifecycleData();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.CollectLifecycleData();
      ```

* **EnableLocalNotifications (endast iOS)**

   Aktivera lokala meddelanden i din app.

   * Här är syntaxen för den här metoden:

      ```java
      public static void EnableLocalNotifications();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.EnableLocalNotifications();
      ```

* **GetDebugLogging**

   Returnerar den aktuella inställningen för felsökningsloggning. Standardvärdet är `false`.

   * Här är syntaxen för den här metoden:

      ```java
      public static bool GetDebugLogging();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var debugEnabled = ADBMobile.GetDebugLogging();
      ```

* **GetLifetimeValue**

   Returnerar livstidsvärdet för den aktuella användaren.

   * Här är syntaxen för den här metoden:

      ```java
      public static double GetLifetimeValue();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var lifetimeValuea = ADBMobile.GetLifetimeValue();
      ```

* **GetPrivacyStatus**

   Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus.
   * `MOBILE_PRIVACY_STATUS_OPT_IN`: Träffar skickas omedelbart.
   * `MOBILE_PRIVACY_STATUS_OPT_OUT`: Träffar ignoreras.
   * `MOBILE_PRIVACY_STATUS_UNKNOWN`: Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras).

      Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras för att anmäla sig. Standardvärdet anges i [filen ADBMobilConfig.json](/help/ios/configuration/json-config/json-config.md) .

   * Här är syntaxen för den här metoden:

      ```java
      public static ADBPrivacyStatus GetPrivacyStatus();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var privacyStatus = ADBMobile.GetPrivacyStatus();
      ```

* **GetUserIdentifier**

   Returnerar den anpassade användaridentifieraren om en anpassad identifierare har angetts. Returnerar null om ingen anpassad identifierare har angetts. Standardvärdet är `null`.

   * Här är syntaxen för den här metoden:

      ```java
      public static string GetUserIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var userId = ADBMobile.GetUserIdentifier();
      ```

* **GetVersion**

   Hämtar biblioteksversionen.

   * Här är syntaxen för den här metoden:

      ```java
      public static string GetVersion();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var version = ADBMobile.GetVersion();
      ```

* **KeepLifecycleSessionAlive (endast iOS)**

   Anger för SDK att nästa återupptagning från bakgrunden inte ska starta en ny session, oavsett värdet på tidsgränsen för livscykelsessionen i konfigurationsfilen.

   >[!TIP]
   >
   >Den här metoden är avsedd att användas för program som registrerar sig för meddelanden i bakgrunden och ska endast anropas från koden som körs medan appen finns i bakgrunden.

   * Här är syntaxen för den här metoden:

      ```java
      public static void KeepLifecycleSessionAlive();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.KeepLifecycleSessionAlive();
      ```

* **PauseCollectingLifecycleData (endast Android)**

   Anger för SDK att din app är pausad, så att livscykelvärdena beräknas korrekt. Vid paus samlas t.ex. en tidsstämpel in för att bestämma den tidigare sessionslängden. Detta anger också en flagga så att livscykeln vet att programmet inte kraschade. Mer information finns i [Livscykelvärden](/help/android/metrics.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void PauseCollectingLifecycleData();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.PauseCollectingLifecycleData();
      ```

* **SetContext (endast Android)**

   Anger för SDK att programkontexten ska ställas in från UnityPlayers aktuella aktivitet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SetContext();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.SetContext();
      ```

* **SetDebugLogging**

   Anger att inställningen för felsökningsloggning ska vara aktiverad.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SetDebugLogging (bool enabled);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.SetDebugLogging(true);
      ```

* **SetPrivacyStatus**

   Anger sekretessstatus för den aktuella användaren till status. Ange något av följande värden:

   * `MOBILE_PRIVACY_STATUS_OPT_IN`: Träffar skickas omedelbart.
   * `MOBILE_PRIVACY_STATUS_OPT_OUT`: Träffar ignoreras.
   * `MOBILE_PRIVACY_STATUS_UNKNOWN`: Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras för att anmäla sig.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SetPrivacyStatus(ADBPrivacyStatusstatus);
      ```

   * Här är kodexemplet för den här syntaxen:

      ```java
      ADBMobile.SetPrivacyStatus(ADBMobile.ADBPrivacyStatus.MOBILE_PRIVACY_STATUS_OPT_IN);
      ```

* **SetUserIdentifier**

   Anger användaridentifieraren till userId.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SetUserIdentifier(string userId);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.SetUserIdentifier("myCustomUserId");
      ```

## Analysmetoder

* **GetTrackingIdentifier**

   Hämtar identifieraren för analysspårning.

   * Här är syntaxen för den här metoden:

      ```java
      public static string GetTrackingIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var trackingId = ADBMobile.GetTrackingIdentifier();
      ```

* **TrackState**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel&quot;titelskärm&quot;,&quot;nivå 1&quot;,&quot;paus&quot; och så vidare. Dessa lägen liknar sidor på en webbplats och anropar `TrackState` stegvisa sidvyer.

   Om läget är tomt visas det som *`app name app version (build)`* i rapporter. Om du ser det här värdet i rapporter måste du ange status för varje `TrackState` anrop.

   >[!TIP]
   >
   >Det här är det enda spårningsanropet som ökar sidvisningen.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackState(string state, Dictionary<string, object> cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var contextData = new Dictionary<string, object>);
      contextData.Add ("user", "jim");
      ADBMobile.TrackState("title screen", contextData);
      ```

* **TrackAction**

   Spårar en åtgärd i din app. Åtgärder är det som händer i appen och som du vill mäta, till exempel&quot;dödsfall&quot;,&quot;ökad nivå&quot;,&quot;feed-prenumerationer&quot; och andra mätvärden.

   >[!TIP]
   >
   >Om du har kod som kan köras medan programmet är i bakgrunden (till exempel en hämtning av bakgrundsdata) använder du `trackActionFromBackground` istället.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackAction(string action, Dictionary<string, object> cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackAction("level gained", null);
      ```

* **TrackActionFromBackground (endast iOS)**

   Spårar en åtgärd som inträffade i bakgrunden. Detta förhindrar att livscykelhändelser utlöses i vissa scenarier.

   >[!TIP]
   >
   >Den här metoden ska bara anropas i kod som körs medan programmet finns i bakgrunden.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackActionFromBackground(string action, Dictionary<string,object> cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackActionFromBackground("majorLocationChange", null);
      ```

* **TrackLocation**

   Skickar de aktuella latitud- och longitudkoordinaterna. Intressepunkter som definierats i filen används också för att avgöra om den plats som angetts som en parameter finns i någon av dina POI-filer. `ADBMobileConfig.json` Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med TrackLocation-anropet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackLocation(float latValue, float lonValue, Dictionary<string, object> cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackLocation(28.418649, -81.581324, null);
      ```

* **TrackBeacon**

   Spårar när en användare kommer in i närheten av en beacon.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackBeacon(int major, int minor, string uuid, ADBBeaconProximity proximity, Dictionary<string, object> cdata);
      ```

* **SpårningRensaAktuellBeteckning**

   Rensar beacons data efter att en användare lämnat beacons närhet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackingClearCurrentBeacon();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackingClearCurrentBeacon();
      ```

* **TrackLifetimeValueIncrease**

   Lägger till belopp till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackLifetimeValueIncrease(double amount, Dictionary<string, object> cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackLifetimeValueIncrease(5, null);
      ```

* **TrackTimedActionStart**

   Starta en tidsbestämd åtgärd med namnåtgärd. Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackTimedActionStart(string action, Dictionary<string,object> cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackTimedActionStart("level2", null);
      ```

* **TrackTimedActionUpdate**

   Skicka data för att uppdatera kontextdata som är associerade med den angivna åtgärden. De data som skickas läggs till befintliga data för den angivna åtgärden och skriver över data om samma nyckel redan har definierats för åtgärden.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackTimedActionUpdate(string action, Dictionary<string, object> cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var contextData = new Dictionary<string, object>;
      contextData.Add("checkpoint", "1:32");
         ADBMobile.TrackTimedActionUpdate("level2", contextData);
      ```

* **TrackTimedActionEnd**

   Avsluta en tidsbestämd åtgärd.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackTimedActionEnd(string action);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackTimedActionEnd("level2");
      ```

* **TrackingTimedActionExists**

   Returnerar om en tidsbestämd åtgärd pågår eller inte.

   * Här är syntaxen för den här metoden:

      ```java
      public static bool TrackingTimedActionExists(string action);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
       var level2InProgress = ADBMobile.TrackingTimedActionExists("level2");
      ```

* **SpåraSkickaKöadeHits**

   Tvingar biblioteket att skicka alla träffar i offlinekön oavsett hur många som står i kö.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackingSendQueuedHits();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackingSendQueuedHits();
      ```

* **SpårningRensaKö**

   Tar bort alla träffar från offlinekön.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackingClearQueue();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADBMobile.TrackingClearQueue();
      ```

* **SpårningHämtaKöstorlek**

   Hämtar antalet träffar som för närvarande finns i offlinekö.

   * Här är syntaxen för den här metoden:

      ```java
      public static int TrackingGetQueueSize();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var queueSize = ADBMobile.TrackingGetQueueSize();
      ```

## Experience Cloud ID-metoder

* **GetMarketingCloudID**

   Hämtar Experience Cloud-ID:t från ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      public static string GetMarketingCloudID();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var mcid = ADBMobile.GetMarketingCloudID();
      ```

* **VisitorSyncIdentifierare**

   Med Experience Cloud-ID:t kan du ange ytterligare kund-ID:n som ska kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare, tillsammans med en kundtypsidentifierare som avgränsar omfattningen för olika kund-ID:n. Den här metoden motsvarar setCustomerID:n i JavaScript-biblioteket.

   * Här är syntaxen för den här metoden:

      ```java
      public static void VisitorSyncIdentifiers(Dictionary<string, object> identifiers);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var ids = new Dictionary<string, object> ();
      ids.Add ("player1", "jimbob");
      ADBMobile.VisitorSyncIdentifiers(ids);
      ```

## Anskaffningsmetoder

* **ProcessGooglePlayInstallReferrerUrl** *(endast Android)*

   Skicka referenswebbadressen som returneras från ett anrop till Google Play Install Reference-API till den här metoden.

   * Här är syntaxen för den här metoden:

      ```java
      public static void ProcessGooglePlayInstallReferrerUrl(string referrerUrl);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      // in actual implementation, the referrer url should be retrieved
      // from the Google Play Install Referrer API.
      var myReferrer = "utm_source=unityTestSource&utm_content=unityTestContent&utm_campaign=unityTestCampaign";
      ADBMobile.ProcessGooglePlayInstallReferrerUrl(myReferrer);
      ```
