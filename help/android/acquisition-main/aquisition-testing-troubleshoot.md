---
description: Följande information hjälper dig att felsöka problem med förvärvstestning.
keywords: android;Acquisition;testing
seo-description: Följande information hjälper dig att felsöka problem med förvärvstestning.
seo-title: Felsökning av värvningstestning
solution: Experience Cloud,Analytics
title: Felsökning av värvningstestning
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Felsökning av värvningstestning {#aquistion-testing-troubleshooting}

Här är några problem som du kan stöta på när du testar förvärvet och några möjliga lösningar:

* Om inget annat anges bör filen ADBMobilConfig.json placeras i mappen assets.

* Namnet är skiftlägeskänsligt, så ange inget namn med gemener.

   Du måste se till att `Config.setContext(this.getApplicationContext())` anropas från huvudaktiviteten. Mer information finns i [Konfigurationsmetoder](https://docs.adobe.com/content/help/en/mobile-services/android/configuration-android/methods.html).

* Det saknas ett fåtal användarbehörigheter i den angivna AndroidManifest.xml-filen. Dessa krävs för att skicka data och registrera anrop för offlinespårning:

   ```html
   <manifest..>
   ... 
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   </manifest>
   ```

* Om timeout-inställningen för referenten är inställd på `referrerTimeout: 5`i konfigurationen, innebär det att du måste skicka installationsmetoden inom en femsekundersperiod efter att programmet installerats och startats för första gången för att se referensinformationen som bifogas till installationsträffen.

   För manuell testning ökar du antalet sekunder `referrerTimeout` till 10-15 sekunder, så att det finns tillräckligt med tid för att skicka information till referenten innan installationsträffen behandlas.

* Det är viktigt att du kör alla steg i [Testing Marketing Link-förvärv](https://docs.adobe.com/content/help/en/mobile-services/android/acquisition-android/t-testing-marketing-link-acquisition.html) för att kontrollera att du kör `adb` gränssnittet och sedan följande:

   ```java
   am broadcast -a com.android.vending.INSTALL_REFERRER -n 
   nl.postnl.app/.tracking.AdobeAcquisitionLinkBroadcastReceiver --es "referrer"
   "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<the newly generated id at step #7>"
   ```

>[!IMPORTANT]
>
>Du måste köra dessa två kommandon oberoende av varandra för att behandla referensmetoden korrekt.  I annat fall `adb` kommer dubbelt så mycket att gå förbi referensinformationen och de data som tas emot av sändningsmottagaren blir ofullständiga.
