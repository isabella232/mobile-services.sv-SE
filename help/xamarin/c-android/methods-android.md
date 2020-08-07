---
description: Android-metoder för Xamarin-komponenter för Experience Cloud-lösningar 4.x SDK.
keywords: Xamarin
seo-description: Android-metoder för Xamarin-komponenter för Experience Cloud-lösningar 4.x SDK.
seo-title: Android-metoder
solution: Marketing Cloud,Developer
title: Android-metoder
uuid: 860af1c4-f57e-4bcb-8308-4e316da9a27b
translation-type: tm+mt
source-git-commit: c198ae57b05f8965a8e27191443ee2cd552d6c50
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 39%

---


# Android-metoder{#android-methods}

Android-metoder för Xamarin-komponenter för Experience Cloud-lösningar 4.x SDK.

## Konfigurationsmetoder {#section_405AA09390E346E5BB7B1F4E0F65F51E}

* **DebugLogging**

   Returnerar den aktuella inställningen för felsökningsloggning och standardinställningen är false.

   * Här är syntaxen för den här metoden:

      ```java
      public static Boolean DebugLogging;
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      getter: var debuglog = Config.DebugLogging;
      setter: Config.DebugLogging = (Java.Lang.Boolean)true;
      ```

* **LifetimeValue**

   Returnerar livstidsvärdet för den aktuella användaren.

   * Här är syntaxen för den här metoden:

      ```java
      public static BigDecimal LifetimeValue; 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
       var lifetimeValue = Config.LifetimeValue;
      ```

* **PrivacyStatus**

   Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus.
   * `ADBMobilePrivacyStatus.OptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatus.OptOut` - träffar tas bort.
   * `ADBMobilePrivacyStatus.Unknown` - Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras för att anmäla sig.

   Standardvärdet anges i [filen ADBMobilConfig.json](/help/android/configuration/json-config/json-config.md) .

   * Här är syntaxen för den här metoden:

      ```java
      public static MobilePrivacyStatus PrivacyStatus; 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      getter: var privacyStatus = Config.PrivacyStatus; 
      setter: Config.PrivacyStatus = MobilePrivacyStatus.MobilePrivacyStatusUnknown;
      ```


* **UserIdentifier**

   Om en anpassad identifierare har angetts returneras den här identifieraren. Om ingen anpassad identifierare anges returneras null. Standardvärdet är `null`.

   * Här är syntaxen för den här metoden:

      ```java
      public static UserIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      getter: var userId = Config.UserIdentifier;
      setter: Config.UserIdentifier = "imBatman";
      ```

* **Version**

   Hämtar biblioteksversionen.

   * Här är syntaxen för den här metoden:

      ```java
      public static string Version;
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var version = ADBMobile.Version;
      ```

* **PauseCollectingLifecycleData**

   Anger för SDK att din app är pausad, så att livscykelvärdena beräknas korrekt. Vid paus samlas t.ex. en tidsstämpel in för att bestämma den tidigare sessionslängden. Detta anger också en flagga så att livscykeln vet att programmet inte kraschade. Mer information finns i [Livscykelvärden](/help/android/metrics.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void PauseCollectingLifecycleData (); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.PauseCollectingLifecycleData();
      ```

* **CollectLifecycleData (aktivitet)**

   (4.2 eller senare) Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/android/metrics.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void collectLifecycleData(Activity activity); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.CollectLifecycleData (this);
      ```

* **CollectLifecycleData (aktivitet)**

   (4.2 eller senare) Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/android/metrics.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void collectLifecycleData(Activity activity, IDictionary<string, Object> context));
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      IDictionary<string, Java.Lang.Object> context = new Dictionary<string, 
      Java.Lang.Object> ();
      context.Add ("key", "value");
      Config.CollectLifecycleData (this, context);
      ```

* **OverrideConfigStream**

   (4.2 eller senare) Gör att du kan läsa in en annan `ADBMobile JSON` konfigurationsfil när programmet startas. Den olika konfigurationen används tills programmet stängs.

   * Här är syntaxen för den här metoden:

      ```java
      public static void OverrideConfigStream (Stream stream);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Stream st1 = Assets.Open ("ADBMobileConfig-2.json"); 
      Config.OverrideConfigStream (st1); 
      ```

* **SetLargeIconResourceId(int resourceId)**

   (4.2 eller senare) Anger den stora ikonen som används för meddelanden som skapas av SDK:n. Den här ikonen är den primära bild som visas när användaren ser det fullständiga meddelandet i meddelandecentret.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SetLargeIconResourceId( int resourceId);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.SetLargeIconResourceId(R.drawable.appIcon);
      ```

