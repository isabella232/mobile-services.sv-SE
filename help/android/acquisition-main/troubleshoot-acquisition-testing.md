---
description: Det här avsnittet innehåller information om hur du felsöker problem som du kan råka ut för under testning av värvning.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Felsöka förvärvningstestning
topic-fix: Developer and implementation
exl-id: 1ed2ad89-4e89-43da-aa21-f688b4d1c0d1
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Felsöka förvärvningstestning {#troubleshoot-acquisition-testing}

Det här avsnittet innehåller information om hur du felsöker problem som du kan råka ut för under testning av värvning.

* Om inget annat anges bör filen ADBMobleConfig.json placeras i mappen `assets`.

   Namnet är skiftlägeskänsligt, så använd inte versaler eller gemener.

* Kontrollera att `Config.setContext(this.getApplicationContext())` anropas från huvudaktiviteten.

   Mer information finns i [Konfigurationsmetoder](../configuration/methods.md).

* Kontrollera att den behörighet som krävs för Mobile SDK finns i `AndroidManifest.xml`-filen:

   ```html
   <manifest ..>
   ... 
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   </manifest>
   ```

* Om `referrerTimeout` är inställt på 5 i ADMobilConfig.json-filen måste du skicka installationsmetoden inom fem sekunder efter att programmet installerats och startats för första gången för att se referensinformationen som bifogas till installationsträffen.

   För manuell testning rekommenderar vi att du ökar `referrerTimeout` till 10-15 sekunder, så att du har tillräckligt med tid för att skicka information om referenten innan installationsträffen bearbetas.

* Kör alla steg i [Testa Marketing Link-förvärv](t-testing-marketing-link-acquisition.md) och kontrollera att du kör kommandot `adb shell` först och sedan följande:

   ```java
   am broadcast -a com.android.vending.INSTALL_REFERRER -n nl.postnl.app/.tracking.AdobeAcquisitionLinkBroadcastReceiver --es "referrer" "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<the newly generated id at step #7>"
   ```

>[!IMPORTANT]
>
>Om du vill bearbeta referensmetoden korrekt måste du köra dessa två kommandon oberoende av varandra. I annat fall kommer `adb` att dubbla escape-värden för referensinformationen och data som tas emot av sändningsmottagaren blir ofullständiga.
