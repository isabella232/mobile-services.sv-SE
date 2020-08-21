---
description: Följande instruktioner hjälper dig att skicka en kundvärvningskampanj via en Marketing Link på en Android-enhet.
keywords: android;library;mobile;sdk
seo-description: Följande instruktioner hjälper dig att skicka en kundvärvningskampanj via en Marketing Link på en Android-enhet.
seo-title: Testar anskaffning av marknadsföringslänk
solution: Marketing Cloud,Analytics
title: Testar anskaffning av marknadsföringslänk
topic: Developer and implementation
uuid: d0933dcc-8fc3-4f60-987f-7a54559aacf5
translation-type: tm+mt
source-git-commit: 7ae626be4d71641c6efb127cf5b1d3e18fccb907
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# Testa Marketing Link-förvärv {#testing-marketing-link-acquisition}

Följande instruktioner hjälper dig att skicka en kundvärvningskampanj via en Marketing Link på en Android-enhet.

Om din mobilapp ännu inte finns i Google Play kan du välja vilken mobilapp som helst som mål när du skapar Marketing Link. Detta påverkar bara den app som förvärvsservern dirigerar om dig till, efter att du klickat på länken för förvärv, och inte möjligheten att testa länken för förvärv. Frågesträngsparametrar skickas till Google Play-butiken, som skickas till appen vid installationen som en del av en kampanjsändning. Testning av mobilappsförvärv kräver simulering av den här typen av sändning.

Appen måste vara nyligen installerad eller ha data rensade i **[!UICONTROL Settings]** varje gång ett test körs. Detta garanterar att de inledande livscykelvärdena som är kopplade till parametrarna för kampanjfrågesträngen skickas när appen startas första gången.

1. Slutför de nödvändiga uppgifterna när du skaffar [mobilappar](/help/android/acquisition-main/acquisition.md) och se till att du har implementerat sändningsmottagaren korrekt för `INSTALL_REFERRER`.
1. I användargränssnittet för Adobe Mobile Services klickar du på **[!UICONTROL Acquisition]** > **[!UICONTROL Marketing Links Builder]** och skapar en URL för Acquisition Marketing Link som anger Google Play som mål för Android-enheter.

   Mer information finns i [Marketing Links Builder](/help/using/acquisition-main/c-marketing-links-builder/c-marketing-links-builder.md).

   Exempel:

   `https://c00.adobe.com/v3/da120731d6c09658b82d8fac78da1d5fc2d09c48e21b3a55f9e2d7344e08425d/start?a_dl=573e5bb3248a501360c2890b`

1. Öppna den genererade länken på Android-enheten.

   Du bör omdirigeras till en sida med en URL som liknar följande exempel:

   `https://play.google.com/store/apps/details?id=com.adobe.android&referrer=utm_campaign%3Dadb_acq_v3%26utm_source%3Dadb_acq_v3%26utm_content%3D91b52ce097b1464b9b47cb2995c493cc6ab2c3a3`

1. Kopiera det unika ID:t efter `utm_content%3D`.

   I föregående exempel är ID:t `91b52ce097b1464b9b47cb2995c493cc6ab2c3a3`.

   Om du inte kan hämta det unika ID:t på enheten kör du följande `CURL` kommando på skrivbordet för att hämta det unika ID:t från svarssträngen.

   `curl -A "Mozilla/5.0 (Linux; Android 5.0.2; SAMSUNG SM-T815Y Build/LRX22G) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.133 Safari/537.36" <Your Marketing Link>`

   Exempel:

   `curl -A "Mozilla/5.0 (Linux; Android 5.0.2; SAMSUNG SM-T815Y Build/LRX22G) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.133 Safari/537.36" https://c00.adobe.com/v3/da120731d6c09658b82d8fac78da1d5fc2d09c48e21b3a55f9e2d7344e08425d/start?a_dl=573e5bb3248a501360c2890b`

1. Skapa länken för kundvärvningen genom att använda det unika ID:t från steg 3, med följande format:

   `https://c00.adobe.com/v3/<appid>/end?a_ugid=<unique id>`

   Exempel: `https://c00.adobe.com/v3/<appid>/end?a_ugid=91b52ce097b1464b9b47cb2995c493cc6ab2c3a3`

1. Öppna länken i en webbläsare.

   Du bör se `contextData` i JSON-svaret:

   ```
   {"fingerprint":"44b2f88a062df7e727c047f006deb9971304617b","endCallbacks":["***"],"timestamp":1464301282,"appguid":"da120731d6c09658b82d8fac78da1d5fc2d09c48e21b3a55f9e2d7344e08425d","contextData": 
   {"a.launch.campaign.trackingcode":"trymttvm","a.referrer.campaign.name":"Android Demo","a.referrer.campaign.trackingcode":"trymttvm"} 
   ,"adobeData":{"unique_id":"9a2be52764a8db125c29a8c10f3b1b3d5d8ed915","deeplinkid":"57476c26072932ec6d3a470b"}}.
   ```