* **SetSmallIconResourceId(int resourceId)**

   (4.2 eller senare) Anger den lilla ikon som används för meddelanden som skapas av SDK. Den här ikonen visas i statusfältet och är den sekundära bilden som visas när användaren ser det fullständiga meddelandet i meddelandecentret.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SetSmallIconResourceId( int resourceId); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
       Config.SetSmallIconResourceId(R.drawable.appIcon);
      ```

## Analysmetoder {#section_63CF636104EF41F790C3E4190D755BBA}

* **TrackingIdentifier**

   Returnerar det automatiskt genererade ID:t för Analytics. Detta är ett programspecifikt unikt ID som genereras vid den första starten och som lagras och används från den tidpunkten. Detta ID bevaras mellan programuppgraderingar och tas bort vid avinstallationen.

   * Här är syntaxen för den här metoden:

      ```java
      public static string TrackingIdentifier;
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Var trackingId = Analytics.TrackingIdentifier
      ```

* **TrackState**

   Spårar ett apptillstånd med valfria kontextdata. `States` är de vyer som är tillgängliga i din app, till exempel&quot;titelskärm&quot;,&quot;nivå 1&quot;,&quot;paus&quot; och så vidare. Dessa lägen liknar sidor på en webbplats och anropar `TrackState` stegvisa sidvyer. Om läget är tomt visas det som&quot;app name app version (build)&quot; i rapporter. Om du ser det här värdet i rapporter måste du ange status för varje `TrackState` anrop.

   >[!TIP]
   >
   >Det här är det enda spårningsanropet som ökar sidvisningen.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackState (string state, IDictionary<string, Object> cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var cdata = new Dictionary<string, Java.Lang.Object>(); 
      cdata.Add ("key", (Java.Lang.Object)"value"); 
      Analytics.TrackState ("stateName", (IDictionary<string, 
      Java.Lang.Object>)cdata);
      ```

