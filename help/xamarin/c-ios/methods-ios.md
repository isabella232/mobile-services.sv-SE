---
description: iOS-metoder för Xamarin-komponenter för Experience Cloud-lösningar 4.x SDK.
keywords: Xamarin
seo-description: iOS-metoder för Xamarin-komponenter för Experience Cloud-lösningar 4.x SDK.
seo-title: iOS-metoder
solution: Marketing Cloud,Developer
title: iOS-metoder
uuid: d6a056db-80c1-44d0-970f-c961ad01b0bc
translation-type: tm+mt
source-git-commit: f53953831e6471ea64eb2ae06ddae16ca0eab6f6

---


# iOS-metoder{#ios-methods}

iOS-metoder för Xamarin-komponenter för Experience Cloud-lösningar 4.x SDK.

## Konfigurationsmetoder {#section_405AA09390E346E5BB7B1F4E0F65F51E}

* **CollectLifecycleData**

   Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/ios/metrics.md).

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void CollectLifecycleData();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.CollectLifecycleData();
      ```

* **DebugLogging**

   Returnerar den aktuella inställningen för felsökningsloggning. Standardvärdet är `false`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static bool DebugLogging(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var debugEnabled = ADBMobile.DebugLogging();
      ```

* **SetDebugLogging**

   Anger att inställningen för felsökningsloggning ska vara aktiverad.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void SetDebugLogging(bool enabled);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.SetDebugLogging(true);
      ```

* **LifetimeValue**

   Returnerar livstidsvärdet för den aktuella användaren.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static double LifetimeValue();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var lifetimeValue = ADBMobile.LifetimeValue();
      ```

* **PrivacyStatus**

   Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus.
   * `ADBMobilePrivacyStatus.OptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatus.OptOut` - träffar tas bort.
   * ADBMoblePrivacyStatus.Unknown - Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras). Om spårning offline är inaktiverat ignoreras träffar tills sekretessstatusen ändras för att anmäla sig.
   Standardvärdet anges i [ADBMobleConfig.json](/help/ios/configuration/json-config/json-config.md).

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static ADBPrivacyStatus PrivacyStatus();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var privacyStatus = ADBMobile.PrivacyStatus();
      ```


* **SetPrivacyStatus**

   Anger sekretessstatus för den aktuella användaren till status. Ange något av följande värden:
   * `ADBMobilePrivacyStatus.OptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatus.OptOut` - träffar tas bort.
   * `ADBMobilePrivacyStatus.Unknown`  - Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras för att anmäla sig.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void SetPrivacyStatus(ADBPrivacyStatus status) 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.SetPrivacyStatus(ADBMobilePrivacyStatus.OptIn); 
      ```

