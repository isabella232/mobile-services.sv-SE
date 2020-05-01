---
description: Här är en lista över metoder som finns i Android-biblioteket.
keywords: android;library;mobile;sdk
seo-description: Här är en lista över metoder som finns i Android-biblioteket.
seo-title: Konfigurationsmetoder
solution: Marketing Cloud,Analytics
title: Konfigurationsmetoder
topic: Developer and implementation
uuid: 663aeb6c-1b97-4a3a-8c0e-dd4c2ec28c01
translation-type: tm+mt
source-git-commit: dae60a21286edc28c84b7638da214b824abf0cd3

---


# Konfigurationsmetoder{#configuration-methods}

Här är en lista över metoder som finns i Android-biblioteket.

## Inledande konfiguration {#section_9169243ECC4744A899A8271F92090ECD}

Följande metod måste anropas en gång i huvudaktivitetens `onCreate` metod:

* `setContext`
Här är kodexemplet för den här metoden:

   ```java
    @Override
    public void onCreate(BundlesavedInstanceState){
      super.onCreate(savedInstanceState)
      setContentView(R.layout.main);
      Config.setContext(this.getApplicationContext());
    }
   ```

## SDK-inställningar (Config-klass) {#section_C1EB977043C04D2B93E5A63DB72828B6}

* **registerAdobeDataCallback**

   * Registrerar ett objekt som implementerar `AdobeDataCallback` gränssnittet. Den överskrivna anropsmetoden anropas med ett `Config.MobileDataEvent` värde och associerade data i en `Map<String, Object>` för den utlösande händelsen. Mer information om vilka händelser som utlöser det här återanropet finns i *MobileDataEventEnum* längst ned i det här avsnittet.

      >[!TIP]
      >
      >Den här metoden kräver version 4.9.0 eller senare.

   * Här är syntaxen för den här metoden:

      ```java
      public static void registerAdobeDataCallback(final AdobeDataCallback&amp;nbsp;callback);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
        Config.registerAdobeDataCallback(new Config.AdobeDataCallback() {
          @Override
          public void call(Config.MobileDataEvent event, Map<String, Object> contextData) {
              // handle each event type accordingly 
              if (event == Config.MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL) {
                   // do something with acquisition data found in contextData parameter
                   HashMap<String, Object> acquisitionData = new HashMap<String, Object>(contextData);
              }
          }
      });
      ```

* **getVersion**

   * Returnerar den aktuella versionen av Adobe Mobile-biblioteket.
   * Här är syntaxen för den här metoden:

      ```java
      public static String getVersion();
      ```

   * Här följer ett kodexempel för den här metoden:

      ```java
      String libraryVersion = Config.getVersion(); 
      ```

* **getPrivacyStatus**

   * Returnerar den uppräknade representationen av den aktuella användarens sekretessstatus.

      Här är sekretessstatusvärdena:

      * `MOBILE_PRIVACY_STATUS_OPT_IN`, där träffar skickas omedelbart.
      * `MOBILE_PRIVACY_STATUS_OPT_OUT`, där de tas bort.
      * `MOBILE_PRIVACY_STATUS_UNKNOWN`, där din rapportsvit är tidsstämpel aktiverad, kommer träffar att sparas tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla dig (träffar tas bort).

         Om rapportsviten inte är tidsstämpelaktiverad, kommer träffar att tas bort tills sekretessstatusen ändras för att anmäla sig. Standardvärdet anges i `ADBMobileConfig.json` filen.
   * Här är syntaxen för den här metoden:

      ```java
      public static MobilePrivacyStatus getPrivacyStatus(); 
      ```

   * Här följer ett kodexempel för den här metoden:

      ```java
      MobilePrivacyStatus privacyStatus Config.getPrivacyStatus();
      ```


* **setPrivacyStatus**

   * Anger sekretessstatus för den aktuella användaren till `status`.

      Du kan ange sekretessstatus till något av följande värden:
      * `MOBILE_PRIVACY_STATUS_OPT_IN`, där träffar skickas omedelbart. De här träffarna skickas omedelbart.
      * `MOBILE_PRIVACY_STATUS_OPT_OUT`, där de tas bort. De här träffarna ignoreras.
      * `MOBILE_PRIVACY_STATUS_UNKNOWN`, där din rapportsvit är tidsstämpel aktiverad, kommer träffar att sparas tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla dig (träffar tas bort).