1. Upprepa steg 3 för att få ett nytt unikt ID.
1. Kontrollera att följande inställningar i konfigurationsfilen är korrekta:

   | Inställning | Värde |
   |--- |--- |
   | förvärv | Servern ska vara `c00.adobe.com`och *`appid`* ska vara lika med `appid` den i din värvningslänk. |
   | analys | För testningsändamål ställer du in att referenspunktens tidsgräns ska tillåta tillräckligt med tid (60 sekunder eller mer) för att skicka sändningen manuellt. Du kan återställa den ursprungliga timeout-inställningen efter testningen. |

1. Anslut enheten till en dator, avinstallera och installera programmet igen.
1. Starta ADB Shell och starta programmet på enheten.

   ```
   adb shell
   ```

1. Skicka en sändning med följande `adb` kommando:

   ```
   am broadcast -a com.android.vending.INSTALL_REFERRER -n com.adobe.android/com.adobe.android.YourBroadcastReceiver --es "referrer" "utm_source=adb_acq_v3&utm_campaign=adb_acq_v3&utm_content=<unique id get on step 5>"
   ```

1. Ersätt `com.adobe.android` med programmets paketnamn, uppdatera mottagarreferensen med referensen till platsen för kampanjspårningsmottagaren i din app och ersätt de värden som är associerade med `utm_content`.

   Om sändningen lyckas bör du förvänta dig ett svar som i följande exempel:

   ```
   Broadcasting: Intent 
   { act=com.android.vending.INSTALL_REFERRER cmp=com.adobe.adms.tests/.ReferralReceiver (has extras) } 
   Broadcast completed: result=0 
   ```

1. (Valfritt) Du kan aktivera felsökningsloggning av SDK för att få ytterligare information.

   Om allt fungerar som det ska bör du se följande loggar:

   ```
   "Analytics - Received referrer information(<referrer content>)" 
   "Analytics - Trying to fetch referrer data from (acquisition end url)"; 
   "Analytics - Received Referrer Data(<A JSON Response>)"
   ```

   Om loggarna inte visas kontrollerar du att du har utfört steg 6 till 10.

   Följande tabell innehåller ytterligare information om möjliga fel:

   | Fel | Beskrivning |
   |--- |--- |
   | Analys - Det gick inte att avkoda svar(`<string>`). | Svaret har fel format. |
   | Analys - Det gick inte att analysera svaret (`a JSON Response`). | JSON-strängen har fel format. |
   | Analys - Det går inte att analysera ett svar från en förvärvstjänst (ingen `contextData` parameter i svaret). | Det finns ingen `contextData` parameter i svaret. |
   | Analys - Referensdata för värvning var inte fullständiga (inga `a.referrer.campaign.name` i kontextdata), ignoreras. | `a.referrer.campaign.name` ingår inte i contextData. |
   | Analys - Anskaffningsreferenten nådde tidsgränsen. | Det gick inte att hämta svaret inom den tid som definierats av `referrerTimeout`. Öka värdet och försök igen.  Du bör även kontrollera att du har öppnat förvärvningslänken innan du installerar appen. |

Kom ihåg följande information:

* Hits som skickas från appen kan övervakas med HTTP-övervakningsverktyg för att verifiera värvningsattribueringen.
* Mer information om hur du sänder `INSTALL_REFERRER`finns i [Testa Google Play Campaign Measurement](https://developers.google.com/analytics/solutions/testing-play-campaigns) i handboken för Google Developers.
* Du kan använda det medföljande `acquisitionTest.jar` Java-verktyget för att få tillgång till det unika ID:t och sändningsreferenten som i sin tur hjälper dig att få fram informationen i steg 3 till 10.

**Installera Java-verktyget**

Så här installerar du Java-verktyget:

1. Ladda ned [`acquistionTester.zip`](../assets/acquisitionTester.zip) filen.
1. Extrahera .jar-filen.

   Du kan köra .jar-filen på kommandoraden.

Exempel:

```
java -jar acquisitionTester.jar -a com.adobe.test -r com.adobe.test.ReferrerReceiver -l "https://c00.adobe.com/v3/appid/start?a_i_id=123456&a_g_id=com.adobe.test&a_dd=i&ctxa.referrer.campaign.name=name&ctxa.referrer.campaign.trackingcode=1234
```

Marknadsföringslänkarna cachas på serversidan med tio minuters förfallotid. När du gör ändringar i länkmarkeringen väntar du i cirka 10 minuter innan ändringarna börjar gälla innan du använder länkarna igen.
