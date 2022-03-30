---
description: Förvärvningslänkar med unika spårningskoder kan genereras i Adobe Mobile-tjänster. När en användare hämtar och kör en app från App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar hämtningsdata till Adobe Mobile-tjänster.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Mobilförvärv
topic-fix: Developer and implementation
uuid: 4d32eae9-e856-4e40-8a29-2b5bccd106e0
exl-id: 266f0266-38f5-410b-ae14-92874fb0e7ce
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Mobile appförvärv {#mobile-app-acquisition}

Förvärvningslänkar med unika spårningskoder kan genereras i Adobe Mobile-tjänster. När en användare hämtar och kör en app från App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar hämtningsdata till Adobe Mobile-tjänster.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
>Om du vill använda förvärvet **måste** har SDK version 4.1 eller senare.

Förvärvningslänkar måste skapas i Adobe Mobile-tjänster. Mer information finns i [Förvärv](/help/using/acquisition-main/acquisition-main.md).

**I SDK version 4.18.0 och senare**:

Från och med den 1 mars 2020 ersätter Google sändningsmekanismen install_reference. Mer information finns i [Använder du fortfarande InstallBroadcast? Växla till API:t Play Reference senast 1 mars 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html). Om du vill fortsätta samla in information om installationsreferenten från Google Play Store måste du uppdatera programmet till SDK version 4.18.0 eller senare.

Med borttagningen i stället för att skapa en `BroadcastReceiver`måste du samla in URL:en för installationsreferenten från ett nytt Google-API och skicka den resulterande URL:en till SDK:n.

1. Lägg till Google Play Install Referrer-paketet i din gradle-fils beroenden:

   `implementation 'com.android.installreferrer:installreferrer:1.1'`

1. Om du vill hämta en referens-URL från API:t för installationsreferenten utför du stegen i [Hämta installationsreferenten](https://developer.android.com/google/play/installreferrer/library#install-referrer).

1. Skicka referenswebbadressen till SDK:

   `Analytics.processGooglePlayInstallReferrerUrl(referrerUrl);`

>[!IMPORTANT]
>
>För att undvika onödiga API-anrop i appen rekommenderar Google att du bara anropar API:t en gång omedelbart efter installationen.

Information om hur du bäst använder Google Play Install Reference API:er i din app finns i Google dokumentation. Här följer ett exempel på hur du använder Adobe SDK med Google Play Install Reference API:er:

```java
void handleGooglePlayReferrer() {
    // Google recommends only calling this API the first time you need it:
    // https://developer.android.com/google/play/installreferrer/library#install-referrer

    // Store a boolean in SharedPreferences to ensure we only call it once.
    final SharedPreferences prefs = getSharedPreferences("acquisition", 0);
    if (prefs != null) {
        if (prefs.getBoolean("referrerHasBeenProcessed", false)) {
            return;
        }
    }

    final InstallReferrerClient referrerClient = InstallReferrerClient.newBuilder(getApplicationContext()).build();
    referrerClient.startConnection(new InstallReferrerStateListener() {
        private boolean complete = false;

        @Override
        public void onInstallReferrerSetupFinished(int responseCode) {
            switch (responseCode) {
                case InstallReferrerClient.InstallReferrerResponse.OK:
                    // connection is established
                    complete();
                    try {
                        final ReferrerDetails details = referrerClient.getInstallReferrer();                        

                        // pass the install referrer url to the SDK
                        Analytics.processGooglePlayInstallReferrerUrl(details.getInstallReferrer());

                    } catch (final RemoteException ex) {
                        Log.w("Acquisition - RemoteException while retrieving referrer information (%s)", ex.getLocalizedMessage() == null ? "unknown" : ex.getLocalizedMessage());
                    } finally {
                        referrerClient.endConnection();
                    }
                    break;
                case InstallReferrerClient.InstallReferrerResponse.FEATURE_NOT_SUPPORTED:
                case InstallReferrerClient.InstallReferrerResponse.SERVICE_UNAVAILABLE:
                default:
                    // API not available in the Play Store app - nothing to do here
                    complete();
                    referrerClient.endConnection();
                    break;
            }
        }

        @Override
        public void onInstallReferrerServiceDisconnected() {
            if (!complete) {
                // something went wrong trying to get a connection, try again
                referrerClient.startConnection(this);
            }
        }

        void complete() {
            complete = true;
            SharedPreferences.Editor editor = getSharedPreferences("acquisition", 0).edit();
            editor.putBoolean("referrerHasBeenProcessed", true);
            editor.apply();
        }
    });
}
```

**I SDK version 4.13.1 och senare**:

Om du inte kan använda de förvärvslänkar som har skapats i Adobe Mobile Services kan förvärvsuppgifterna ändå samlas in och skickas av SDK med hjälp av Google Play Acquisition.

Så här samlar du in inköps-data från en standardkampanj för Google Play Acquisition:

* Använd standardmetoden för förvärv av Google Play Store.

   Anpassade inhämtningsdata kan användas med standardvärdepar för Google Play Acquisition.

* När användaren laddar ned och kör en app som ett resultat av en köp från Google Play Store, samlas data från referenten in och skickas till Adobe Mobile Services.

   * Data lagras och är tillgängliga i `AdobeDataCallback` -instans som registrerades tidigare med SDK.

      Mer information finns i [Konfigurationsmetoder](/help/android/configuration/methods.md).

   * The `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` eller `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` händelsetyp används.

   * Anpassade nycklar som var en del av inhämtningsdata från Google Play namnfördelas med &quot; `a.acquisition.custom.`&quot;

Om du använder förvärvslänkarna som skapades på Adobe Mobile Services lägger du till anpassade data i hämtningslänken genom att utföra följande uppgifter:

1. Lägg till en förvärvsvariabel som prefix med &quot; `adb`&quot;.

   När SDK tar emot förvärvsdata från Adobe Mobile Services vid första starten lagras dessa data och är tillgängliga i `AdobeDataCallback` -instans som registrerades tidigare med SDK. Mer information finns i [Konfigurationsmetoder](/help/android/configuration/methods.md).

1. The `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` eller `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` händelsetypen kommer att användas.

1. De anpassade datanycklarna har prefixet &quot;`a.acquisition.custom.`&quot;

>[!TIP]
>
>Om du skickar data till flera rapportsviter ska du använda förvärvsdata från appen som är kopplad till den första rapportsviten i din lista över rapportsvitens-ID:n.

Uppdateringarna i det här avsnittet gör det möjligt för SDK att skicka förvärvsdata från en länk.

## Spåra mobilförvärv {#section_CEA30C652AC8470784B8054E299B80FA}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Implementera `BroadcastReceiver` för hänvisaren:

   ```java
   package com.your.package.name;  // replace with your app package name
   
   import android.content.BroadcastReceiver;
   import android.content.Context;
   import android.content.Intent;
   
   public class GPBroadcastReceiver extends BroadcastReceiver {
     @Override
     public void onReceive(Context c, Intent i) {
      com.adobe.mobile.Analytics.processReferrer(c, i);
     }
   }
   ```

1. Uppdatera `AndroidManifest.xml` för att aktivera `BroadcastReceiver` som skapades i föregående steg:

   ```xml
   <receiver android:name="com.your.package.name.GPBroadcastReceiver" android:exported="true">
    <intent-filter>
     <action android:name="com.android.vending.INSTALL_REFERRER" />
    </intent-filter>
   </receiver>
   ```

1. Verifiera att `ADBMobileConfig.json` filen innehåller de hämtningsinställningar som krävs:

   ```xml
   "acquisition": {
      "server": "c00.adobe.com",
      "appid": "0652024f-adcd-49f9-9bd7-2552a4565d2f"
   },
   "analytics": {
     "referrerTimeout": 5,
     ...
   ```

   >[!IMPORTANT]
   >
   >Om du skickar data till flera rapportsviter använder du hämtningsinställningarna (hämtningsserver och appid) från appen som är associerad med den första rapportsviten i din lista över rapportsvits-ID:n.

   The `acquisition` inställningarna genereras av Adobe Mobile-tjänster och bör inte ändras. Mer information om hur du hämtar en anpassad `ADBMobileConfig.json` filen med `acquisition` förkonfigurerade inställningar, se [Innan du börjar](/help/android/getting-started/requirements.md).

När dessa inställningar har aktiverats skickas kundvärvningsdata automatiskt med det inledande livscykelanropet efter att appen startades första gången.

>[!CAUTION]
>
>`referrerTimeout` måste anges till ett högre värde än 0 för att appinhämtning ska kunna aktiveras.
