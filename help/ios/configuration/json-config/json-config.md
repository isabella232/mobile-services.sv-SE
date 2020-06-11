---
description: Den här informationen hjälper dig att använda ADBMobil.json-konfigurationsfilen.
seo-description: Den här informationen hjälper dig att använda ADBMobil.json-konfigurationsfilen.
seo-title: ADBMomobile JSON-konfiguration
solution: Marketing Cloud,Analytics
title: ADBMomobile JSON-konfiguration
topic: Developer and implementation
uuid: d9708d59-e30a-4f6c-ab1b-d9499855d0c2
translation-type: tm+mt
source-git-commit: 86ba045b44bf6553e80727c0d61ccdd9a552d16c
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 7%

---


# ADBMomobile JSON-konfiguration {#adbmobile-json-config}

Den här informationen hjälper dig att använda `ADBMobile.json` konfigurationsfilen.

## ADBMobileConfig.json, referens till konfigurationsfil {#section_5AD4EDF87E304980B4AC4A5657FDA8B9}

Samma config-fil kan användas för appen på flera plattformar:

>[!TIP]
>
>På **iOS** kan `ADBMobileConfig.json` filen placeras var som helst där den är tillgänglig i ditt paket.

* **förvärv**

   Möjliggör förvärv av mobilappar.

   Om det här avsnittet saknas aktiverar du förvärvet av mobilappar och hämtar SDK-konfigurationsfilen igen. Mer information finns i *referenceTimeout* nedan.

   * `server` - Förvärvsserver som kontrolleras vid den första starten för en förvärvshänvisningsprogram.
   * `appid` - Genererat ID som unikt identifierar den här appen på förvärvsservern.
   * Minsta SDK-version: 4.1

* **analyticsForwardingEnabled**

   Egenskapen i `audienceManager` objektet. Om `Audience Manager` är konfigurerad och `analyticsForwardingEnabled` är inställd på `true`vidarebefordras all Analytics-trafik också till Audience Manager. Standardvärdet är `false`.

   * Minsta SDK-version: 4.8.0

* **backdateSessionInfo**

   Gör att Adobe SDK kan uppdatera sessionsinfo.

   Sessionsinformationsträffar består för närvarande av krascher och sessionslängd och kan aktiveras eller inaktiveras.

   * Om du anger värdet `false`inaktiveras **** träffarna.

      SDK:n återgår till det beteende som gällde före 4.1, där sessionsinformationen för föregående session sammanfogades med den första träffen i efterföljande session. Adobe SDK bifogar även sessionsinformationen till den aktuella livscykeln, vilket gör att det inte går att skapa ett uppblåst besök. Eftersom antalet uppblåsta besök inte längre skapas sker en omedelbar minskning av antalet besök.

   * Om du inte anger något värde är standardvärdet `true`och träffar **aktiveras**.

      När träffarna är aktiverade uppdaterar Adobe SDK sessionsinformationen till en sekund efter den sista träffen i föregående session. Detta innebär att krasch- och sessionsdata korrelerar med rätt datum då de inträffade. En bieffekt av detta är att SDK kan skapa ett besök för den efterdaterade träffen. En träff är inaktuell vid varje ny programstart.

   * Minsta SDK-version: 4.6
   >[!IMPORTANT]
   >
   >Senare information om sessionsträffen skickas i ett sessionsinfoserveranrop, och ytterligare serveranrop kan gälla.


* **batchLimit**

   Tröskelvärde för hur många träffar som ska skickas i efterföljande anrop. Om `batchLimit` till exempel är 10 sparas varje träff före den 10:e träffen i kön. När den 10:e träffen kommer skickas alla 10 träffar i följd.

   * Standardvärdet är `0`, vilket betyder att gruppering inte är aktiverat.
   * Kräver `offlineEnabled = true`.
   * Minsta SDK-version: 4.1

