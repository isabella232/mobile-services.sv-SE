---
description: Den här informationen hjälper er att skicka en länk till en kampanj för V3-förvärv baserat på ett enhets fingeravtryck.
seo-description: Den här informationen hjälper er att skicka en länk till en kampanj för V3-förvärv baserat på ett enhets fingeravtryck.
seo-title: Testar V3-förvärv
solution: Experience Cloud,Analytics
title: Testar V3-förvärv
uuid: 89137ccf-4839-4b37-926e-303cf8e511a5
exl-id: 3cf66802-1f2c-428f-86ef-a9afc57e3470
source-git-commit: 8db8f51a42acbbc0bbc4545b7d97cb214b490ab3
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Testar V3-förvärv{#testing-v-acquisition}

Den här informationen hjälper er att skicka en länk till en kampanj för V3-förvärv baserat på ett enhets fingeravtryck.

>[!IMPORTANT]
>
>V3 Acquisition avser de förvärvslänkar du skapar med Acquisition Builder i användargränssnittet för Adobe Mobile Services. Om du vill använda den här funktionen måste du uppgradera till iOS SDK version 4.6.0 eller senare.

Om mobilappen ännu inte finns i App Store väljer du en mobilapp som mål när du skapar kampanjlänken. Detta påverkar bara den app som förvärvsservern dirigerar om dig till efter att du klickat på länken, men det påverkar inte möjligheten att testa länken.

1. Slutför de nödvändiga uppgifterna i [Anskaffning av mobilapp](/help/ios/acquisition-main/acquisition.md).
1. Navigera till **[!UICONTROL Acquisition Builder]** i användargränssnittet för mobiltjänster i Adobe och generera en URL för anskaffningskampanj.

   Exempel:

   ```
   https://c00.adobe.com/v3/<appid>/start?a_i_id=iostestapp&a_g_id=com.adobe.android&a_dd=i&ctxa.referrer.campaign.name=name&ctxa.referrer.campaign.trackingcode=trackingcode
   ```


   Om du refererar till både iOS- och Android-appar i förvärvslänken använder du Apple Store som standardbutik.
1. Öppna den genererade länken i en webbläsare och gå till `https://c00.adobe.com/v3/<appid>/end`.

   Du bör se `contextData` i JSON-svaret:

   ```js
   {"fingerprint":"228d7e6058b1d731dc7a8b8bd0c15e1d78242f31","timestamp":1457989293,"appguid":"","contextData":{"a.referrer.campaign.name":"name","a.referrer.campaign.trackingcode":"trackingcode"}}.
   ```

   Om du inte ser `contextData`, eller om en del av den saknas, kontrollerar du att förvärvs-URL:en följer det format som anges i [Skapa förvärvningslänk manuellt](/help/using/acquisition-main/c-marketing-links-builder/acquisition-link-manual.md).
1. Kontrollera att följande inställningar i konfigurationsfilen är korrekta:

   | Inställning | Värde |
   |--- |--- |
   | förvärv | Servern ska vara `c00.adobe.com`. *`appid`* ska vara lika med  *`appid`* er förvärvslänk. |
   | analys | `referrerTimeout` ska ha ett värde som är större än 0. |


1. (Villkorligt) Om `ssl`-inställningen i appens konfigurationsfil är true uppdaterar du din hämtningslänk så att HTTPS-protokollet används.
1. Klicka på den genererade länken från den mobila enhet som du tänker installera appen på.

   Adobe-servrar ( `c00.adobe.com`) lagrar fingeravtrycket och omdirigerar till App Store. Appen behöver inte laddas ned för testning.
1. Starta programmet första gången från samma mobila enhet som du använde i steg 6.

   Du kan ta bort och installera programmet igen om det behövs.
1. (Valfritt) Du kan aktivera felsökningsloggning av SDK för att få ytterligare information.

   Om allt fungerar som det ska bör du se följande loggar:

   `"Analytics - Trying to fetch referrer data from <acquisition end url>"`
   `"Analytics - Received Referrer Data(<Json Object>)"`

   Om du inte ser loggarna ovan kontrollerar du att du har slutfört steg 4 och 5.

   Här följer information om möjliga fel:

   * `Analytics - Unable to retrieve acquisition service response (<error message>)`
Ett nätverksfel uppstod.

   * `Analytics - Unable to parse acquisition service response (<error message>)`

      Svaret har inte rätt format.

   * `Analytics - Unable to parse acquisition service response (no contextData parameter in response)`

      Det finns ingen `contextData`-parameter i svaret.

   * `Analytics - Acquisition referrer data was not complete, ignoring`

      `a.referrer.campaign.name` ingår inte i  `contextData`.

   * `Analytics - Acquisition referrer timed out`

      Det gick inte att hämta svaret i den tid som är definierad av `referrerTimeout`. Öka värdet och försök igen. Du bör också kontrollera att du har öppnat förvärvningslänken innan du installerar appen och att du använder samma nätverk när du klickar på URL:en och öppnar appen.

      Kom ihåg följande information:

      * Hämtningsservern tillhandahåller en attribueringsmatchning som baseras på IP-adressen och användaragentinformationen som registreras i länkklicket (steg 6) och när appen startas (steg 7).

         Du bör vara i samma nätverk när du klickar på URL:en och när du öppnar appen.

      * Med HTTP-övervakningsverktyg kan träffar som skickas från appen övervakas för att bekräfta förvärvsattribueringen.

         Du bör se en `/v3/<appid>/start`-begäran och en `/v3/<appid>/end`-begäran som skickas till förvärvsservern. Variationer i användaragenten som skickas kan göra att attribueringen misslyckas.

         >[!TIP]
         >
         >Se till att `https://c00.adobe.com/v3/<appid>/start` och `https://c00.adobe.com/v3/<appid>/end` har samma användaragentvärden.

      * Förvärvningslänken och träffen från SDK bör använda samma HTTP/HTTPS-protokoll.

         Om de använder olika protokoll (till exempel HTTP och HTTPS används i SDK), kan IP-adressen skilja sig åt för varje begäran (för vissa bärare) och attribueringen kan misslyckas.
