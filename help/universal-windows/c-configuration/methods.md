---
description: Klasser och metoder som tillhandahålls av Universal Windows Platform-biblioteket.
seo-description: Klasser och metoder som tillhandahålls av Universal Windows Platform-biblioteket.
seo-title: SDK-metoder
solution: Experience Cloud,Analytics
title: SDK-metoder
topic-fix: Developer and implementation
uuid: e3aa41d6-7bc0-4208-a662-12907c209a77
exl-id: 0aac477c-074d-457c-b117-bb205119c475
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 22%

---

# SDK-metoder {#sdk-methods}

Klasser och metoder som tillhandahålls av Universal Windows Platform-biblioteket.

>[!TIP]
>
>När du använder `winmd`-metoder från winJS (JavaScript) kommer den första bokstaven automatiskt att sänkas för alla metoder.

* **GetVersion (winJS: getVersion)**

   Returnerar den aktuella versionen av Adobe Mobile-biblioteket.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Platform::String ^GetVersion();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;var libVersion = ADB.Config.getVersion();
      ```

* **GetPrivacyStatusAsync (winJS: getPrivacyStatusAsync)**

   Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus.

   * `ADBMobilePrivacyStatusOptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut` - Träffar tas bort.
   * `ADBMobilePrivacyStatusUnknown` - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla dig (träffar ignoreras). Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

      Standardvärdet anges i konfigurationsfilen `ADBMobileConfig.json`. Mer information finns i [ADBMobleConfig.json config file](/help/universal-windows/c-configuration/c.json.md).

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::IAsyncOperation<ADBMobilePrivacyStatus>
      ^getPrivacyStatusAsync();
      ```

   * Här är kodexemplen för den här metoden:

      **C Sharp**

      ```csharp
      public enum class ADBMobilePrivacyStatus : int { ADBMobilePrivacyStatusOptIn = 1, 
      ADBMobilePrivacyStatusOptOut = 2, 
      ADBMobilePrivacyStatusUnknown = 3};
      ```

      **JavaScript**

      ```javascript
      var ADB = ADBMobile;
      var status;
      ADB.Config.getPrivacyStatusAsync.then(function(privacyStatus) {
        status = privacyStatus;}
      );
      ```

* **SetPrivacyStatus (winJS: setPrivacyStatus)**

   Anger den aktuella användarens sekretessstatus till `status`. Ange något av följande värden:
   * `ADBMobilePrivacyStatusOptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut` - träffar tas bort.
   * `DBMobilePrivacyStatusUnknown` - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller välja bort (träffar tas bort). Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

      * Här är syntaxen för den här metoden:

         ```csharp
         static void SetPrivacyStatus(ADBMobilePrivacyStatus status);
         ```

      * Här är kodexemplen för den här metoden:

         **C-vass**

         ```csharp
         public enum class ADBMobilePrivacyStatus : int { 
           ADBMobilePrivacyStatusOptIn = 1, 
           ADBMobilePrivacyStatusOptOut = 2
           ADBMobilePrivacyStatusUnknown = 3
         };
         ```

         **JavaScript**

         ```js
         var ADB = ADBMobile;
         ADB.Config.setPrivacyStatus (ADB.ADBMobilePrivacyStatus.adbmobilePrivacyStatusOptIn
         );
         ```

* **GetLifetimeValue (winJS: getLifetimeValue)**

   Returnerar livstidsvärdet för den aktuella användaren. Standardvärdet är `0`.

   * Här är syntaxen för den här metoden:

      ```csharp
      static float GetLifetimeValue(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      var ltv = ADB.Config.getLifetimeValue();
      ```

* **GetUserIdentifier (winJS: getUserIdentifier)**

   Returnerar den anpassade användaridentifieraren om en anpassad identifierare har angetts. Returnerar `null` om ingen anpassad identifierare har angetts.
Standardvärdet är `null`.

   >[!IMPORTANT]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas den tidigare ID-tjänsten (anpassad eller automatiskt genererad) och lagras som en anpassad användaridentifierare. Detta bevarar besöksdata mellan uppgraderingar av SDK. För nya installationer på 4.x SDK är användaridentifieraren `null` tills den anges.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Platform::String ^GetUserIdentifier(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```csharp
      var ADB = ADBMobile;
      var userId = ADB.Config.getUserIdentifier(); 
      ```

* **SetUserIdentifier (winJS: setUserIdentifier)**

   Anger användaridentifieraren till `identifier`.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void SetUserIdentifier(Platform::String ^userIdentifier); 
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      var ADB = ADBMobile;
      ADB.Config.setUserIdentifier("someUserId");
      ```

* **GetDebugLogging (winJS: getDebugLogging)**

   Returnerar den aktuella inställningen för felsökningsloggning. Standardvärdet är `false`.

   * Här är syntaxen för den här metoden:

      ```csharp
      static bool GetDebugLogging();
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      var ADB = ADBMobile;
      var logging = ADB.Config.getDebugLogging();
      ```

* **SetDebugLogging (winJS: setDebugLogging)**

   Anger inställningen för felsökningsloggning till `debugLogging`. Felsökningsloggning fungerar endast när felsökningsversionen av biblioteket används. Den här inställningen ignoreras av den officiella versionen.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void SetDebugLogging(bool debugLogging);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      ADB.Config.setDebugLogging(true);
      ```

* **CollectLifecycleData (winJS: collectLifecycleData)**

   Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelmått](/help/universal-windows/metrics.md).

   * Här är syntaxen för den här metoden:

      ```csharp
      static void CollectLifecycleData();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      ADB.Config.collectLifecycleData();
      ```

* **PauseCollecting &#x200B; LifecycleData (winJS: pauseSamlar &#x200B; LifecycleData)**

   Anger för SDK att din app är pausad, så att livscykelvärdena beräknas korrekt. Vid paus samlas t.ex. en tidsstämpel in för att bestämma den tidigare sessionslängden. Detta anger också en flagga så att livscykeln vet att programmet inte kraschade. Mer information finns i [Livscykelvärden](/help/universal-windows/metrics.md).

   * Här är syntaxen för den här metoden:

      ```csharp
      static void PauseCollectingLifecycleData();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      ADB.Config.pauseCollectingLifecycleData(); 
      ```