* **charset**

   Definierar den teckenuppsättning som du använder för data som skickas till Analytics. Teckenuppsättningen används för att konvertera inkommande data till UTF-8 för lagring och rapportering. Mer information finns i [s.charSet](https://docs.adobe.com/content/help/en/analytics/implementation/vars/config-vars/charset.html).

   * Minsta SDK-version: 4.0

* **clientCode**

   Din tilldelade klientkod.

   >[!IMPORTANT]
   >
   >Den här variabeln krävs av Target.

   * Minsta SDK-version: 4.0

* **coopUnsafe**

   För medlemmar i Device Co-op som kräver det här värdet måste du `true`arbeta med Co-op-teamet för att begära en blocklist-flagga på ditt Device Co-op-konto. Det finns ingen självbetjäningsväg för att aktivera dessa flaggor.

   Kom ihåg följande information:

   * När `coopUnsafe` är inställt på `true`läggs `coop_unsafe=1` alltid till i träffar för Audience Manager och Visitor ID.
   * Om du aktiverar vidarebefordran på serversidan för Analytics till Audience Manager kan du även se `coop_unsafe=1` Analytics-träffar.
   Här är ytterligare information:

   * Minsta SDK-version: 4.16.1
   * Den booleska egenskapen för det objekt `marketingCloud` som, när den är inställd på `true`det, gör att enheten avanmäts från Device Co-Op i Experience Cloud.
   * Standardvärdet är `false`.
   * Den här inställningen används **endast** för Device Co-op-etablerade kunder.



* **environmentId**

   ID:t för miljön som du vill använda. Du kan ange ett giltigt ID (`environmentId=8`), och om `environmentId` inte inkluderas används standardproduktionsmiljön.

   * Minsta SDK-version: 4.14

* **lifecycleTimeout**

   Standardvärdet är 300 sekunder.

   Anger hur lång tid (i sekunder) som måste gå mellan den tidpunkt då programmet startas men innan det betraktas som en ny session. Den här tidsgränsen gäller även när programmet skickas till bakgrunden och återaktiveras. Den tid som programmet lägger i bakgrunden inkluderas inte i sessionslängden.

   * Minsta SDK-version: 4.0

* **meddelanden**

   Inställningarna för meddelanden i appen definieras automatiskt av Adobe Mobile Services. Mer information finns i avsnittet *Meddelandebeskrivning* nedan.

   * Minsta SDK-version: 4.2

* **offlineEnabled**

   När det här alternativet är aktiverat köas träffar när enheten är offline och skickas senare när enheten är online. Din rapportsvit måste vara tidsstämpelaktiverad för att du ska kunna använda offline-spårning. Standardvärdet är `false`.

   Här är viktig information:

   * Om tidsstämplar är aktiverade i rapportsviten `offlineEnabled` måste ** konfigurationsegenskapen vara true.
   * Om rapportsviten inte är tidsstämpelaktiverad `offlineEnabled` måste ** konfigurationsegenskapen vara false.

      Om detta inte är korrekt konfigurerat går data förlorade. Om du är osäker på om en rapportsserie är tidsstämplad eller aktiverad kan du kontakta kundtjänst eller hämta konfigurationsfilen från Adobe Mobile Services. Om du för närvarande rapporterar AppMeasurement-data till en rapportserie som även samlar in data från JavaScript, kan du behöva skapa en separat rapportserie för mobildata eller inkludera en anpassad tidsstämpel för alla JavaScript-träffar som använder `s.timestamp` variabeln.

   * Minsta SDK-version: 4.0

* **org**

   Anger Experience Cloud-organisations-ID för Adobe Experience Platform Identity Service.

   * Minsta SDK-version: 4.3

* **poi**

   Varje POI-array innehåller POI-namnet, latituden, longituden och radien (i meter) för punktens område. POI-namnet kan vara vilken sträng som helst. När ett `trackLocation` anrop skickas, om de aktuella koordinaterna finns i en definierad POI, fylls en kontextdatavariabel i och skickas med `trackLocation` anropet.

   * Minsta SDK-version: 4.0

   ```js
   "poi" [ 
           ["sanfrancisco",37.757144,-122.44812,7000]
           ["santacruz",36.972935,-122.01725,600]
         ] 
   ```

   >[!TIP]
   >
   >Från och med version 4.2 definieras POI i Adobe Mobile-gränssnittet och synkroniseras dynamiskt till programkonfigurationsfilen. Synkroniseringen kräver `analytics.poi` inställningen:

   ```js
   “analytics.poi”: “`https://assets.adobedtm.com/…/yourfile.json`”,
   ```

   Om den här inställningen inte är konfigurerad måste filen uppdateras så att den innehåller den här raden `ADBMobile.json` . Information om hur du hämtar en uppdaterad konfigurationsfil finns i [Innan du startar](/help/ios/getting-started/requirements.md).

* **återanslående**

   Definitionen för&quot;callback&quot;-meddelandemallen visas nedan:

   ```js
   "payload":{
       "templateurl":"",//required- will be token-expanded prior to being sent
       "templatebody":"", //optional-if this length > 0 POST will be used as transport method. This is a base-64 encoded blob,which will be decoded and token-expanded prior to being sent.
       "contenttype":"", //optional-if this is length > 0 and POST type is selected, this will be set as the Content-Typeheader. if this is not supplied for a POST request,the default will be "application/x-www-form-urlencoded"
       "timeout": 0 //optional-number of seconds to wait before timingout.Defaultis2.}
   ```

   Objektet i koden är en exempelnyttolast för en meddelandedefinition som skulle finnas i `payload` `ADBMobileConfig.json` filen. Mer information finns i [Återställningar](/help/ios/analytics-main/postback/postback.md).

   * Minsta SDK-version: 4.6

* **privacyDefault**

   * Ty `optedin`träffar skickas omedelbart.
   * Ty `optedout`träffarna tas bort.
   * Om rapportsviten till `optunknown`exempel är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla dig (träffar ignoreras).

      Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

      Detta anger bara det inledande värdet. Om det här värdet anges eller ändras i koden används det nya värdet tills det ändras igen eller när programmet avinstalleras och installeras om. Standardvärdet är `optedin`.

   * Minsta SDK-version: 4.0

* **referrerTimeout**

   Antal sekunder som SDK väntar på att hämta referensdata för hämtning vid den första starten innan timeout inträffar. Om du använder förvärv rekommenderar vi en 5-sekunderstimeout.

   >[!IMPORTANT]
   >
   >Den här variabeln krävs av förvärvet. Om variabeln är inställd på `0`, eller inte inkluderas, väntar SDK inte på förvärvsdata och förvärvsstatistik spåras inte.

   * Minsta SDK-version: 4.1

* **fjärrplatser**

   Konfigureras automatiskt och definierar Adobe-hanterade slutpunkter för dynamiska konfigurationsfiler. Den senaste uppdateringstiden för varje konfigurationsfil kontrolleras mot den aktuella versionen vid varje start och uppdateringarna hämtas och sparas.

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

   Den här variabeln ska fyllas i med serverdomänen, utan ett `https://` - eller `https://` protokollprefix. Det här prefixet hanteras automatiskt av biblioteket och baseras på `ssl` variabeln.

   Om `ssl` så är `true`fallet skapas en säker anslutning till den här servern. Om `ssl` så är `false`fallet skapas en osäker anslutning till den här servern.

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

   Objektet i koden är en exempelnyttolast för en meddelandedefinition som placeras i `payload` `ADBMobileConfig.json` filen. Mer information finns i [Återställningar](/help/ios/analytics-main/postback/postback.md).

   * Minsta SDK-version: 4.0

* **timeout**

   Anger hur länge Target väntar på ett svar.

   * Minsta SDK-version: 4.0


## Exempelfil `ADBMobileConfig.json` {#section_52FA7C71A99147AFA9BE08D2177D8DA7}

Here is a sample `ADBMobileConfig.json` file:

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

Meddelandenoden genereras automatiskt av Adobe Mobile Services och behöver vanligtvis inte ändras manuellt. Följande beskrivning tillhandahålls i felsökningssyfte:

* &quot;messageId&quot;

   * Genererat ID, obligatoriskt

* &quot;template&quot;

   * &quot;alert&quot;, &quot;fullscreen&quot; eller &quot;local&quot;
   * obligatoriskt

* &quot;nyttolast&quot;

   * &quot;html&quot;

      * endast helskärmsmall, obligatoriskt
      * html som definierar meddelandet
   * &quot;image&quot;

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
