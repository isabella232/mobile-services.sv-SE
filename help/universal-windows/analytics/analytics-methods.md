---
description: Information som hjälper dig att använda universella Windows Platform SDK med Adobe Analytics.
solution: Experience Cloud,Analytics
title: Analysmetoder
topic-fix: Developer and implementation
uuid: cc299bb5-ec61-49bf-869a-f3c3bc83359f
exl-id: 3ceaedfa-274f-4dc7-9e4c-15233d09f935
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 29%

---

# Analysmetoder {#analytics-methods}

Information som hjälper dig att använda universella Windows Platform SDK med Adobe Analytics.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target och Audience Manager. Metoderna är prefasta enligt lösningen. Analysmetoder har prefixet&quot;Analytics&quot;.

Var och en av dessa metoder används för att skicka data till din Adobe Analytics rapportsvit.

>[!TIP]
>
>När du använder `winmd`-metoder från winJS (JavaScript) kommer den första bokstaven automatiskt att sänkas för alla metoder.

* **TrackState (winJS: trackState)**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel&quot;heminstrumentpanel&quot;,&quot;appinställningar&quot;,&quot;kundvagn&quot; och så vidare. Dessa lägen liknar sidor på en webbplats och `TrackState` anropar stegvisa sidvyer.
Om `state` är tom visas den som &quot;programnamnsprogramversion (build)&quot; i rapporter. Om det här värdet visas i rapporter måste du ange `state` för varje `TrackState`-anrop.

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

   Skickar de aktuella x y-koordinaterna. Intressepunkter som definieras i `ADBMobileConfig.json`-filen används också för att avgöra om platsen som anges som en parameter finns i något av dina POI-dokument. Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med anropet `trackLocation`.

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

   Lägger till `amount` till användarens livstidsvärde.

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

   Ange `contextData` för att uppdatera kontextdata som är associerade med angiven `action`. `data` som skickas läggs till i befintliga data för den angivna åtgärden och skriver över data om samma nyckel redan har definierats för `action`.

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
