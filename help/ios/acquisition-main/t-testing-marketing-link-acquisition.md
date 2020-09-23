---
description: Följande instruktioner hjälper er att skicka en kundvärvningskampanj via en Marketing Link som baseras på ett enhets fingeravtryck.
keywords: android;library;mobile;sdk
seo-description: Följande instruktioner hjälper er att skicka en kundvärvningskampanj via en Marketing Link som baseras på ett enhets fingeravtryck.
seo-title: Testa Marketing Link-förvärv
solution: Experience Cloud,Analytics
title: Testa Marketing Link-förvärv
topic: Developer and implementation
uuid: 69503e01-182d-44c6-b0fb-e1c012ffa3bd
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# Testa Marketing Link-förvärv {#testing-marketing-link-acquisition}

Följande instruktioner hjälper er att skicka en kundvärvningskampanj via en Marketing Link som baseras på ett enhets fingeravtryck.

1. Slutför de nödvändiga uppgifterna i [anskaffning](/help/ios/acquisition-main/acquisition.md)av mobilappar.
1. I användargränssnittet för Adobe Mobile Services klickar du på **[!UICONTROL Marketing Links Builder]** och genererar en länk för kundvärvning som anger App Store som mål för iOS-enheter.

   Exempel:

   ```
   https://c00.adobe.com/v3/da120731d6c09658b82d8fac78da1d5fc2d09c48e21b3a55f9e2d7344e08425d/start?a_dl=57477650072932ec6d3a470f
   ```

   Mer information finns i [Marketing Links Builder](/help/using/acquisition-main/c-marketing-links-builder/c-marketing-links-builder.md).


1. Öppna den genererade länken på iOS-enheten och öppna `https://c00.adobe.com/v3/<appid>/end`.

   Du bör se contextData i JSON-svaret:

   ```js
   {"fingerprint":"bae91bb778f0ad52e37f0892961d06ac6a5c935b","endCallbacks":["***"],"timestamp":1464301217,"appguid":"da120731d6c09658b82d8fac78da1d5fc2d09c48e21b3a55f9e2d7344e08425d","contextData":
   {"a.launch.campaign.trackingcode":"twdf4546","a.referrer.campaign.name":"iOS Demo","a.referrer.campaign.trackingcode":"twdf4546"}
   ,"adobeData":{"unique_id":"8c14098d7c79e8a180c15e4b2403549d3cc21ea8","deeplinkid":"57477650072932ec6d3a470f"}}
   ```

1. Kontrollera att följande inställningar i konfigurationsfilen är korrekta:

   | Inställning | Värde |
   |--- |--- |
   | förvärv | Servern bör vara `c00.adobe.com`. `appid` ska vara lika med *`appid`* er förvärvslänk. |
   | analys | `referrerTimeout` ska ha ett värde som är större än 0. |

1. (Villkorligt) Om SSL-inställningen i appens konfigurationsfil är `false`ska du uppdatera din hämtningslänk så att HTTP-protokollet används i stället för HTTPS.
1. Klicka på den genererade länken från den mobila enhet som du vill installera appen på.

   Adobe-servrar (`c00.adobe.com`) lagrar fingeravtrycket och omdirigerar till App Store. Appen behöver inte laddas ned för testning.
1. Starta programmet första gången från samma mobila enhet som du använde i steg 6.

   Du kan ta bort och installera programmet igen om det behövs.
1. (Valfritt) Aktivera felsökningsloggning av SDK för att få ytterligare information.

   Om allt fungerar som det ska bör du se följande loggar:

   `"Analytics - Trying to fetch referrer data from <acquisition end url>"`
   `"Analytics - Received Referrer Data(<Json Object>)"`

   Om loggarna inte visas kontrollerar du att du har utfört steg 4 och 5.

   Här följer information om möjliga fel:

   * `Analytics - Unable to retrieve acquisition service response (<error message>)`:

      Ett nätverksfel uppstod.

   * `Analytics - Unable to parse acquisition service response (<error message>)`

      Svaret har inte rätt format.

   * `Analytics - Unable to parse acquisition service response (no contextData parameter in response)`

      Det finns ingen `contextData` parameter i svaret.

   * `Analytics - Acquisition referrer data was not complete, ignoring`

      `a.referrer.campaign.name` ingår inte i `contextData`.

   * `Analytics - Acquisition referrer timed out`

      Det gick inte att hämta svaret inom den tid som definieras av `referrerTimeout`. Öka värdet och försök igen. Du bör också kontrollera att du har öppnat förvärvningslänken innan du installerar appen och att du använder samma nätverk när du klickar på URL:en och öppnar appen.

Kom ihåg följande information:

* Hämtningsservern ger en attribueringsmatchning som baseras på IP-adressen och användaragentinformationen som spelades in i länkklicket (steg 6) och när appen startas (steg 7).

   Du bör vara i samma nätverk när du klickar på URL:en och när du öppnar appen.

* Med HTTP-övervakningsverktyg kan träffar som skickas från appen övervakas för att bekräfta förvärvsattribueringen.

   Du bör se en `/v3/<appid>/start` begäran och en `/v3/<appid>/end` begäran som skickas till förvärvsservern.

* Variationer i användaragenten som skickas kan göra att attribueringen misslyckas.

   Se till att `https://c00.adobe.com/v3/<appid>/start` och `https://c00.adobe.com/v3/<appid>/end` ha samma användaragentvärden.

* Förvärvningslänken och träffen från SDK bör använda samma HTTP/HTTPS-protokoll.

   Om länken och träffen använder olika protokoll, där till exempel HTTP och SDK använder HTTPS, kan IP-adressen skilja sig åt för vissa operatörer för varje begäran. Detta kan få attribueringen att misslyckas.

* Marknadsföringslänkarna cachas på serversidan med tio minuters förfallotid.

   När du gör ändringar i marknadsföringslänkar bör du vänta i ungefär 10 minuter innan du använder länkarna.