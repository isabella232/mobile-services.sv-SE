---
description: Den här informationen hjälper dig att använda ADBMobil.json-konfigurationsfilen.
solution: Experience Cloud Services,Analytics
title: ADBMomobile JSON-konfiguration
topic-fix: Developer and implementation
uuid: d9708d59-e30a-4f6c-ab1b-d9499855d0c2
exl-id: e3515de3-3aec-4dd0-996d-9c561ad1b1de
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 8%

---

# ADBMomobile JSON-konfiguration {#adbmobile-json-config}

Den här informationen hjälper dig att använda `ADBMobile.json` config-fil.

## ADBMobileConfig.json, referens till konfigurationsfil {#section_5AD4EDF87E304980B4AC4A5657FDA8B9}

Samma config-fil kan användas för appen på flera plattformar:

>[!TIP]
>
>På **iOS**, `ADBMobileConfig.json` filen kan placeras var som helst där den är tillgänglig i ditt paket.

* **förvärv**

   Möjliggör förvärv av mobilappar.

   Om det här avsnittet saknas aktiverar du förvärvet av Mobile App och hämtar SDK-konfigurationsfilen igen. Mer information finns i *referrerTimeout* nedan.

   * `server` - Förvärvsserver som kontrolleras vid den första starten för en förvärvshänvisningsprogram.
   * `appid` - Genererat ID som unikt identifierar den här appen på förvärvsservern.
   * Minsta SDK-version: 4.1

* **analyticsForwardingEnabled**

   Egenskapen i `audienceManager` -objekt. If `Audience Manager` är konfigurerad och `analyticsForwardingEnabled` är inställd på `true`, vidarebefordras all Analytics-trafik till Audience Manager. Standardvärdet är `false`.

   * Minsta SDK-version: 4.8.0

* **backdateSessionInfo**

   Aktiverar/inaktiverar möjligheten för Adobe SDK att uppdatera sessionsinfo-träffar.

   Sessionsinformationsträffar består för närvarande av krascher och sessionslängd och kan aktiveras eller inaktiveras.

   * Om du anger värdet till `false`, träffar är **inaktiverad**.

      SDK:n återgår till det beteende som gällde före 4.1, där sessionsinformationen för föregående session sammanfogades med den första träffen i efterföljande session. Adobe SDK bifogar även sessionsinformationen till den aktuella livscykeln, vilket gör att det inte går att skapa ett uppblåst besök. Eftersom antalet uppblåsta besök inte längre skapas sker en omedelbar minskning av antalet besök.

   * Om du inte anger något värde används standardvärdet `true`och träffar är **aktiverad**.

      När träffarna är aktiverade uppdaterar Adobe SDK sessionsinformationen till en sekund efter den sista träffen i föregående session. Detta innebär att krasch- och sessionsdata korrelerar med rätt datum då de inträffade. En bieffekt av detta är att SDK kan skapa ett besök för den efterdaterade träffen. En träff är inaktuell vid varje ny programstart.

   * Minsta SDK-version: 4.6
   >[!IMPORTANT]
   >
   >Senare information om sessionsträffen skickas i ett sessionsinfoserveranrop, och ytterligare serveranrop kan gälla.


* **batchLimit**

   Tröskelvärde för hur många träffar som ska skickas i efterföljande anrop. Om `batchLimit` är inställd på 10, så att varje träff före den 10:e träffen lagras i kön. När den 10:e träffen kommer skickas alla 10 träffar i följd.

   * Standardvärdet är `0`, vilket betyder att gruppering inte är aktiverat.
   * Kräver `offlineEnabled = true`.
   * Minsta SDK-version: 4.1

* **charset**

   Definierar den teckenuppsättning som du använder för data som skickas till Analytics. Teckenuppsättningen används för att konvertera inkommande data till UTF-8 för lagring och rapportering. Mer information finns i [charSet](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/charset.html) i Adobe Analytics-dokumentationen.

   * Minsta SDK-version: 4.0

* **clientCode**

   Din tilldelade klientkod.

   >[!IMPORTANT]
   >
   >Den här variabeln krävs av Target.

   * Minsta SDK-version: 4.0