Om rapportsviten inte är tidsstämpelaktiverad, kommer träffar att tas bort tills sekretessstatusen ändras för att anmäla sig.
   * Här är syntaxen för den här metoden:

      ```java
      public static void setPrivacyStatus(MobilePrivacyStatus status); 
      ```

   * Här följer ett kodexempel för den här metoden:

      ```java
      Config.setPrivacyStatus(MobilePrivacyStatus.MOBILE_PRIVACY_STATUS_OPT_IN); 
      ```


* **getLifetimeValue**

   * Returnerar livstidsvärdet för den aktuella användaren. Standardvärdet är `0`.

   * Här är syntaxen för den här metoden:

      ```java
      public static BigDecimal getLifetimeValue();
      ```

   * Här följer ett kodexempel för den här metoden:

      ```java
      BigDecimal currentLifetimeValue Config.getLifetimeValue(); 
      ```

* **getUserIdentifier**

   * Om en anpassad identifierare har angetts returneras den anpassade användaridentifieraren. Om ingen anpassad identifierare har angetts returneras den `null`. Standardvärdet är `null`.

      >[!TIP]
      >
      >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas det tidigare anpassade eller automatiskt genererade besökar-ID:t och lagras som en anpassad användaridentifierare. Detta bevarar besöksdata mellan SDK-uppgraderingar. För nya installationer på 4.x SDK är användaridentifieraren `null`tills den är inställd.

   * Här är syntaxen för den här metoden:

      ```java
      public static String&amp getUserIdentifier();
      ```

   * Här följer kodexemplet för den här metoden:

      ```java
      String userId = Config.getUserIdentifier();
      ```

* **setUserIdentifier**

   * Anger användaridentifieraren till `identifier`.
   * Här är syntaxen för den här metoden:

      ```java
      public static void setUserIdentifer(String identifier);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.setUserIdentifier("billybob"); 
      ```

* **getDebugLogging**

   * Returnerar den aktuella inställningen för felsökningsloggning. Standardvärdet är `false`.
   * Här är syntaxen för den här metoden:

      ```java
      public static Boolean getDebugLogging(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Boolean debugging = Config.getDebugLogging(); 
      ```

* **setDebugLogging**
   * Anger loggningsinställningar för felsökning till `debugLogging`.
   * Här är syntaxen för den här metoden:

      ```java
      public static void setDebugLogging(Boolea debugLogging);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.setDebugLogging(true);
      ```

* **collectLifecycleData**
   * Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/android/configuration/methods.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void collectLifecycleData(final Activity activity,final Map<String, Object>contextData); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      @Override
      protectedvoid  onResume()  {
        super.onResume();
        Config.collectLifecycleData(this);
        } 
      ```

      Med extra kontextdata:

      ```java
      @Override
      public  void  onResume()  {
        HashMap<String, Object> contextData = new HashMap<String, Object>();
        contextData.put("myapp.category", "Game");        Config.collectLifecycleData(this, contextData);} 
      ```

* **collectLifecycleData (aktivitet)**

   * (**version 4.2 eller senare**) Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelvärden](/help/android/metrics.md).
   * Här är syntaxen för den här metoden:

      ```java
      public static void collectLifecycleData(final Activity activity);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      @Overrideprotected void onResume() {
        super.onResume()
        // assume being called in an Activity class Config.collectLifecycleData(this);
        } 
        ```
      
* **pauseCollecting &#x200B; LifecycleData**

   * Anger för SDK att din app är pausad, så att livscykelvärdena beräknas korrekt. En tidsstämpel `onPause` samlas till exempel in för att bestämma den föregående sessionslängden. Detta anger också en flagga så att livscykeln vet att appen inte kraschade. Mer information finns i [Livscykelvärden](/help/android/metrics.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void pauseCollectingLifecycleData(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      @Override
      protected void onPause() {
        super.onPause();
        Config.pauseCollectingLifecycleData();
      } 
      ```