* **TrackAction**

   Spårar en åtgärd i din app. Åtgärder är det som händer i appen och som du vill mäta, till exempel&quot;dödsfall&quot;,&quot;ökad nivå&quot;,&quot;feed-prenumerationer&quot; och andra mätvärden.

   >[!TIP]
   >
   >
   >Om du har kod som kan köras medan programmet är i bakgrunden (till exempel en hämtning av bakgrundsdata) använder du `trackActionFromBackground` istället.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackAction(string action, IDictionary<string,Object> cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var cdata = new Dictionary<string, Java.Lang.Object> (); 
      cdata.Add ("key", (Java.Lang.Object)"value");
      Analytics.TrackAction ("actionName", (IDictionary<string, 
      Java.Lang.Object>)cdata);
      ```

* **TrackLocation**

   Skickar de aktuella latitud- och longitudkoordinaterna. Intressepunkter som definierats i filen används också för att avgöra om platsen som angavs som parameter finns i någon av dina POI:er. `ADBMobileConfig.json` Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `TrackLocation` anropet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackLocation(Location location, IDictionary<string, Object> cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
       Location loc = new Location(LocationManager.GpsProvider);;
       loc.Latitude = 111; 
       loc.Longitude = 44; 
       loc.Accuracy = 5; 
       Analytics.TrackLocation (loc, null);
      ```

* **TrackBeacon**

   Spårar när en användare kommer in i närheten av en beacon.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackBeacon (string uuid, string major, string minor,  Analytics.BEACON_PROXIMITY prox, IDictionary<string, Object> cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.TrackBeacon ("UUID", "1", "2", 
      Analytics.BEACON_PROXIMITY.ProximityImmediate, null); 
      ```

* **ClearBeacon**

   Rensar beacons data efter att en användare lämnat beacons närhet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackingClearCurrentBeacon();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.ClearBeacon(); 
      ```

* **TrackLifetimeValueIncrease**

   Lägger till ett belopp till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackLifetimeValueIncrease (double amount, IDictionary<string,Object> cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.TrackLifetimeValueIncrease(5,null);
      ```

* **TrackTimedActionStart**

   Starta en tidsbestämd åtgärd med namnåtgärd. Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   > Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackTimedActionStart(string action,IDictionary<string, Object> cdata); 
      ```

   * Här följer ett kodexempel för den här metoden:

      ```java
      Analytics.TrackTimedActionStart("level2", null);
      ```

* **TrackTimedActionUpdate**

   Skicka data för att uppdatera kontextdata som är associerade med den angivna åtgärden. De data som skickas läggs till befintliga data för den angivna åtgärden och skriver över data om samma nyckel redan har definierats för åtgärden.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackTimedActionUpdate(string action, IDictionary<string, Object> cdata); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var updatedData = new Dictionary<string, Java.Lang.Object> (); 
      cdata.Add ("key", (Java.Lang.Object)"value"); 
      Analytics.TrackTimedActionUpdate("level2", updatedData); 
      ```

* **TrackTimedActionEnd**

   Avsluta en tidsbestämd åtgärd.

   * Här är syntaxen för den här metoden:

      ```java
      public static void TrackTimedActionEnd(string action,
        Analytics.ITimedActionBlock block);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.TrackTimedActionEnd ("level2", new TimedActionBlock()); 
           class TimedActionBlock: Java.Lang.Object, 
      Analytics.ITimedActionBlock{ 
           public Java.Lang.Object Call (long inAppDuration, long 
      totalDuration IDictionary<string, Java.Lang.Object> contextData){ 
           return Java.Lang.Boolean.True; 
        } 
      }
      ```

* **TrackingTimedActionExists**

   Returnerar om en tidsbestämd åtgärd pågår.

   * Här är syntaxen för den här metoden:

      ```java
      public static bool TrackingTimedActionExists(string action); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var level2InProgress = Analytics.TrackingTimedActionExists("level2"); 
      ```

* **SendQueuedHits**

   Tvingar biblioteket att skicka alla träffar i offlinekön, oavsett hur många träffar som står i kö.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SendQueuedHits();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.SendQueuedHits(); 
      ```

* **ClearQueue**

   Tar bort alla träffar från offlinekön.

   * Här är syntaxen för den här metoden:

      ```java
      public static void ClearQueue(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.ClearQueue(); 
      ```

* **QueueSize**

   Hämtar antalet träffar som finns i offlinekön.

   * Här är syntaxen för den här metoden:

      ```java
      public static long QueueSize(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var queueSize = Analytics.QueueSize();
      ```

## Experience Cloud ID-metoder {#section_157919E46030443DBB5CED60D656AD9F}

* **MarketingCloudId**

   Hämtar Experience Cloud-ID:t från ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      public static string MarketingCloudId;
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var mcid = Visitor.MarketingCloudId;
      ```

* **SyncIdentifiers**

   Med Experience Cloud-ID:t kan du ange ytterligare kund-ID:n som ska kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare, med en kundtypsidentifierare som avgränsar omfånget för olika kund-ID:n. Den här metoden motsvarar den `setCustomerIDs` i JavaScript-biblioteket.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SyncIdentifiers((IDictionary<string> identifiers);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      IDictionary<string,string> ids = new Dictionary<string, string> ();
      ids.Add ("pushID", ;"value2");
      Visitor.SyncIdentifiers (ids);
      ```

## Målmetoder {#section_C1E4121CAF9D43538511D857A1F549A7}

* **LoadRequest**

   Skickar en begäran till din konfigurerade målserver och returnerar strängvärdet för erbjudandet som genererats i ett `Action<NSDictionary>` återanrop.

   * Här är syntaxen för den här metoden:

      ```java
      public static void LoadRequest (TargetLocationRequest request, Target.ITargetCallback callback); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      class TargetBlock: Java.Lang.Object, Target.ITargetCallback{ 
          public void Call (Java.Lang.Object content) 
         { 
          Console.WriteLine (content.ToString()); 
         } 
      } 
      var req = Target.CreateRequest ("AndroidTest", "defGal", parameters); 
           Target.LoadRequest (req, new TargetBlock()); 
      ```

* **CreateRequest**

   Bekvämt med konstruktor för att skapa ett `ADBTargetLocationRequest` objekt med de givna parametrarna.

   * Här är syntaxen för den här metoden:

      ```java
      public static TargetLocationRequest TargetCreateRequest(string name,string defaultContent,IDictionary<string,string> parameters); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      IDictionary<string, Java.Lang.Object> parameters = new Dictionary> string, Java.Lang.Object> (); 
          parameters.Add ("key1", "value2"); 
      var req = Target.CreateRequest ("AndroidTest", "defGal", parameters); 
      ```

* **CreateOrderConfirmRequest**

   Skapar en `ADBTargetLocationRequest`.

   * Här är syntaxen för den här metoden:

      ```java
      public static TargetLocationRequest TargetCreateRequest (string name, string defaultContent, IDictionary<;string, string> parameters);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      var orderConfirm = Target.CreateOrderConfirmRequest ("myOrder", "12345", "29.41", "cool stuff", null); 
      ```

* **ClearCookies**

   Rensar Target-cookies från din app.

   * Här är syntaxen för den här metoden:

      ```java
      public static void ClearCookies(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Target.ClearCookies (); 
      ```

## Audience Manager {#section_862C4202B6294B978DEEBB15C5CD5C01}

* **VisitorProfile**

   Returnerar den besökarprofil som senast hämtades. Returnerar noll om ingen signal har skickats ännu. Besökarprofilen sparas i `NSUserDefaults` så att du enkelt kan komma åt den när du startar appen.

   * Här är syntaxen för den här metoden:

      ```java
      public static IDictionary<string, Object> VisitorProfile; 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      NSDictionary profile = AudienceManager.VisitorProfile; 
      ```

* **Dpid**

   Returnerar aktuell `DPID`.

   * Här är syntaxen för den här metoden:

      ```java
      public static string Dpuuid; 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      string currentDpid = AudienceManager.Dpid;
      ```

* **Dpuuid**

   Returnerar aktuell `DPUUID`.

   * Här är syntaxen för den här metoden:

      ```java
      public static string AudienceDpuuid; 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      string currentDpuuid = AudienceManager.Dpuuid;
      ```

* **AudienceSetDpidAndDpuuid**

   Anger `dpid` och `dpuuid`. Om `dpid` och `dpuuid` är inställda skickas de med varje signal.

   * Här är syntaxen för den här metoden:

      ```java
      public static void AudienceSetDpidAndDpuuid (string Dpid, String Dpuuid);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      AudienceManager.SetDpidAndDpuuid ("testDpid", "testDpuuid");
      ```

* **SignalWithData**

   Skickar målgruppshantering en signal med egenskaper och hämtar matchande segment som returneras i ett `Action<NSDictionary>` återanrop.

   * Här är syntaxen för den här metoden:

      ```java
      public static void SignalWithData (IDictionary<string, Object> audienceData, AudienceManager.IAudienceManagerCallback callback); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      class AudienceManagerCallback: Java.Lang.Object, 
       AudienceManager.IAudienceManagerCallback{ 
         public void Call (Java.Lang.Object content) 
        {
          Console.WriteLine (content.ToString()); 
        }
      }
      IDictionary<string, Java.Lang.Object> traits = new Dictionary<string, 
      Java.Lang.Object> (); 
         traits.Add ("trait", "b");
      AudienceManager.SignalWithData (traits, new AudienceManagerCallback());
      ```

* **Återställ**

   Återställer målgruppshanteraren `UUID` och tömmer den aktuella besökarprofilen.

   * Här är syntaxen för den här metoden:

      ```java
      public static void Reset ();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
       AudienceManager.Reset ();
      ```

## Video {#section_CBCE1951CE204A108AD4CA7BB07C7F98}

Mer information om videoanalys finns i [Videoanalys](/help/android/analytics-main/video-qs.md).

* **MediaSettings**

   Returnerar ett `MediaSettings` objekt med angivna parametrar.

   * Här är syntaxen för den här metoden:

      ```java
      public static MediaSettings SettingsWith (string name, double length, string playerName, string playerID);  
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      MediaSettings settings = Media.SettingsWith("name1", 10, "playerName1", "playerID1");
      ```

* **AdSettingsWith**

   Returnerar ett `MediaSettings` objekt som ska användas för att spåra en annonsvideo.

   * Här är syntaxen för den här metoden:

      ```java
      public static MediaSettings AdSettingsWith ( string name, double length, 
        string playerName, string parentName, string parentPod, 
      double parentPodPosition, string CPM); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      MediaSettings adSettings = Media.AdSettingsWith ("adName1", 2, "playerName1", "name1", "podName1", 4, "CPM1"); 
      ```

* **Öppna**

   Öppnar ett `ADBMediaSettings` objekt för spårning.

   * Här är syntaxen för den här metoden:

      ```java
      public static void Open (MediaSettings settings, Media.IMediaCallback callback);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      MediaSettings settings = Media.SettingsWith ("name1", 10, "playerName1", "playerID1"); 
         Media.Open (settings, new MediaCallback()); 
         class MediaCallback: Java.Lang.Object, Media.IMediaCallback{ 
      public void Call (Java.Lang.Object content) 
      {
      }
      }
      ```

* **Stäng**

   Stänger medieobjektet med namnet name.

   * Här är syntaxen för den här metoden:

      ```java
      public static void Close(string name);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.Close (settings.Name); 
      ```

* **Spela upp**

   Spelar upp medieobjektet med namnet name vid angiven förskjutning (i sekunder).

   * Här är syntaxen för den här metoden:

      ```java
      public static void Play ( string name, double offset); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.Play (settings.Name, 0); 
      ```

* **Slutförd**

   Markera medieobjektet som slutfört manuellt vid angiven förskjutning (i sekunder).

   * Här är syntaxen för den här metoden:

      ```java
      public static void Complete (string name, double offset); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.Complete (settings.Name, 5); 
      ```

* **Stoppa**

   Meddelar mediemodulen att videon har stoppats eller pausats vid den angivna förskjutningen.

   * Här är syntaxen för den här metoden:

      ```java
      public static void Stop ( string name, double offset); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.Stop (settings.Name, 3);
      ```

* **Klicka på**

   Meddelar mediemodulen att någon har klickat på medieobjektet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void Click ( string name, double offset); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.Click (settings.Name, 3); 
      ```

* **Spåra**

   Skickar ett spåråtgärdsanrop (ingen sidvy) för det aktuella medieläget.

   * Här är syntaxen för den här metoden:

      ```java
      public static void Track ( string name, NSDictionary data); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.Track (settings.Name, null); 
      ```
