---
description: Det här avsnittet innehåller information om hur du felsöker problem som du kan råka ut för under testning av värvning.
keywords: android;library;mobile;sdk
seo-description: Det här avsnittet innehåller information om hur du felsöker problem som du kan råka ut för under testning av värvning.
seo-title: Felsöka förvärvningstestning
solution: Experience Cloud,Analytics
title: Felsöka förvärvningstestning
topic: Developer and implementation
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Felsöka förvärvningstestning {#troubleshoot-acquisition-testing}

Det här avsnittet innehåller information om hur du felsöker problem som du kan råka ut för under testning av värvning.

* Om inget annat anges bör filen ADBMobilConfig.json placeras i `assets` mappen.

   Namnet är skiftlägeskänsligt, så använd inte versaler eller gemener.

* Se till att du `Config.setContext(this.getApplicationContext())` anropas från huvudaktiviteten.

   Mer information finns i [Konfigurationsmetoder](https://docs.adobe.com/content/help/en/mobile-services/android/configuration-android/methods.html).

* Kontrollera att det finns nödvändiga behörigheter för Mobile SDK i `AndroidManifest.xml` filen:

   ```html
   <manifest ..>
   ... 
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   </manifest>
   ```

* Om inställningen `referrerTimeout` är 5 i ADMobilConfig.json-filen måste du skicka installationsmetoden inom fem sekunder efter att programmet installerats och startats för första gången för att se referensinformationen som bifogas till installationsträffen.

   För manuell testning rekommenderar vi att du ökar antalet `referrerTimeout` till 10-15 sekunder, så att du har tillräckligt med tid för att skicka information till referenten innan installationsträffen behandlas.

* Kör alla steg i [Testing Marketing Link och kontrollera att du kör](https://docs.adobe.com/content/help/en/mobile-services/android/acquisition-android/t-testing-marketing-link-acquisition.html) `adb shell` kommandot först och sedan följande:

   ```java
   am broadcast -a com.android.vending.INSTALL_REFERRER -n nl.postnl.app/.tracking.AdobeAcquisitionLinkBroadcastReceiver --es "referrer" "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<the newly generated id at step #7>"
   ```

>[!IMPORTANT]
>
>Om du vill bearbeta referensmetoden korrekt måste du köra dessa två kommandon oberoende av varandra. I annat fall `adb` kommer dubbelt så mycket information att kringgå referensinformationen och de data som tas emot av sändningsmottagaren blir ofullständiga.