* **setSmallIconResourceId(int resourceId)**

   * (**version 4.2 eller senare**) Anger den lilla ikon som ska användas för meddelanden som har skapats av SDK. Den här ikonen visas i statusfältet och är den sekundära bilden som visas när användaren ser det fullständiga meddelandet i meddelandecentret.
   * Här är syntaxen för den här metoden:

      ```java
      public static void setSmallIconResourceId(final int resourceId); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.setSmallIconResourceId(R.drawable.appIcon);
      ```

* **setLargeIconResourceId(int resourceId)**

   * (**version 4.2 eller senare**) Anger den stora ikon som ska användas för meddelanden som skapats av SDK. Den här ikonen är den primära bilden som visas när användaren ser det fullständiga meddelandet i meddelandecentret.
   * Här är syntaxen för den här metoden:

      ```java
      public static void setLargeIconResourceId(final int  resourceId);
      ```

   * Här är kodexemplet för den här metoden:

      ```Java
      Config.setLargeIconResourceId(R.drawable.appIcon);
      ```

* **overrideConfigStream(InputStream configInput)**

   * (**version 4.2 eller senare**) Gör att du kan läsa in en annan ADBMomobile JSON-konfigurationsfil när programmet startas. Den olika konfigurationen används tills programmet stängs.
   * Här är syntaxen för den här metoden:

      ```java
      public static void overrideConfigStream(final InputStream configInput);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
       try {
          InputStream configInput = getAssets().open("ExampleJSONFile.json") 
          Config.overrideConfigStream(configInput)
          } catch (IOException ex) { 
          //do something with the exception if needed
      }
      ```

* **setPushIdentifier**

   * Anger enhetstoken för push-meddelanden.
   * Här är syntaxen för den här metoden:

      ```java
      public static void setPushIdentifier(final String registrationId); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ...// note the code to retreive the push token must run in the background
      InstanceID instanceID= InstanceID.getInstance(getApplicationContext());String token=instanceID.getToken("835015092242", GoogleCloudMessaging.INSTANCE_ID_SCOPE null);Config.setPushIdentifier(token);
      ...
      ```

* **submitAdvertisingIdentifierTask**

   * Ger SDK:n ett anrop som returnerar den sträng med annonsidentifieraren som returneras från Google Play Services. SDK kör den här aktiviteten på en bakgrundstråd och ställer in en intern variabel för Advertising Identifier som baseras på värdet som returneras från anropsfunktionen.

      >[!IMPORTANT]
      > 
      >Om du vill använda Advertising Identifier i Acquisition eller Lifecycle anropar du den innan du ringer `Config.collectLifecycleData`.

      * Här är syntaxen för den här metoden:

         ```java
         public static void submitAdvertisingIdentifierTask(final Callable<String> task); 
         ```

      * Här är kodexemplet för den här metoden:

         ```java
         @Override
         public void  onResume() {
             super.onResume();
             final  Callable<String>; task = new Callable<String>(){
                 @Override
                 public String call() throws Exception {
                    AdvertisingIdClient.Info idInfo;
                    String adid = null;
                    Context appContext = CLASSNAME.this.getApplicationContext();
                    try {
                         idInfo = AdvertisingIdClient.getAdvertisingIdInfo(appContext);
                         if (idInfo != null) { 
                             adid = idInfo.getId();
                         } 
                    } catch  (Exception ex) {
                        Log.e("Error",  ex.getLocalizedMessage());
                    }
                    return  adid;
                 }
           };
           Config.submitAdvertisingIdentifierTask(task); 
           Config.collectLifecycleData(this);
         }
         ```


## Gränssnitt för AdobeDataCallback {#section_600A63B3136F47DCB928071485C5117C}

```java
public interface AdobeDataCallback {  
    void call(MobileDataEvent event, Map<String, Object> contextData);  
} 
```

## MobileDataEvent Enum {#section_92732814141646E294782BC9020367EB}

```java
public enum MobileDataEvent {  
    MobileDataEvent.MOBILE_EVENT_LIFECYCLE, // triggers on a lifecycle hit  
    MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL, // triggers on a app install that has acquisition data  
    MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH // triggers on launch when the device previously installed via acquisition  
}
```
