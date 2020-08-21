---
description: Förvärvningslänkar med unika spårningskoder kan genereras i Adobe Mobile-tjänster. När en användare hämtar och kör en app från App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar hämtningsdata till Adobe Mobile-tjänster.
keywords: android;library;mobile;sdk
seo-description: Förvärvningslänkar med unika spårningskoder kan genereras i Adobe Mobile-tjänster. När en användare hämtar och kör en app från App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar hämtningsdata till Adobe Mobile-tjänster.
seo-title: Mobilförvärv
solution: Marketing Cloud,Analytics
title: Mobilförvärv
topic: Developer and implementation
uuid: 4d32eae9-e856-4e40-8a29-2b5bccd106e0
translation-type: tm+mt
source-git-commit: 7ae626be4d71641c6efb127cf5b1d3e18fccb907
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 1%

---


# Mobile app acquisition {#mobile-app-acquisition}

Förvärvningslänkar med unika spårningskoder kan genereras i Adobe Mobile-tjänster. När en användare hämtar och kör en app från App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar hämtningsdata till Adobe Mobile-tjänster.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
>Om du vill använda förvärvet **måste** du ha SDK version 4.1 eller senare.

Förvärvningslänkar måste skapas i Adobe Mobile-tjänster. Mer information finns i [Anskaffning](/help/using/acquisition-main/acquisition-main.md).

**I SDK version 4.18.0 och senare**:

Från och med 1 mars 2020 har Google ersatt sändningsmekanismen install_reference. Mer information finns i [Använda InstallBroadcast? Växla till API:t Play Reference senast 1 mars 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html). Om du vill fortsätta samla in installationsreferensinformation från Google Play-butiken uppdaterar du programmet till SDK version 4.18.0 eller senare.

I stället för att skapa en `BroadcastReceiver`behöver du med den borttagna versionen samla in URL:en för installationsreferenten från ett nytt Google API och skicka den resulterande URL:en till SDK:n.

1. Lägg till paketet Google Play Install Reference i din gradle-fils beroenden:

   `implementation 'com.android.installreferrer:installreferrer:1.1'`

1. Om du vill hämta referenswebbadressen från installationsreferensens API, slutför du stegen i [Hämta installationsreferenten](https://developer.android.com/google/play/installreferrer/library#install-referrer).

1. Skicka referenswebbadressen till SDK:

   `Analytics.processGooglePlayInstallReferrerUrl(referrerUrl);`

>[!IMPORTANT]
>
>För att undvika onödiga API-anrop i appen rekommenderar Google att du bara anropar API:t en gång omedelbart efter installationen.

Information om hur du bäst använder Google Play Install Referrer-API:er för installation i din app finns i dokumentationen för Google. Här följer ett exempel på hur du använder Adobe SDK med Google Play Install Reference-API:erna:

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

Om du inte kan använda de förvärvslänkar som har skapats i Adobe Mobile Services kan förvärvsdata fortfarande samlas in och skickas av SDK med Google Play Acquisition.

Så här samlar du in inhämtningsdata från en Google Play Acquisition-kampanj:

* Använd den vanliga förvärvsmetoden för Google Play Store.

   Anpassade inhämtningsdata kan användas med standardvärdepar för Google Play Acquisition.

* När användaren hämtar och kör en app som ett resultat av en Google Play-butik samlas data från referenten in och skickas till Adobe Mobile Services.

   * Data lagras och är tillgängliga i den `AdobeDataCallback` instans som registrerades tidigare med SDK:n.

      Mer information finns i [Konfigurationsmetoder](/help/android/configuration/methods.md).

   * Händelsetypen `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` eller `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` händelsetypen används.

   * Anpassade nycklar som var en del av hämtningsdata från Google Play kommer att namnfördelas med &quot; `a.acquisition.custom.`&quot;

Om du använder förvärvslänkarna som skapades på Adobe Mobile Services lägger du till anpassade data till hämtningslänken genom att utföra följande uppgifter:

1. Lägg till en förvärvsvariabel som prefix med &quot; `adb`&quot;.

   När SDK tar emot förvärvsdata från Adobe Mobile Services vid första starten lagras data och är tillgängliga i den `AdobeDataCallback` instans som registrerats tidigare med SDK. Mer information finns i [Konfigurationsmetoder](/help/android/configuration/methods.md).

1. Händelsetypen `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` eller `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` händelsetypen kommer att användas.

1. De anpassade datanycklarna har prefixet &quot;`a.acquisition.custom.`&quot;

>[!TIP]
>
>Om du skickar data till flera rapportsviter ska du använda förvärvsdata från appen som är kopplad till den första rapportsviten i din lista över rapportsvitens-ID:n.

Uppdateringarna i det här avsnittet gör det möjligt för SDK att skicka förvärvsdata från en länk.

## Spåra mobilförvärv {#section_CEA30C652AC8470784B8054E299B80FA}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Implementera `BroadcastReceiver` för referenten:

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

1. Uppdatera `AndroidManifest.xml` för att aktivera `BroadcastReceiver` det som skapades i föregående steg:

   ```xml
   <receiver android:name="com.your.package.name.GPBroadcastReceiver" android:exported="true">
    <intent-filter>
     <action android:name="com.android.vending.INSTALL_REFERRER" />
    </intent-filter>
   </receiver>
   ```

1. Kontrollera att `ADBMobileConfig.json` filen innehåller de hämtningsinställningar som krävs:

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

   Inställningarna `acquisition` genereras av Adobe Mobile-tjänsterna och bör inte ändras. Mer information om hur du hämtar en anpassad `ADBMobileConfig.json` fil med förkonfigurerade `acquisition` inställningar finns i [Innan du börjar](/help/android/getting-started/requirements.md).

När dessa inställningar har aktiverats skickas kundvärvningsdata automatiskt med det inledande livscykelanropet efter att appen startades första gången.

>[!CAUTION]
>
>`referrerTimeout` måste anges till ett högre värde än 0 för att appinhämtning ska kunna aktiveras.
