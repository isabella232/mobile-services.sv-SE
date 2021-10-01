---
description: Lista över Audience Manager-metoder i Windows 8.1 Universal App Store-biblioteket.
solution: Experience Cloud,Analytics
title: Audience Manager-metoder
topic-fix: Developer and implementation
uuid: e39c9c3e-fd53-4b46-8fff-88101a064a9c
exl-id: b10d7274-0fc6-4822-a40b-1192b71592b9
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 28%

---

# Audience Manager-metoder {#audience-manager-methods}

Lista över Audience Manager-metoder i Windows 8.1 Universal App Store-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target och Audience Manager. Metoderna är prefasta enligt lösningen. Audience Manager-metoder har prefixet &quot;AudienceManager&quot;.

>[!NOTE]
>
>När du använder winmd-metoder från winJS (JavaScript) får alla metoder automatiskt sin första bokstav att sänkas.

Om målgruppshanteraren är konfigurerad i JSON-filen skickas en signal med livscykelstatistik in med din livscykelträff.

* **GetVisitorProfile (winJS: getVisitorProfile)**

   Returnerar den besökarprofil som senast hämtades. Returnerar `null` om ingen signal har skickats ännu. Besökarprofilen sparas i `SharedPreferences` så att du enkelt kan komma åt den när du startar programmet flera gånger.

   * Här är syntaxen för den här metoden:

      ```csharp
      static fWindows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^GetVisitorProfile();
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

   Skickar Audience Manager en signal med egenskaper och hämtar matchande segment som returneras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::IAsyncOperation<Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object> > ^SignalWithData(Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^data);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile; 
      var traits = new Windows.Foundation.Collections.PropertySet(); 
      traits["trait"] = "b"; 
      ADB.AudienceManager.signalWithData(traits).then(function(visitorProfile) { 
        // segments come back here in "visitorProfile", normally found in the "segs" object of your json 
      }); 
      ```
