---
description: Information som hjälper dig att använda universella Windows Platform SDK med Adobe Analytics.
seo-description: Information som hjälper dig att använda universella Windows Platform SDK med Adobe Analytics.
seo-title: Analysmetoder
solution: Experience Cloud,Analytics
title: Analysmetoder
topic: Developer and implementation
uuid: cc299bb5-ec61-49bf-869a-f3c3bc83359f
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 28%

---


# Analysmetoder {#analytics-methods}

Information som hjälper dig att använda universella Windows Platform SDK med Adobe Analytics.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target och Audience Manager. Metoderna är prefasta enligt lösningen. Analysmetoder har prefixet&quot;Analytics&quot;.

Var och en av dessa metoder används för att skicka data till din Adobe Analytics rapportsvit.

>[!TIP]
>
>När du använder `winmd` metoder från winJS (JavaScript) får alla metoder automatiskt sin första bokstav nedsänkt.

* **TrackState (winJS: trackState)**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel&quot;heminstrumentpanel&quot;,&quot;appinställningar&quot;,&quot;kundvagn&quot; och så vidare. Dessa lägen liknar sidor på en webbplats och anropar `TrackState` stegvisa sidvyer.
Om `state` är tom visas den som&quot;programnamnsversion (build)&quot; i rapporter. Om du ser det här värdet i rapporter måste du kontrollera att du anger det `state` i varje `TrackState` samtal.

   >[!TIP]
   >
   >Det här är det enda spårningsanropet som ökar sidvisningen.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void TrackState(Platform::String ^state, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object> ^contextData); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile
      ADB.Analytics.trackState("loginScreen", null);
      ```

* **TrackAction (winJS: trackAction)**

   Spårar en åtgärd i din app. Åtgärder är det som händer i appen som du vill mäta, till exempel&quot;inloggningar&quot;,&quot;banderollknappar&quot;,&quot;flödesprenumerationer&quot; och andra mätvärden.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void TrackAction(Platform::String ^action, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object> ^contextData); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varADB=ADBMobile; 
      ADB.Analytics.trackAction("ButtonClick",null); 
      ```

* **GetTrackingIdentifierAsync (winJS: getTrackingIdentifierAsync)**

   Returnerar det automatiskt genererade besökar-ID:t för Analytics. Detta är ett programspecifikt unikt besökar-ID som genereras vid den första starten och sedan lagras och används från den tidpunkten. Detta ID bevaras mellan programuppgraderingar och tas bort vid avinstallationen.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::IAsyncOperation<Platform::String> ^GetTrackingIdentifierAsync(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      vartrackingIdentifier; 
      ADBMobile.Analytics.getTrackingIdentifierAsync().then(function(trackingid){
      trackingIdentifier=trackingid;
      });
      ```

* **TrackLocation (winJS: trackLocation)**

   Skickar de aktuella x y-koordinaterna. Intressepunkter som definierats i filen används också för att avgöra om den plats som angetts som en parameter finns i någon av dina POI-filer. `ADBMobileConfig.json` Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation` anropet.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void TrackLocation(double lat, double lon, double accuracy, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object> ^contextData);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varADB=ADBMobile; 
      ADB.Analytics.trackLocation(47.60621,-122.33207,null);
      ```

* **TrackLifetime &#x200B; ValueIncrease (winJS: trackLifetime &#x200B; ValueIncrease)**

   Lägger `amount` till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void TrackLifetimeValueIncrease(float amount, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object> ^contextData); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varADB=ADBMobile;
      ADB.Analytics.trackLifetimeValueIncrease(10,null);
      ```

* **TrackTimed &#x200B; ActionStart (winJS: trackTimed &#x200B; ActionStart)**

   Starta en tidsbestämd åtgärd med namnet `action`. Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void TrackTimedActionStart(Platform::String ^action, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^contextData); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varADB=ADBMobile;
      ADB.Analytics.trackTimedActionStart("cartToCheckout",null); 
      ```

* **TrackTimed &#x200B; ActionUpdate (winJS: trackTimed &#x200B; ActionUpdate)**

   Skicka in `contextData` för att uppdatera kontextdata som är associerade med den angivna `action`. Den `data` inskickade filen läggs till i befintliga data för den angivna åtgärden och skriver över data om samma nyckel redan har definierats för `action`.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void TrackTimedActionUpdate(Platform::String ^action, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object> ^contextData); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varADB = ADBMobile;
      varcontextData = newWindows.Foundation.Collections.PropertySet();
      contextData["quantity"]=3; 
      ADB.Analytics.trackTimedActionUpdate("cartToCheckout",contextData);
      ```

* **TrackTimedActionExistsAsync (winJS: trackTimedActionExistsAsync)**

   Returnerar true om den angivna tidsbestämda åtgärden finns och false om den inte finns.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::IAsyncOperation<bool> ^TrackTimedActionExistsAsync(Platform::String ^action); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADBMobile.Analytics.trackTimedActionExistsAsync("signUp").then(function(exists){ 
          actionExists = exists; 
      });
      ```

* **TrackTimed &#x200B; ActionEnd (winJS: trackTimed &#x200B; ActionEnd)**

   Avsluta en tidsbestämd åtgärd.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void TrackTimedActionEnd(Platform::String ^action);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varADB = ADBMobile; 
      ADB.Analytics.trackTimedActionEnd("cartToCheckout"); 
      ```

* **ClearTrackingQueue (winJS: clearTrackingQueue)**

   Tar bort alla lagrade träffar från kön för Analytics-spårning.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void ClearTrackingQueue();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADBMobile.Analytics.clearTrackingQueue();
      ```

* **GetQueueSizeAsync (winJS: getQueueSizeAsync)**

   Returnerar antalet träffar som för närvarande lagras i Analytics-kön.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::IAsyncOperation<int> ^GetQueueSizeAsync();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varqueueSize;
      ADBMobile.Analytics.getQueueSizeAsync().then(function(size){ 
          queueSize=size;
      });
      ```
