---
description: Den här informationen hjälper dig att skicka en länk till en kampanj för version 3 på en Android-enhet.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Testa version 3 - förvärv
topic-fix: Developer and implementation
uuid: 5e38b43d-389e-4412-99e5-3e6223b6ad28
exl-id: 2ce78e2e-da51-4af8-a461-ec6c642a7854
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# Testar förvärvet av V3 {#testing-version-acquisition}

Den här informationen hjälper dig att skicka en länk till en kampanj för version 3 på en Android-enhet.

>[!IMPORTANT]
>
>Förvärv i V3 avser de förvärvslänkar som du skapar med förvärvsverktyget i användargränssnittet för Mobile-tjänster i Adobe. Om du vill använda den här funktionen måste du uppgradera till Android SDK 4.x för Experience Cloud Solutions 4.6.0 eller senare.

Om mobilappen ännu inte finns i Google Play kan du välja vilken mobilapp som helst som mål när du skapar kampanjlänken. Detta påverkar bara den app som förvärvsservern dirigerar om dig till efter att du klickat på länken, men det påverkar inte möjligheten att testa länken. Frågesträngsparametrar skickas till Google Play Store, som skickas till appen vid installationen som en del av en kampanjsändning. Testning av mobilappsförvärv kräver simulering av den här typen av sändning.

>[!IMPORTANT]
>
>Om du implementerar med Google Play Install Referrer API:er kan du inte testa förvärvet innan appen finns i Google Play Store.

Appen måste vara nyligen installerad eller ha data rensade i **[!UICONTROL Settings]**, varje gång ett test körs. Detta garanterar att de inledande livscykelvärdena som är kopplade till parametrarna för kampanjfrågesträngen skickas när appen startas första gången.

1. Slutför nödvändiga uppgifter i [Mobile App Acquisition](/help/android/acquisition-main/acquisition.md) och se till att du har implementerat sändningsmottagaren korrekt för `INSTALL_REFERRER`.

1. I användargränssnittet för Mobile-tjänster i Adobe klickar du på  **[!UICONTROL Acquisition]** > **[!UICONTROL Marketing Links Builder]** och generera en URL för Acquisition Marketing Link som anger Google Play som mål för Android-enheter.

   Mer information finns i [Marketing Links Builder](/help/using/acquisition-main/c-marketing-links-builder/c-marketing-links-builder.md).

   Exempel, `https://c00.adobe.com/v3/<appid>/start?a_i_id=iostestapp&a_g_id=com.adobe.android&a_dd=g&ctxa.referrer.campaign.name=name&ctxa.referrer.campaign.trackingcode=trackingcode`.

   >[!TIP]
   >
   >Om du refererar till både Android- och iOS-appar i förvärvslänken använder du Google Play som standardbutik.

1. Öppna den genererade länken i en webbläsare.

   Du bör omdirigeras till en sida med en URL som liknar följande exempel:
   `https://play.google.com/store/apps/details?id=com.adobe.android&referrer=utm_campaign%3Dadb_acq_v3%26utm_source%3Dadb_acq_v3%26utm_content%3D91b52ce097b1464b9b47cb2995c493cc6ab2c3a3`

1. Kopiera det unika ID:t efter `utm_content%3D`.

   I föregående exempel är ID:t `91b52ce097b1464b9b47cb2995c493cc6ab2c3a3`.

1. Skapa länken för kundvärvningen genom att använda det unika ID:t från steg 3 med följande format:

   `https://c00.adobe.com/v3/<appid>/end?a_ugid=<unique id>`.

   Exempel, `https://c00.adobe.com/v3/<appid>/end?a_ugid=91b52ce097b1464b9b47cb2995c493cc6ab2c3a3`.

1. Öppna länken i en webbläsare.

   Du borde se `contextData` i JSON-svaret:

   `{"fingerprint":"228d7e6058b1d731dc7a8b8bd0c15e1d78242f31","timestamp":1457989293,"appguid":"","contextData":{"a.referrer.campaign.name":"name","a.referrer.campaign.trackingcode":"trackingcode"}}.`

   Om du inte ser `contextData`, eller en del av strängen saknas, kontrollera att hämtnings-URL:en följer formatet i [Skapa förvärvningslänk manuellt](/help/using/acquisition-main/c-marketing-links-builder/acquisition-link-manual.md).
