---
description: Det här avsnittet innehåller information om hur du felsöker problem som du kan råka ut för under testning av värvning.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Felsöka förvärvningstestning
topic-fix: Developer and implementation
exl-id: 1ed2ad89-4e89-43da-aa21-f688b4d1c0d1
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Felsöka förvärvningstestning {#troubleshoot-acquisition-testing}

Det här avsnittet innehåller information om hur du felsöker problem som du kan råka ut för under testning av värvning.

* Om inget annat anges bör filen ADBMobleConfig.json placeras i `assets` mapp.

   Namnet är skiftlägeskänsligt, så använd inte versaler eller gemener.

* Se till att `Config.setContext(this.getApplicationContext())` anropas från din huvudaktivitet.

   Mer information finns i [Konfigurationsmetoder](../configuration/methods.md).

* Kontrollera att de behörigheter som krävs för Mobile SDK finns i `AndroidManifest.xml` fil:

   ```html
   <manifest ..>
   ... 
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   </manifest>
   ```

* Om `referrerTimeout` är inställt på 5 i ADMobilConfig.json-filen. Du måste skicka installationsmetoden inom en femsekundersperiod efter att programmet installerades och startades för första gången för att se referensinformationen som bifogas till installationsträffen.

   För manuell testning rekommenderar vi att du ökar `referrerTimeout` till 10-15 sekunder, så att du har tillräckligt med tid för att skicka information om referenten innan installationsträffen behandlas.

* Kör alla steg i [Testa Marketing Link-förvärv](t-testing-marketing-link-acquisition.md) och se till att du kör `adb shell` först och sedan följande:

   ```java
   am broadcast -a com.android.vending.INSTALL_REFERRER -n nl.postnl.app/.tracking.AdobeAcquisitionLinkBroadcastReceiver --es "referrer" "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<the newly generated id at step #7>"
   ```

>[!IMPORTANT]
>
>Om du vill bearbeta referensmetoden korrekt måste du köra dessa två kommandon oberoende av varandra. Annars `adb` kommer att göra att refererarinformationen kan kringgås och de data som tas emot av sändningsmottagaren blir ofullständiga.
