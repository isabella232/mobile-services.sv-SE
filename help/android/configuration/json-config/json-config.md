---
description: Den här informationen hjälper dig att använda ADBMobil.json-konfigurationsfilen.
seo-description: Den här informationen hjälper dig att använda ADBMobil.json-konfigurationsfilen.
seo-title: ADBMomobile JSON-konfiguration
solution: Experience Cloud,Analytics
title: ADBMomobile JSON-konfiguration
topic-fix: Developer and implementation
uuid: 1decf605-7bc3-4e73-ad52-1ecd5821599e
exl-id: 652aeb05-b052-448d-98c8-d513d050a6f5
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 4%

---

# ADBMomobile JSON-konfigurationsfil {#adbmobile-json-config}

Den här informationen hjälper dig att förstå variablerna i ADBMobil.json-konfigurationsfilen.

## `ADBMobileConfig.json` config file reference  {#section_5AD4EDF87E304980B4AC4A5657FDA8B9}

Samma config-fil kan användas för appen på flera plattformar:

>[!TIP]
>
>I **Android** måste filen `ADBMobileConfig.json` placeras i mappen `assets`.

Här är en lista över variablerna i JSON-filen och den SDK-version du behöver för varje variabel:

* **förvärv**
   * Minsta SDK-version: 4.1
   * Möjliggör förvärv av mobilappar.
      * `server`, som är förvärvsservern som kontrolleras vid den första starten för en förvärvshänvisare.
      * `appid`, som är det genererade ID som unikt identifierar den här appen på förvärvsservern.

   Om det här avsnittet saknas aktiverar du förvärvet av mobilappar och hämtar SDK-konfigurationsfilen igen. Mer information finns i *referenceTimeout* i den här variabellistan.

* **analyticsForwardingEnabled**
   * SDK-version är minst 4.8.0.
   * Standardvärdet är `false`.

      Egenskapen i `audienceManager`-objektet. Om Audience Manager är konfigurerat och `analyticsForwardingEnabled` är inställt på `true` vidarebefordras även all Analytics-trafik till Audience Manager.

* **backdateSessionInfo**
   * Minsta SDK-version: 4.6.
   * Aktiverar/inaktiverar möjligheten för Adobe SDK att uppdatera sessionsinfo-träffar.

      Sessionsinformationsträffar består för närvarande av krascher och sessionslängd och kan aktiveras eller inaktiveras.

      **Aktivera eller inaktivera träffar**

      * Om du anger värdet `false` är träffarna **inaktiverade**. SDK:n återgår till det beteende som gällde före 4.1, där sessionsinformationen för föregående session sammanfogades med den första träffen i efterföljande session. Adobe SDK bifogar även sessionsinformationen till den aktuella livscykeln, vilket gör att det inte går att skapa ett uppblåst besök. Eftersom antalet uppblåsta besök inte längre skapas sker en omedelbar minskning av antalet besök.

      * Om du inte anger något värde är standardvärdet `true` och träffarna är **aktiverade**. När träffarna är aktiverade uppdaterar Adobe SDK sessionsinformationen till en sekund efter den sista träffen i föregående session. Detta innebär att krasch- och sessionsdata korrelerar med rätt datum då de inträffade. En bieffekt av detta är att SDK kan skapa ett besök för den efterdaterade träffen. En träff är inaktuell vid varje ny programstart.

         >[!IMPORTANT]
         >
         >Senare information om sessionsträff skickas i ett sessionsinfoserveranrop och ytterligare serveranrop kan gälla.

* **batchLimit**
   * Minsta SDK-version: 4.1
   * Tröskelvärde för hur många träffar som ska skickas i efterföljande anrop.

      Om till exempel `batchLimit` är 10 sparas varje träff före den 10:e träffen i kön. När den 10:e träffen kommer, skickas alla 10 träffar i följd.

      Kom ihåg följande information:

      * Standardvärdet är `0`, vilket betyder att gruppering inte är aktiverat.
      * Kräver `offlineEnabled = true`.

* **charset**
   * Minsta SDK-version: 4.0
   * Definierar den teckenuppsättning som du använder för data som skickas till Analytics.

      Teckenuppsättningen används för att konvertera inkommande data till UTF-8 för lagring och rapportering.

* **clientCode**
   * Minsta SDK-version: 4.0
   * Din tilldelade klientkod.

      >[!IMPORTANT]
      >
      >Den här variabeln krävs av Target.

