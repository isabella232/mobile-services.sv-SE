---
description: Följande information hjälper dig att felsöka problem med förvärvstestning.
keywords: android;Förvärv;testning
solution: Experience Cloud Services,Analytics
title: Felsökning av värvningstestning
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
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

* I konfigurationen, om referensens timeout är inställd på `referrerTimeout: 5`innebär det att du måste skicka installationsavgivningen inom fem sekunder efter att programmet installerades och startades för första gången för att se referensinformationen som bifogas till installationsträffen.

   För manuell testning kan du öka `referrerTimeout` till 10-15 sekunder, så att det finns tillräckligt med tid för att skicka information om referenten innan installationsträffen behandlas.

* Det är viktigt att du kör alla steg i [Testa Marketing Link-förvärv](t-t-testing-marketing-link-acquisition.md) i ordning och se till att du kör `adb` skal och sedan följande:

   ```java
   am broadcast -a com.android.vending.INSTALL_REFERRER -n 
   nl.postnl.app/.tracking.AdobeAcquisitionLinkBroadcastReceiver --es "referrer"
   "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<the newly generated id at step #7>"
   ```

>[!IMPORTANT]
>
>Du måste köra dessa två kommandon oberoende av varandra för att behandla referensmetoden korrekt.  I annat fall `adb` &quot;double&quot;-konvertering&quot; tar bort referensinformationen och de data som tas emot av sändningsmottagaren blir ofullständiga.
