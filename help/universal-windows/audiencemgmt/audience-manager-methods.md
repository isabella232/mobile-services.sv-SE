---
description: Lista över Audience Manager-metoder som tillhandahålls av Universal Windows Platform-biblioteket.
seo-description: Lista över Audience Manager-metoder som tillhandahålls av Universal Windows Platform-biblioteket.
seo-title: Audience Manager-metoder
solution: Marketing Cloud,Analytics
title: Audience Manager-metoder
topic: Developer and implementation
uuid: efbe8f33-7f53-40a6-b7aa-a36ac718c047
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Audience Manager-metoder{#audience-manager-methods}

Lista över Audience Manager-metoder som tillhandahålls av Universal Windows Platform-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target och Audience Manager. Metoderna är prefasta enligt lösningen. Audience Manager-metoder har prefixet `AudienceManager`.

>[!TIP]
>
>När du använder `winmd` metoder från winJS (JavaScript) får alla metoder automatiskt sin första bokstav nedsänkt.

Om målgruppshanteraren är konfigurerad i din JSON-fil skickas en signal som innehåller livscykelvärden in med livscykelträffen.

* **GetVisitorProfile (winJS: getVisitorProfile)**

   Returnerar den besökarprofil som senast hämtades. Returneras `null` om ingen signal har skickats ännu. Besökarprofilen sparas i `SharedPreferences` så att du enkelt kan komma åt den när du startar appen.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::Collections::IMap<Platform::String^,Platform::Object^> ^GetVisitorProfile();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile; 
      var profile = ADB.AudienceManager.getVisitorProfile();
      ```

* **GetDpid (winJS: getDpid)**

   Returnerar aktuellt DPID.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Platform::String ^GetDpid();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      var dpid = ADB.AudienceManager.getDpid(); 
      ```

* **GetDpuuid (winJS: getDpuuid)**

   Returnerar aktuellt DPUID.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Platform::String ^GetDpuuid();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile; 
      var dpuuid = ADB.AudienceManager.getDpuuid();
      ```

* **SetDpidAndDpuuid (winJS: setDpidAndDpuuid)**

   Anger DPID och DPUID. Om DPID och DPUID anges skickas de med varje signal.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void SetDpidAndDpuuid(Platform::String ^dpid, Platform::String ^dpuuid);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile; 
      ADB.AudienceManager.setDpidAndDpuuid("newDpid", "newDpuuid");
      ```

* **SignalWithData (winJS: signalWithData)**

   Skickar målgruppshantering en signal med egenskaper och hämtar matchande segment som returneras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```csharp
      static 
      Windows::Foundation::IAsyncOperation<Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^> ^SignalWithData(Windows::Foundation::Collections::IMap<Platform::String^,Platform::Object> ^data);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      var traits = new Windows.Foundation.Collections.PropertySet(); 
      traits["trait"] = "b";
      ADB.AudienceManager.signalWithData(traits).then(function (visitorProfile) { 
        // segments come back here in "visitorProfile", normally found in the "segs" object of your json 
      }); 
      