* **coopUnsafe**
   * Minsta SDK-version: 4.16.1
   * Den booleska egenskapen för `marketingCloud`-objektet som, när det är inställt på `true`, gör att enheten avanmäls från Experience Cloud Device Co-Op.
   * Standardvärdet är `false`.
   * Den här inställningen används **endast** för Device Co-op-etablerade kunder.

   För medlemmar i Device Co-op som kräver det här värdet `true` måste du arbeta med Co-op-teamet för att begära en blockeringslista-flagga på ditt Device Co-op-konto. Det finns ingen självbetjäningsväg för att aktivera dessa flaggor.

   Kom ihåg följande information:

   * När `coopUnsafe` är inställt på `true` läggs `coop_unsafe=1` alltid till i Audience Manager och besökar-ID-träffar.
   * Om du aktiverar vidarebefordran på serversidan för Analytics till Audience Manager visas även `coop_unsafe=1` Analytics-träffar.


* **environmentId**
   * Minsta SDK-version: 4.14
   * ID:t för miljön som du vill använda.

      Du kan ange ett giltigt ID (`environmentId=8`), och om `environmentId` inte inkluderas används standardproduktionsmiljön.

* **lifecycleTimeout**
   * Minsta SDK-version: 4.0
   * Standardvärdet är 300 sekunder.

      Anger hur lång tid (i sekunder) som måste gå mellan den tidpunkt då programmet startas men innan det betraktas som en ny session. Den här tidsgränsen gäller även när programmet skickas till bakgrunden och återaktiveras.

      Den tid som programmet lägger i bakgrunden inkluderas inte i sessionslängden.

* **meddelanden**

   * Minsta SDK-version: 4.2
   * Inställningarna för meddelanden i appen definieras automatiskt av Adobe Mobile-tjänster. Mer information finns i avsnittet *Meddelandebeskrivning* nedan.

* **offlineEnabled**

   * Minsta SDK-version: 4.0
   * När det här alternativet är aktiverat köas träffar när enheten är offline och skickas senare när enheten är online.

      Din rapportsvit måste vara tidsstämpelaktiverad för att du ska kunna använda offline-spårning.

      Standardvärdet är `false`.

      >[!IMPORTANT]
      >
      >Om tidsstämplar är aktiverade i rapportsviten måste `offlineEnabled` konfigurationsegenskapen **vara** vara true. Om rapportsviten inte är tidsstämpelaktiverad måste `offlineEnabled`-konfigurationsegenskapen **vara** vara false.
      >
      >Om detta inte är korrekt konfigurerat går data förlorade. Om du är osäker på om en rapportsserie är tidsstämplad eller inte kan du kontakta kundtjänst eller hämta konfigurationsfilen från Adobe Mobile-tjänster.

      Om du för närvarande rapporterar AppMeasurement-data till en rapportserie som även samlar in data från JavaScript, kan du behöva skapa en separat rapportserie för mobildata eller inkludera en anpassad tidsstämpel för alla JavaScript-träffar som använder variabeln `s.timestamp`.

* **org**

   * Minsta SDK-version: 4.3
   * Anger ID-tjänstens Experience Cloud-organisations-ID.

* **poi**
   * Minsta SDK-version: 4.0
   * Varje POI-array (point of interest) innehåller POI-namnet, latituden, longituden och radien i meter för punktens område.

      POI-namnet kan vara vilken sträng som helst. När ett `trackLocation`-anrop skickas och de aktuella koordinaterna finns inom en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation`-anropet.

      ```javascript
      "poi": [
                 ["san francisco",37.757144,-122.44812,7000]
                 ["santa cruz",36.972935,-122.01725,600]
             ]
      ```

      Från och med version 4.2 definieras POI i gränssnittet för Adobe Mobile och synkroniseras dynamiskt till programkonfigurationsfilen. Synkroniseringen kräver inställningen `analytics.poi`:

      ```javascript
        “analytics.poi“: `https://assets.adobedtm.com/`
      …/yourfile.json”`,
      ```

      Om den här inställningen inte är konfigurerad måste `ADBMobile.json`-filen uppdateras för att inkludera den här raden. Information om hur du hämtar en uppdaterad konfigurationsfil finns i [Innan du startar](/help/android/getting-started/requirements.md).

* **återanslående**
   * Minsta SDK-version: 4.6
   * Här är definitionen för meddelandemallen &quot;callback&quot;:

      ```javascript
      "payload":{
        "templateurl":"", //required will be token-expanded prior to being sent
        "templatebody":"", //optional - if this length > 0 POST will be used as transport method. This is a base64 encoded blob, which will be decoded and token-expanded prior to being sent.
        "contenttype": "", // optional - if this is length > 0 and POST type is selected this will be set as the Content-Type header.  if this is not supplied for a POST request, the default will be "application/x-www-form-urlencoded"
        "timeout": 0 // optional - number of seconds to wait before timing out.  Default is 2.}
      ```

      Objektet `payload` i koden är en provnyttolast för en meddelandedefinition som finns i filen `ADBMobileConfig.json`. Mer information finns i [Eftersläpningar](/help/android/analytics-main/postbacks/postbacks.md).

