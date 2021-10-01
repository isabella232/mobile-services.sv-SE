---
description: Följande information hjälper dig att felsöka problem med förvärvstestning.
keywords: android;Förvärv;testning
solution: Experience Cloud,Analytics
title: Felsökning av värvningstestning
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Felsökning av värvningstestning {#aquistion-testing-troubleshooting}

Här är några problem som du kan stöta på när du testar förvärvet och några möjliga lösningar:

* Om inget annat anges bör filen ADBMobilConfig.json placeras i mappen assets.

* Namnet är skiftlägeskänsligt, så ange inget namn med gemener.

   Du måste se till att `Config.setContext(this.getApplicationContext())` anropas från huvudaktiviteten. Mer information finns i [Konfigurationsmetoder](../configuration/methods.md).

* Det saknas ett fåtal användarbehörigheter i den angivna AndroidManifest.xml-filen. Dessa krävs för att skicka data och registrera anrop för offlinespårning:

   ```html
   <manifest..>
   ... 
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   </manifest>
   ```

* Om referenspunktens timeout är inställd på `referrerTimeout: 5` betyder det i konfigurationen att du måste skicka installationsmetoden inom en femsekundersperiod efter att programmet installerats och startats för första gången för att se referensinformationen som bifogas till installationsträffen.

   För manuell testning ökar du `referrerTimeout` till 10-15 sekunder, så att det finns tillräckligt med tid för att skicka referensinformation innan installationsträffen behandlas.

* Det är viktigt att du kör alla steg i [Testing Marketing Link-förvärv](t-t-testing-marketing-link-acquisition.md) för att kontrollera att du kör `adb`-gränssnittet och sedan följande:

   ```java
   am broadcast -a com.android.vending.INSTALL_REFERRER -n 
   nl.postnl.app/.tracking.AdobeAcquisitionLinkBroadcastReceiver --es "referrer"
   "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<the newly generated id at step #7>"
   ```

>[!IMPORTANT]
>
>Du måste köra dessa två kommandon oberoende av varandra för att behandla referensmetoden korrekt.  I annat fall kommer `adb`-dubbel att kringgå referensinformationen och data som tas emot av sändningsmottagaren blir ofullständiga.