* **coopUnsafe**

   För Device Co-op-medlemmar som kräver det här värdet anges till `true`måste du arbeta med Co-op-teamet för att begära en blockeringslista-flagga på ditt Device Co-op-konto. Det finns ingen självbetjäningsväg för att aktivera dessa flaggor.

   Kom ihåg följande information:

   * När `coopUnsafe` är inställd på `true`, `coop_unsafe=1` läggs alltid till i Audience Manager och besökar-ID:n.
   * Om du aktiverar vidarebefordran på serversidan för Analytics till Audience Manager visas även `coop_unsafe=1` i Analytics-träffar.

   Här är ytterligare information:

   * Minsta SDK-version: 4.16.1
   * Den booleska egenskapen i `marketingCloud` objekt som, när de anges till `true`, gör att enheten väljs ut från Experience Cloud Device Co-Op.
   * Standardvärdet är `false`.
   * Den här inställningen används **endast** för Device Co-op-etablerade kunder.



* **environmentId**

   ID:t för miljön som du vill använda. Du kan ange ett giltigt ID (`environmentId=8`), och om `environmentId` ingår inte, standardproduktionsmiljön används.

   * Minsta SDK-version: 4.14

* **lifecycleTimeout**

   Standardvärdet är 300 sekunder.

   Anger hur lång tid (i sekunder) som måste gå mellan den tidpunkt då programmet startas men innan det betraktas som en ny session. Den här tidsgränsen gäller även när programmet skickas till bakgrunden och återaktiveras. Den tid som programmet lägger i bakgrunden inkluderas inte i sessionslängden.

   * Minsta SDK-version: 4.0

* **meddelanden**

   Inställningarna för meddelanden i appen definieras automatiskt av Adobe Mobile-tjänster. Mer information finns i *Meddelandebeskrivning* nedan.

   * Minsta SDK-version: 4.2

* **offlineEnabled**

   När det här alternativet är aktiverat köas träffar när enheten är offline och skickas senare när enheten är online. Din rapportsvit måste vara tidsstämpelaktiverad för att du ska kunna använda offline-spårning. Standardvärdet är `false`.

   Här är viktig information:

   * Om tidsstämplar är aktiverade i rapportsviten kan du `offlineEnabled` konfigurationsegenskap *måste* vara sant.
   * Om rapportsviten inte är tidsstämpel aktiverad kan du `offlineEnabled` konfigurationsegenskap *måste* vara falskt.

      Om detta inte är korrekt konfigurerat går data förlorade. Om du är osäker på om en rapportsserie är tidsstämplad eller aktiverad kan du kontakta kundtjänst eller hämta konfigurationsfilen från Adobe Mobile-tjänster. Om du för närvarande rapporterar AppMeasurement-data till en rapportserie som även samlar in data från JavaScript, kan du behöva skapa en separat rapportserie för mobildata eller inkludera en anpassad tidsstämpel för alla JavaScript-träffar som använder `s.timestamp` variabel.

   * Minsta SDK-version: 4.0

* **org**

   Anger Experience Cloud organisation-ID för Adobe Experience Platform identitetstjänst.

   * Minsta SDK-version: 4.3

