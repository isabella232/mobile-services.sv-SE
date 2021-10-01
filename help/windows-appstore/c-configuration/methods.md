---
description: Klasser och metoder som tillhandahålls av Windows 8.1 Universal App Store-biblioteket.
solution: Experience Cloud,Analytics
title: SDK-metoder
topic-fix: Developer and implementation
uuid: 0f558ff4-73d3-4439-9d51-62fbd74d2cea
exl-id: c328fd79-6e10-43b7-9d08-8da395098b60
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 22%

---

# SDK-metoder {#sdk-methods}

Klasser och metoder som tillhandahålls av Windows 8.1 Universal App Store-biblioteket.

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
      varADB = ADBMobile;var libVersion = ADB.Config.getVersion(); 
      ```

* **GetPrivacyStatusAsync (winJS: getPrivacyStatusAsync)**

   Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus.

   * `ADBMobilePrivacyStatusOptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut` - träffar tas bort.
   * `ADBMobilePrivacyStatusUnknown` - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

      Standardvärdet anges i filen [ADBMobleConfig.json config](/help/windows-appstore/c-configuration/c.json.md).

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::IAsyncOperation<ADBMobilePrivacyStatus> ^getPrivacyStatusAsync(); 
      ```

   * Här är kodexemplen för den här metoden:

      ```csharp
      public enum class ADBMobilePrivacyStatus : int  {
        ADBMobilePrivacyStatusOptIn = 1, 
        ADBMobilePrivacyStatusOptOut =  2,
        ADBMobilePrivacyStatusUnknown = 3
      };
      ```

      ```js
      var ADB = ADBMobile;
      var status;
      ADB.Config.getPrivacyStatusAsync.then(function(privacyStatus) {
      status = privacyStatus;
      }); 
      ```

* **SetPrivacyStatus (winJS: setPrivacyStatus)**

   Anger den aktuella användarens sekretessstatus till `status`. Ange något av följande värden:

   * `ADBMobilePrivacyStatusOptIn` - träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut` - träffar tas bort.
   * `ADBMobilePrivacyStatusUnknown` - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void SetPrivacyStatus(ADBMobilePrivacyStatus status);
      ```

   * Här är kodexemplet för den här metoden:

      ```csharp
      public enum class ADBMobilePrivacyStatus : int {
        ADBMobilePrivacyStatusOptIn = 1,
        ADBMobilePrivacyStatusOptOut = 2,
        ADBMobilePrivacyStatusUnknown = 3
        }; 
      ```

      ```js
      var ADB = ADBMobile;
      ADB.Config.setPrivacyStatus(ADB.ADBMobilePrivacyStatus.adbmobilePrivacyStatusOptIn); 
      ```

* **GetLifetimeValue (winJS: getLifetimeValue)**

   Returnerar livstidsvärdet för den aktuella användaren. Standardvärdet är 0.

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

   Returnerar den anpassade användaridentifieraren om en anpassad identifierare har angetts. Returnerar null om ingen anpassad identifierare har angetts. Standardvärdet är `null`.

   >[!TIP]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas det tidigare ID:t (antingen anpassat eller automatiskt genererat) och lagras som en anpassad användaridentifierare. Detta bevarar besöksdata mellan uppgraderingar av SDK. För nya installationer på 4.x SDK är användaridentifieraren `null` tills den anges.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Platform::String^GetUserIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
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

      ```js
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

      ```js
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

   Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/windows-appstore/metrics.md).

   >[!TIP]
   >
   >Anropa den här metoden i `onResume()`-metoden i varje aktivitet i programmet, vilket visas i följande exempel. Vi rekommenderar också att du skickar aktiviteten eller tjänsten som kontextobjekt i stället för som global programkontext.

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

   Anger för SDK att din app är pausad, så att livscykelvärdena beräknas korrekt. Vid paus samlas t.ex. en tidsstämpel in för att bestämma den tidigare sessionslängden. Detta anger också en flagga så att livscykeln vet att programmet inte kraschade. Mer information finns i [Livscykelvärden](/help/windows-appstore/metrics.md).

   >[!TIP]
   >
   >Anropa den här metoden i `onPause()`-metoderna i varje aktivitet i ditt program, vilket visas i exemplet. Vi rekommenderar också att du skickar aktiviteten eller tjänsten som kontextobjekt i stället för som global programkontext.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void PauseCollectingLifecycleData();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      ADB.Config.pauseCollectingLifecycleData();
      ```