1. Upprepa steg 3 för att få ett nytt unikt ID.
1. Kontrollera att följande inställningar i konfigurationsfilen är korrekta:

   | Inställning | Värde |
   |--- |--- |
   | förvärv | Servern bör vara `c00.adobe.com`.   *`appid`*  ska vara lika med `appid`  på er förvärvslänk. |
   | analys | För testningsändamål ställer du in att referenspunktens tidsgräns ska tillåta tillräckligt med tid (60 sekunder eller mer) för att skicka sändningen manuellt. Du kan återställa den ursprungliga timeout-inställningen efter testningen. |

1. Anslut enheten till en dator, avinstallera och installera programmet igen.
1. Starta ADB Shell och starta programmet på enheten.
1. Skicka en sändning med följande `adb` kommando:

   `am broadcast -a com.android.vending.INSTALL_REFERRER -n com.adobe.android/com.adobe.android.YourBroadcastReceiver --es "referrer" "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<unique id get on step 5>"`

1. Utför följande steg:
   1. Ersätt `com.adobe.android` med programmets paketnamn.
   1. Uppdatera mottagarreferensen med den för var kampanjspårningsmottagaren finns i din app
   1. Ersätt värden som är kopplade till `utm_content`.

   Om sändningen lyckas kan du förvänta dig ett svar som liknar följande exempel:

   ```
   Broadcasting: Intent
   { act=com.android.vending.INSTALL_REFERRER cmp=com.adobe.adms.tests/.ReferralReceiver (has extras) }
   Broadcast completed: result=0
   ```

1. (Valfritt) Du kan aktivera felsökningsloggning av SDK för att få ytterligare information.

   Om allt fungerar som det ska bör du se följande loggar:

`"Analytics - Received referrer information(<referrer content>)"   "Analytics - Trying to fetch referrer data from (acquisition end url)"; "Analytics - Received Referrer Data(<A JSON Response>)"`

Om du inte ser loggarna ovan kontrollerar du att du har slutfört steg 6 till 12.

Följande tabell innehåller ytterligare information om möjliga fel:

| Fel | Beskrivning |
|--- |--- |
| Analys - Det går inte att avkoda svar(*Sträng*). | Svaret har fel format. |
| Analys - Det gick inte att analysera svaret (*ett JSON-svar*). | JSON-strängen har fel format. |
| Analys - Det går inte att parsa ett svar på en förvärvstjänst (ingen contextData-parameter i svaret). | Det finns ingen contextData-parameter i svaret. |
| Analys - data för inköpsorderreferensen var inte fullständiga (ingen `a.referrer.campaign.name` i kontextdata), ignorerar. | `a.referrer.campaign.name`  ingår inte i contextData. |
| Analys - Anskaffningsreferenten nådde tidsgränsen. | Det gick inte att hämta svaret inom den tid som definierats av `referrerTimeout`. Öka värdet och försök igen.  Du bör även kontrollera att du har öppnat förvärvningslänken innan du installerar appen. |

Kom ihåg följande information:

* Hits som skickas från appen kan övervakas med HTTP-övervakningsverktyg för att verifiera förvärvsattribueringen.
* Mer information om hur du sänder `INSTALL_REFERRER`, se [Testa Google Play Campaign Measurement](https://developers.google.com/analytics/solutions/testing-play-campaigns) i Google Developers Guide.

* En felkorrigering släpptes för förvärv på Android 4.8.2.

   Uppgradera SDK till den senaste versionen innan du testar.

* Du kan använda följande `acquisitionTest.jar` Java-verktyget hjälper dig att få det unika ID:t och broadcast-installationsprogrammet, som i sin tur hjälper dig att få information i steg 3 till 12.

   **Installera Java-verktyget**

Så här installerar du Java-verktyget:

1. Ladda ned [`acquisitionTester.zip`](/help/android/assets/acquisitionTester.zip) -fil.

1. Extrahera .jar-filen.

   Du kan köra filen på kommandoraden.

   Exempel:

   ```java
   java -jar acquisitionTester.jar -a com.adobe.test -r com.adobe.test.ReferrerReceiver -l "https://c00.adobe.com/v3/appid/start?a_i_id=123456&a_g_id=com.adobe.test&a_dd=i&ctxa.referrer.campaign.name=name&ctxa.referrer.campaign.trackingcode=1234
   ```