* **poi**

   Varje POI-array innehåller POI-namnet, latituden, longituden och radien (i meter) för punktens område. POI-namnet kan vara vilken sträng som helst. När en `trackLocation` anropet skickas, om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation` ring.

   * Minsta SDK-version: 4.0

   ```js
   "poi" [ 
           ["sanfrancisco",37.757144,-122.44812,7000]
           ["santacruz",36.972935,-122.01725,600]
         ] 
   ```

   >[!TIP]
   >
   >Från och med version 4.2 definieras POI i Adobe Mobile-gränssnittet och synkroniseras dynamiskt till programkonfigurationsfilen. Synkroniseringen kräver `analytics.poi` inställning:

   ```js
   "analytics.poi": "`https://assets.adobedtm.com/…/yourfile.json`",
   ```

   Om den här inställningen inte är konfigurerad `ADBMobile.json` filen måste uppdateras för att den här raden ska ingå. Information om hur du hämtar en uppdaterad konfigurationsfil finns i [Innan du börjar](/help/ios/getting-started/requirements.md).

* **återanslående**

   Definitionen för&quot;callback&quot;-meddelandemallen visas nedan:

   ```js
   "payload":{
       "templateurl":"",//required- will be token-expanded prior to being sent
       "templatebody":"", //optional-if this length > 0 POST will be used as transport method. This is a base-64 encoded blob,which will be decoded and token-expanded prior to being sent.
       "contenttype":"", //optional-if this is length > 0 and POST type is selected, this will be set as the Content-Typeheader. if this is not supplied for a POST request,the default will be "application/x-www-form-urlencoded"
       "timeout": 0 //optional-number of seconds to wait before timingout.Defaultis2.}
   ```

   The `payload` -objektet i koden är en exempelnyttolast för en meddelandedefinition som skulle finnas i `ADBMobileConfig.json` -fil. Mer information finns i [Eftersläpning](/help/ios/analytics-main/postback/postback.md).

   * Minsta SDK-version: 4.6

* **privacyDefault**

   * För `optedin`, skickas träffar omedelbart.
   * För `optedout`, kommer träffar att försvinna.
   * För `optunknown`, om rapportsviten är tidsstämpelaktiverad, sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras).

      Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

      Detta anger bara det inledande värdet. Om det här värdet anges eller ändras i koden används det nya värdet tills det ändras igen eller när programmet avinstalleras och installeras om. Standardvärdet är `optedin`.

   * Minsta SDK-version: 4.0

* **referrerTimeout**

   Antal sekunder som SDK väntar på att hämta referensdata för hämtning vid den första starten innan timeout inträffar. Om du använder förvärv rekommenderar vi en 5-sekunderstimeout.

   >[!IMPORTANT]
   >
   >Den här variabeln krävs av förvärvet. Om variabeln är inställd på `0`, eller inte ingår, väntar SDK inte på förvärvsdata och förvärvsstatistik spåras inte.

   * Minsta SDK-version: 4.1

* **fjärrplatser**

   Konfigureras automatiskt och definierar slutpunkter på Adobe för dynamiska konfigurationsfiler. Den senaste uppdateringstiden för varje konfigurationsfil kontrolleras mot den aktuella versionen vid varje start och uppdateringarna hämtas och sparas.

   * `analytics.poi` är slutpunkten för POI-konfigurationen som lagras.

   * `messages` är slutpunkten för konfigurationen av värdbaserade meddelanden i programmet.

   * Minsta SDK-version: 4.2

* **rsids**

   En eller flera rapportsviter för att ta emot analysdata. Flera rapportpaket-ID:n ska vara kommaavgränsade utan mellanrum.

   ```js
   "rsids": "rsid"
   ```

   ```js
   "rsids" : "rsid1,rsid2" 
   ```

   >[!IMPORTANT]
   >
   >Den här variabeln krävs av Analytics.

   * Minsta SDK-version: 4.0

* **server**

   Analytics- eller Audience Management-servern, baserad på den överordnade noden.

   Den här variabeln ska fyllas i med serverdomänen, utan en `https://` eller `https://` protokollprefix. Prefixet hanteras automatiskt av biblioteket och baseras på `ssl` variabel.

   If `ssl` är `true`skapas en säker anslutning till den här servern. If `ssl` är `false`, en osäker anslutning görs till den här servern.

   >[!IMPORTANT]
   >
   >Den här variabeln krävs av Analytics och/eller Audience Management.

   * Minsta SDK-version: 4.0

* **ssl**

   >[!IMPORTANT]
   >
   > Från och med version 4.10.0 är SSL som standard true om flaggan inte är inställd.

   Aktiverar (`true`) eller inaktiverar (`false`) möjligheten att skicka mätdata med SSL (HTTPS).

   Definitionen för&quot;callback&quot;-meddelandemallen visas nedan:

   ```js
   "payload":{
       "templateurl":"",//required-will be token-expanded prior to being sent
       "templatebody":"",//optional-if this length > 0, POST will be used as transport method. This is a base64 encoded blob,which will be decoded and token-expanded prior to being sent.
       "contenttype":"",//optional-if this is length > 0 and POST type is selected this will be set as the Content-Typeheader. if this is not supplied for a POST request,the default will be "application/x-www-form-urlencoded"
       "timeout":0//optional-numberofsecondstowaitbeforetimingout.Defaultis2.} 
   ```

   The `payload` -objektet i koden är en exempelnyttolast för en meddelandedefinition som finns i `ADBMobileConfig.json` -fil. Mer information finns i [Eftersläpning](/help/ios/analytics-main/postback/postback.md).

   * Minsta SDK-version: 4.0

* **timeout**

   Anger hur länge Target väntar på ett svar.

   * Minsta SDK-version: 4.0

## Exempel `ADBMobileConfig.json` fil {#section_52FA7C71A99147AFA9BE08D2177D8DA7}

Här är ett exempel `ADBMobileConfig.json` fil:

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
         `image` går inte att nå
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

* ”audiences”

   En array med objekt som definierar hur meddelandet ska visas:

   * ”key”

      Variabelnamn att söka efter i träffen, och det är obligatoriskt.

   * ”matches”

      Typ av matchare som används vid jämförelsen:

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

      En array med värden som används för att matcha mot värdet för variabeln som namnges i följande:

      * key
      * med matchningstypen i
      * matchar


* ”triggers”

   Samma som målgrupper, men här är åtgärderna i stället för målgruppen:

   * ”key”
   * ”matches”
   * ”values”