* **UserIdentifier**

   Returnerar den anpassade användaridentifieraren om en anpassad identifierare har angetts. Returnerar null om ingen anpassad identifierare har angetts. Standardvärdet är `null`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static string UserIdentifier(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var userId = ADBMobile.UserIdentifier(); 
      ```

* **SetUserIdentifier**

   Returnerar den anpassade användaridentifieraren om en anpassad identifierare har angetts. Returnerar null om ingen anpassad identifierare har angetts. Standardvärdet är `null`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static string UserIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.SetUserIdentifier ("customUserIdentifier”); 
      ```

* **GetVersion**

   Hämtar biblioteksversionen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static string Version();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var version = ADBMobile.Version();
      ```

* **KeepLifecycleSessionAlive (endast iOS)**

   Anger för SDK att nästa återupptagning från bakgrunden inte ska starta en ny session, oavsett värdet på tidsgränsen för livscykelsessionen i konfigurationsfilen.

   >[!TIP]
   >
   >Den här metoden är avsedd att användas för program som registrerar sig för meddelanden i bakgrunden och ska endast anropas från koden som körs medan appen finns i bakgrunden.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void KeepLifecycleSessionAlive();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.KeepLifecycleSessionAlive();
      ```

## Analysmetoder {#section_63CF636104EF41F790C3E4190D755BBA}

* **TrackingIdentifier**

   Hämtar identifieraren för analysspårning.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static string TrackingIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var trackingId = ADBMobile.TrackingIdentifier();
      ```

* **TrackState**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel&quot;titelskärm&quot;,&quot;nivå 1&quot;,&quot;paus&quot; och så vidare. Dessa lägen liknar sidor på en webbplats och anropar `TrackState` inkrementella sidvyer. Om läget är tomt visas det som&quot;programnamnsversion (build)&quot; i rapporter. Om du ser det här värdet i rapporter måste du ange status för varje `TrackState` anrop.

   [!TIP]
   >Det här är det enda spårningsanropet som ökar sidvisningen.
   >
   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackState(string state, NSDictionary cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDictionary contextData; 
       contextData = NSDictionary.FromObjectAndKey (NSObject.FromObject("val"),NSObject.FromObject("key")); 
        ADBMobile.TrackState("title screen", contextData); 
      ```

* **TrackAction**

   Spårar en åtgärd i din app. Åtgärder är det som händer i appen och som du vill mäta, till exempel&quot;dödsfall&quot;,&quot;ökad nivå&quot;,&quot;feed-prenumerationer&quot; och andra mätvärden.

   >[!TIP]
   Om du har kod som kan köras medan programmet är i bakgrunden (till exempel en hämtning av bakgrundsdata) använder du `trackActionFromBackground` istället.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackAction(string action, NSDictionary cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackAction("level gained", null); 
      ```

* **TrackActionFromBackground (endast iOS)**

   Spårar en åtgärd som inträffade i bakgrunden. Detta förhindrar att livscykelhändelser utlöses i vissa scenarier.

   >[!TIP]
   Den här metoden ska bara anropas i kod som körs medan programmet finns i bakgrunden.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackActionFromBackground(string action, NSDictionary cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackActionFromBackground("majorLocationChange", null);
      ```

* **TrackLocation**

   Skickar de aktuella latitud- och longitudkoordinaterna. Intressepunkter som definierats i filen används också för att avgöra om den plats som angetts som en parameter finns i någon av dina POI-filer. `ADBMobileConfig.json` Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `TrackLocation` anropet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackLocation(CLLocation location, NSDictionary cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      CoreLocation.CLLocation l = new CoreLocation.CLLocation  (111.111, 44.156);
      ADBMobile.TrackLocation (l, null);
      ```

* **TrackBeacon**

   Spårar när en användare kommer in i närheten av en beacon.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackBeacon( CLBeacon beacon, NSDictionary cdata);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      CoreLocation.CLBeacon beacon = new CoreLocation.CLBeacon (); 
      ADBMobile.TrackBeacon (beacon, null);
      ```

* **SpårningRensaAktuellBeteckning**

   Rensar beacons data efter att en användare lämnat beacons närhet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackingClearCurrentBeacon();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackingClearCurrentBeacon();
      ```

* **TrackLifetimeValueIncrease**

   Lägger till belopp till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      public nbsp;static void TrackLifetimeValueIncrease(double amount, NSDictionary cdata);

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackLifetimeValueIncrease(5, null); 
      ```

* **TrackTimedActionStart**

   Starta en tidsbestämd åtgärd med namnåtgärd. Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackTimedActionStart(string action, NSDictionary cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackTimedActionStart("level2", null);
      ```

* **TrackTimedActionUpdate**

   Skicka data för att uppdatera kontextdata som är associerade med den angivna åtgärden. De data som skickas läggs till befintliga data för den angivna åtgärden och skriver över data om samma nyckel redan har definierats för åtgärden.

   >[!TIP]
   Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackTimedActionUpdate(string action, NSDictionary cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDictionary updatedData = NSDictionary.FromObjectAndKey (NSObject.FromObject("val2"), NSObject.FromObject ("key2")); 
        ADBMobile.TrackTimedActionUpdate("level2", updatedData); 
      ```

* **TrackTimedActionEnd**

   Avsluta en tidsbestämd åtgärd.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackTimedActionEnd(string action, Func<double, double, NSMutableDictionary, sbyte> block); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackTimedActionEnd  ("level2", (double  arg1,  double  arg2,  NSMutableDictionary  arg3)  =>  { 
      return  Convert.ToSByte(true); 
      });
      ```

* **TrackingTimedActionExists**

   Returnerar om en tidsbestämd åtgärd pågår (eller inte).

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static bool TrackingTimedActionExists(string action); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackTimedActionEnd  ("timedAction",  (double  inAppDuration, 
      double  totalDuration,  NSMutableDictionary  data)  =>  { 
                   return  true; 
      });
      ```

* **SpåraSkickaKöadeHits**

   Tvingar biblioteket att skicka alla träffar i offlinekön oavsett hur många som står i kö.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackingSendQueuedHits();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TrackingSendQueuedHits(); 
      ```

* **SpårningRensaKö**

   Tar bort alla träffar från offlinekön.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TrackingClearQueue(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
       ADBMobile.TrackingClearQueue();
      ```

* **SpårningHämtaKöstorlek**

   Hämtar antalet träffar som för närvarande finns i offlinekö.

   * Här är kodexemplet för den här metoden:

      ```objective-c
      public static int TrackingGetQueueSize();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var queueSize = ADBMobile.TrackingGetQueueSize(); 
      ```

## Experience Cloud ID-metoder {#section_157919E46030443DBB5CED60D656AD9F}

* **GetMarketingCloudID**

   Hämtar Experience Cloud-ID:t från ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static string GetMarketingCloudID(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var mcid = ADBMobile.GetMarketingCloudID();
      ```

* **VisitorSyncIdentifierare**

   Med Experience Cloud ID kan ni ange ytterligare kund-ID:n som ska kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare, tillsammans med en kundtypsidentifierare som avgränsar omfattningen för olika kund-ID:n. Den här metoden motsvarar setCustomerID:n i JavaScript-biblioteket.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void VisitorSyncIdentifiers(NSDictionary identifiers);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDictionary  ids  =  NSDictionary.FromObjectAndKey  (NSObject.FromObject  ("value2"),  NSObject.FromObject  ("pushID")); 
      ADBMobile.VisitorSyncIdentifiers(ids); 
      ```

## Målmetoder {#section_C1E4121CAF9D43538511D857A1F549A7}

* **TargetLoadRequest**

   Skickar begäran till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett `Action<NSDictionary>` återanrop.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TargetLoadRequest (ADBTargetLocationRequest request, Action<NSString> callback); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDictionary  dict  =  NSDictionary.FromObjectAndKey  (NSObject.FromObject  ("value2"),  NSObject.FromObject  ("key1")); 
      ADBTargetLocationRequest  req  =  ADBMobile.TargetCreateRequest  ("iOSTest",  "defGal",  dict); 
      ADBMobile.TargetLoadRequest(req,    (context)  =>  { 
      Console.WriteLine  (context); 
      });
      ```

* **TargetCreateRequest**

   Bekvämt med konstruktor för att skapa ett `ADBTargetLocationRequest` objekt med de givna parametrarna.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static ADBTargetLocationRequest ADBTargetLocationRequest TargetCreateRequest (string name, string defaultContent, NSDictionary parameters); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDictionary  dict  =  NSDictionary.FromObjectAndKey  (NSObject.FromObject  ("value2"),  NSObject.FromObject  ("key1")); 
      ADBTargetLocationRequest  req  =  ADBMobile.TargetCreateRequest  ("iOSTest",  "defGal",  dict); 
      ```

* **TargetCreateOrderConfirmRequest**

   Skapar en `ADBTargetLocationRequest`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static ADBTargetLocationRequest ADBTargetLocationRequest TargetCreateRequest (string name, string defaultContent, NSDictionary parameters);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TargetCreateOrderConfirmRequest ("myOrder", "12345", "29.41", "cool stuff", null); 
      ```

* **TargetClearCookies**

   Tar bort alla målcookies från din app.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void TargetClearCookies(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.TargetClearCookies(); 
      ```

## Audience Manager {#section_862C4202B6294B978DEEBB15C5CD5C01}

* **AudienceVisitorProfile**

   Returnerar den besökarprofil som senast hämtades. Returnerar noll om ingen signal har skickats ännu. Besökarprofilen sparas i `NSUserDefaults` så att du enkelt kan komma åt den när du startar appen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static NSDictionary AudienceVisitorProfile (); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDictionary profile = ADBMobile.AudienceVisitorProfile();
      ```

* **AudienceDpid**

   Returnerar aktuellt DPID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static string AudienceDpid ();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      string currentDpid = ADBMobile.AudienceDpid();
      ```

* **AudienceDpuuid**

   Returnerar aktuellt DPUID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static string AudienceDpuuid ();
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      string currentDpuuid = ADBMobile.AudienceDpuuid(); 
      ```

* **AudienceSetDpidAndDpuuid**

   Ställer in dpid och dpuuid. Om dpid och dpuuid är inställda skickas de med varje signal.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void AudienceSetDpidAndDpuuid (NSDictionary data, Action<NSDictionary> callback); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.AudienceSetDpidAndDpuuid ("testDppid", "testDpuuid")
      ```

* **AudienceSignalWithData**

   Skickar målgruppshantering en signal med egenskaper och hämtar matchande segment som returneras i ett `Action<NSDictionary>` återanrop.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void AudienceSignalWithData (NSDictionary data, Action<NSDictionary> callback); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSDictionary  audienceData  =  NSDictionary.FromObjectAndKey  (NSObject.FromObject  ("value2"),  NSObject.FromObject  ("key1")); 
      ADBMobile.AudienceSignalWithData  (audienceData,  (context)  =>  { 
      Console.WriteLine  (context); 
      }); 
      ```

* **AudienceReset**

   Återställer UUID för målgruppshanteraren och tömmer den aktuella besökarprofilen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void AudienceReset ();
      ```

   * Här är syntaxen för den här metoden:

      ```objective-c
      ADBMobile.AudienceReset ();
      ```

## Video {#section_CBCE1951CE204A108AD4CA7BB07C7F98}

Mer information finns i [Videoanalys](/help/ios/getting-started/dev-qs.md).

* **MediaCreateSettings**

   Returnerar ett `ADBMediaSettings` objekt med angivna parametrar.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static ADBMediaSettings MediaCreateSettings ([string name, double length, string playerName, string playerID); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMediaSettings settings = ADBMobile.MediaCreateSettings ("name1", 10, "playerName1", "playerID1"); 
      ```

* **MediaAdCreateSettings**

   Returnerar ett `ADBMediaSettings` objekt som ska användas för att spåra en annonsvideo.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static ADBMediaSettings MediaAdCreateSettings ( string name,  double length,  string playerName,  string parentName,  string parentPod,  double parentPodPosition,  string CPM); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMediaSettings adSettings = ADBMobile.MediaAdCreateSettings("adName1", 2, "playerName1", "name1", "podName1", 4, "CPM1");
      ```

* **MediaOpenWithSettings**

   Öppnar ett `ADBMediaSettings` objekt för spårning.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void MediaOpenWithSettings ( ADBMediaSettings settings,  Action<ADBMediaState> callback); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMediaSettings settings = ADBMobile.MediaCreateSettings  ("name1",  10,  "playerName1",  "playerID1"); 
      ADBMobile.MediaOpenWithSettings  (settings,  (state)  =>  { 
      Console.WriteLine  (state.Name); 
      }); 
      ```

* **MediaClose**

   Stänger medieobjektet med namnet name.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void MediaClose ( string name);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.MediaClose  (settings.Name);
      ```

* **MediaPlay**

   Spelar upp medieobjektet med namnet name vid angiven förskjutning (i sekunder).

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void MediaPlay ( string name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.MediaPlay (settings.Name, 0); 
      ```

* **MediaComplete**

   Markera medieobjektet som slutfört manuellt vid angiven förskjutning (i sekunder).

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void MediaComplete ( string name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.MediaComplete (settings.Name, 5);
      ```

* **MediaStop**

   Meddelar mediemodulen att videon har stoppats eller pausats vid den angivna förskjutningen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void MediaStop ( string name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.MediaStop (settings.Name, 3);
      ```

* **MediaClick**

   Meddelar mediemodulen att någon har klickat på medieobjektet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void MediaClick ( string name, double offset); 
      ```

* **MediaTrack**

   Skickar ett spåråtgärdsanrop (ingen sidvy) för det aktuella medieläget.

   * Här är syntaxen för den här metoden:

      ```objective-c
      public static void MediaTrack ( string name, NSDictionary data); 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
       ADBMobile.MediaTrack (settings.Name, null);
      ```
