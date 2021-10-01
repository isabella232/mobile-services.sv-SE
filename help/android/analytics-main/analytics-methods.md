---
description: Här är en lista över Adobe Analytics-metoder som finns i Android-biblioteket.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Analysmetoder
topic-fix: Developer and implementation
uuid: ac7c640e-9dcc-4724-b561-019cc025d5a7
exl-id: 7914d13e-40a2-4ae2-b759-2660817c2058
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 29%

---

# Analysmetoder {#analytics-methods}

Här är en lista över Adobe Analytics-metoder som finns i Android-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna prefixas enligt lösningen, till exempel har Experience Cloud ID-metoder prefixet `analytics`.

Var och en av följande metoder används för att skicka data till din Adobe Analytics rapportsvit:

* **trackState**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel `home dashboard`, `app settings`, `cart` och så vidare. Dessa lägen liknar sidor på en webbplats och `trackState` anropar stegvisa sidvyer.

   Om `state` är tomt visas `app name app version (build)` i rapporter. Om det här värdet visas i rapporter måste du ange `state` för varje `trackState`-anrop.

   >[!TIP]
   >
   >Det här är det enda spårningsanropet som ökar sidvisningen.

   * Här är syntaxen för den här metoden:

      ```java
      public static void trackState(String state, Map<String, Object> contextData);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.trackState("loginScreen", null);
      ```

* ****
trackActionTracks an action in your app.

   Åtgärder som du vill mäta, t.ex. `logons`, `banner taps`, `feed subscriptions` och andra mått, som finns i din app.

   * Här är syntaxen för den här metoden:

      ```java
      public static void trackAction(String state, Map<String, Object> contextData);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.trackAction("heroBannerTouched", null);
      ```

* ****
getTrackingIdentifierReturnerar den automatiskt genererade besökaridentifieraren för Analytics.

   Detta är ett programspecifikt, unikt besökar-ID som genereras vid den första starten och som lagras och används från den tidpunkten och framåt. ID:t bevaras mellan programuppgraderingar och tas bort när programmet avinstalleras.

   * Här är syntaxen för den här metoden:

      ```java
      public static String getTrackingIdentifier();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      String trackingId = Analytics.getTrackingIdentifier();
      ```

* **trackLocation**

   Skickar aktuell latitud, longitud och plats i en angiven intressepunkt. Mer information finns i [Geografisk placering och intressepunkter](/help/android/location/geo-poi.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void trackLocation(Location location, Map<String, Object> contextData);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.trackLocation(userLocation, null);
      ```

* **trackLifetime &#x200B; ValueIncrease**

   Lägger till `amount` till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```java
      public static void trackLifetimeValueIncrease(BigDecimal amount, Map<String, Object> contextData);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.trackLifetimeValueIncrease(new BigDecimal(30), null);
      ```

* **trackTimed &#x200B; ActionStart**

   Starta en tidsbestämd åtgärd med namnet `action`.

   Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

   ```java
   public static void trackTimedActionStart(String action, Map<String, Object> contextData);
   ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.trackTimedActionStart("cartToCheckout", null)
      ```


* **trackTimed &#x200B; ActionUpdate**

   Ange `contextData` för att uppdatera kontextdata som är associerade med `action`. Det `data` som skickas läggs till i befintliga data för åtgärden, och om samma nyckel redan har definierats för `action` skrivs data över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      public static void trackTimedActionUpdate(String action, Map<String, Object> contextData);
      ```

   * Här följer ett kodexempel för den här metoden:

      ```java
      HashMap cdata = new HashMap<String Object> ();
      cdata.put("quantity",3);
      Analytics.trackTimedActionUpdate("cartToCheckout", cdata);
      ```

* **trackTimed &#x200B; ActionEnd**

   Avsluta en tidsbestämd åtgärd. Om du anger `block` kan du komma åt de slutliga tidsvärdena och ändra `data` innan du skickar den sista träffen.

   >[!TIP]
   >
   >Om du anger `block` måste du returnera `true` för att skicka en träff. Om du skickar `null` för `block` skickas den sista träffen.

   * Här är syntaxen för den här metoden:

      ```java
      public static void trackTimedActionEnd(String action, TimedActionBlock<Boolean> logic);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.trackTimedActionEnd("cartToCheckout",new
      Analytics.TimedActionBlock<Boolean>(){
          @Override
          public Boolean call(long inAppDuration, long totalDuration, Map<String, Object> contextData) {
              contextData.put("price", 49.95);
              return true;
          }
      });
      ```

* **sendQueuedHits**

   **Kräver SDK 4.1.**

   Oavsett hur många träffar som köas tvingar den här metoden biblioteket att skicka alla träffar i offlinekön.

   * Här är syntaxen för den här metoden:

      ```java
      public static void sendQueuedHits();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.sendQueuedHits();
      ```

* **getQueueSize**

   Returnerar antalet lagrade spårningsanrop i offlinekö.

   * Här är syntaxen för den här metoden:

      ```java
      public static long getQueueSize();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      long queueSize = Analytics.getQueueSize();
      ```

* **clearQueue**

   Tar bort alla träffar från offlinekön.

   * Här är syntaxen för den här metoden:

      ```java
      public static void clearQueue();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.clearQueue();
      ```

      >[!WARNING]
      >
      > Var försiktig när du rensar kön manuellt. Den här processen kan inte ångras.

* **processReferer**

   Bearbetar referenskampanjdata från Google Play Store för senare användning.

   * Här är syntaxen för den här metoden:

      ```java
      public static void processReferrer(final Context context, final Intent intent);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.processReferrer(getApplicationContext(), intent);
      ```

* **processGooglePlayInstallReferrerUrl**

   >[!IMPORTANT]
   >
   > Detta API är tillgängligt från och med SDK version 4.18.0

   Hämtar förvärvsdata från angiven Google Play Install Reference URL.

   De data som samlas in från detta API skickas vid installationsträffar som skickas till Analytics och är tillgängliga i Adobe Data Callback.

   Om referensdata redan har samlats in av SDK, kommer ett anrop till den här metoden att resultera i en no-op.

   Mer information om hur du hämtar referenswebbadressen finns i Google-dokumentationen: https://developer.android.com/google/play/installreferrer/library.

   * Här är syntaxen för den här metoden:

      ```java
      public static void processGooglePlayInstallReferrerUrl(final String referrerUrl);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Analytics.processGooglePlayInstallReferrerUrl(referrerUrl);
      ```