* **privacyDefault**
   * Minsta SDK-version: 4.0
   * Standardvärdet är `optedin`.
      * För `optedin` skickas träffarna omedelbart.
      * För `optedout` ignoreras träffarna.
      * För `optunknown`, om rapportsviten är tidsstämpelaktiverad, sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras).

      Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till `optedin`.  Detta anger bara det inledande värdet. Om det här värdet anges eller ändras i koden används det nya värdet tills det ändras igen eller när programmet avinstalleras och installeras om.


* **referrerTimeout**
   * Minsta SDK-version: 4.1
   * Antal sekunder som SDK väntar på att hämta referensdata för hämtning vid den första starten innan timeout inträffar. Om du använder förvärv rekommenderar vi en 5-sekunderstimeout.

      >[!IMPORTANT]
      >
      >Den här variabeln krävs av förvärvet. Om variabeln är inställd på `0` eller inte inkluderas väntar SDK inte på förvärvsdata och förvärvsstatistik spåras inte.

* **fjärrplatser**
   * Minsta SDK-version: 4.2
   * Konfigureras automatiskt och definierar slutpunkter på Adobe för dynamiska konfigurationsfiler.

      Den senaste uppdateringstiden för varje konfigurationsfil kontrolleras mot den aktuella versionen vid varje start och uppdateringarna hämtas och sparas.
      * `analytics.poi` är slutpunkten för POI-konfigurationen som lagras.
      * `messages` är slutpunkten för konfigurationen av värdbaserade meddelanden i programmet.

* **rsids**
   * Minsta SDK-version: 4.0
   * En eller flera rapportsviter för att ta emot analysdata. Flera rapportpaket-ID:n ska vara kommaavgränsade utan mellanrum.

      ```javascript
        "rsids" "rsid"
      ```

      ```javascript
        "rsids" "rsid1,rsid2"
      ```

      >[!IMPORTANT]
      >
      >Den här variabeln krävs av Analytics.

* **server**
   * Minsta SDK-version: 4.0
   * Analytics- eller Audience Management-servern, baserad på den överordnade noden. Den här variabeln ska fyllas i med serverdomänen, utan ett `https://`- eller `https://`-protokollprefix. Det här prefixet hanteras automatiskt av biblioteket och baseras på variabeln `ssl`. Om `ssl` är `true` skapas en säker anslutning till den här servern. Om `ssl` är `false` skapas en osäker anslutning till den här servern.

* **ssl**
   * Minsta SDK-version: 4.0
   * Standardvärdet är `false`.

      Aktiverar (`true`) eller inaktiverar (`false`) möjligheten att skicka mätdata med SSL (HTTPS).

      Definitionen för&quot;callback&quot;-meddelandemallen visas nedan:

      ```javascript
      "payload": {
          "templateurl":"",//required-will be token-expanded prior to being sent 
          "templatebody": "", //optional - if this length >  0 POST will be used& as transport method. This is a base64 encoded blob, which will be  decoded and token-expanded prior to being sent.
          "contenttype": "" // optional - if this is length > 0 POST type is selected this will be set as the Content-Type header. if this is not supplied for a POST request, the default will be "application/x-www-form-urlencoded"
          "timeout": 0 // optional - number of seconds to wait before timing& out. Default is 2.}
      ```

* **timeout**
   * Minsta SDK-version: 4.0
   * Anger hur länge Target väntar på ett svar.


## Exempel på `ADBMobileConfig.json` fil {#section_4655EF79744649E5A5AE19E3224C472C}

Här följer ett exempel på en `ADBMobileConfig.json`-fil:

```js
 { 
    "version": "2014-08-05T19:18:28.169Z", 
    "marketingCloud" : { 
        "org": "016D5C175213CCA80A490D05@AdobeOrg", 
        "coopUnsafe": false 
    }, 
    "target": { 
        "clientCode": "", 
        "timeout": 5, 
        "environmentId": 8 
    }, 
    "audienceManager": { 
        "server": "", 
        "analyticsForwardingEnabled": false 
    }, 
    "acquisition": { 
        "server": "c00.adobe.com", 
        "appid": "10a77a60192fbb628376e1b1daeeb65debf934e2c807e067ceb2963a41b165ee" 
    }, 
    "analytics": { 
        "rsids": "coolApp", 
        "server": "my.CoolApp.com", 
        "ssl": true, 
        "offlineEnabled": true, 
        "charset": "UTF-8", 
        "lifecycleTimeout": 300, 
        "privacyDefault": "optedin", 
        "batchLimit": 0, 
        "referrerTimeout": 5, 
        "poi": [ 
            ["san francisco",37.757144,-122.44812,7000],  
            ["santa cruz",36.972935,-122.01725,600] 
        ] 
    }, 
    "messages": [ 
        { 
            "messageId": "cb426565-a563-497a-a889-9dbeb451f8ae", 
            "template": "fullscreen", 
            "payload": { 
                 "html": "<!DOCTYPE html><html><head><meta charset=\"utf-8\" /><title></title><style></style></head><body><iframe src=\"https://www.adobe.com/\" frameborder=\"0\"></iframe></body></html>" 
            }, 
            "showOffline": false, 
            "showRule": "always", 
            "endDate": 2524730400, 
            "startDate": 0, 
            "audiences": [], 
            "triggers": [ 
                { 
                    "key": "pev2", 
                    "matches": "eq", 
                    "values": [ 
                        "AMACTION:custom" 
                    ] 
                } 
            ] 
        } 
    ], 
    "remotes": { 
        "analytics.poi": "https://assets.adobedtm.com/staging/42a6fc9b77cd9f29082cf19b787bae75b7d1f9ca/scripts/satellite-53e0faadc2f9ed92bc00003b.json", 
        "messages": "https://assets.adobedtm.com/staging/42a6fc9b77cd9f29082cf19b787bae75b7d1f9ca/scripts/satellite-53e0f9e2c2f9ed92bc000032.json" 
    } 
}
```

## Meddelandebeskrivning {#section_B97D654BA92149CE91F525268D7AD71F}

Meddelandenoden genereras automatiskt av Adobe Mobile-tjänster och behöver vanligtvis inte ändras manuellt. Följande beskrivning tillhandahålls i felsökningssyfte:

* &quot;messageId&quot;
* Genererat ID, obligatoriskt
* &quot;template&quot;
   * &quot;alert&quot;, &quot;fullscreen&quot; eller &quot;local&quot;
   * obligatoriskt

* &quot;showOffline&quot;
   * true eller false
   * default is false

* &quot;showRule&quot;
   * &quot;always&quot;, &quot;once&quot; eller &quot;untilClick&quot;
   * obligatoriskt

* &quot;endDate&quot;
   * antal sekunder sedan 1 januari 1970
   * standard är 2524730400

* &quot;startDate&quot;
   * antal sekunder sedan 1 januari 1970
   * standardvärdet är 0

* &quot;nyttolast&quot;
   * &quot;html&quot;
      * endast helskärmsmall, obligatoriskt
      * html som definierar meddelandet
   * &quot;bild&quot;
      * endast helskärm, valfritt
      * URL till bilden som ska användas för helskärmsbilden
   * &quot;altImage&quot;
      * endast helskärm, valfritt
      * namnet på den paketerade bilden som ska användas om den URL som anges i
         * bild
         * går inte att nå
   * &quot;title&quot;
      * helskärm och varning, krävs
      * titeltext för helskärm eller varningsmeddelande
   * &quot;content&quot;
      * avisering och lokal avisering, krävs
      * undertext för ett varningsmeddelande eller meddelandetext för ett lokalt meddelandemeddelande
   * &quot;bekräfta&quot;
      * varning, valfri
      * text som används i bekräftelseknappen
   * &quot;cancel&quot;
      * varning, krävs
      * text som används i knappen Avbryt
   * &quot;url&quot;
      * varning, valfri
      * URL-åtgärd som ska läsas in om användaren klickar på bekräftelseknappen
   * &quot;wait&quot;
      * lokal avisering, krävs
      * hur lång tid det tar att vänta (i sekunder) på att skicka det lokala meddelandet efter att villkoret har matchats



* ”audiences”
   * en array med objekt som definierar hur meddelandet ska visas
   * ”key”
      * variabelnamn att söka efter i träffen, krävs
* ”matches”
   * typ av matchare som används vid jämförelsen
   * eq = lika med
   * ne = är inte lika med
   * co = contains
   * nc = innehåller inte
   * sw = börjar med
   * ew = slutar med
   * ex = finns
   * nx = finns inte
   * lt = mindre än
   * le = mindre än eller lika med
   * gt = större än
   * ge = större än eller lika med
* ”values”
   * en array med värden som används för att matcha mot värdet för variabeln som namnges i
      * key
      * med matchningstypen i
      * matchar
* ”triggers”
   * samma som målgrupper, men detta är åtgärden istället för målgruppen
   * ”key”
   * ”matches”
   * ”values”
