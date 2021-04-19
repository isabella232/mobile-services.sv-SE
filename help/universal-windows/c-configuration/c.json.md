---
description: Information som hjälper dig att använda ADBMomobile JSON Config-filen.
seo-description: Information som hjälper dig att använda ADBMomobile JSON Config-filen.
seo-title: ADBMobileConfig.json-konfiguration
solution: Experience Cloud,Analytics
title: ADBMobileConfig.json-konfiguration
topic-fix: Developer and implementation
uuid: cbcb54a3-4b8f-4651-8ce9-2731ac988545
exl-id: 57d50d30-651c-4943-835e-1cbce7467baf
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# ADBMobileConfig.json-konfigurationsfil {#adbmobileconfig-json-config}

Information som hjälper dig att använda ADBMomobile JSON Config-filen.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target och Audience Manager. Metoderna är prefasta enligt lösningen. Konfigurationsmetoderna har prefixet &quot;Config&quot;.

* **rsids**

   (**Krävs av Analytics**) En eller flera rapportsviter för att ta emot Analytics-data. Flera rapportpaket-ID:n ska vara kommaavgränsade utan mellanrum.

   * Här är syntaxen för den här metoden:

      ```js
      "rsids" : "rsid"
      ```

      ```js
      "rsids" : "rsid1,rsid2"
      ```

* **server**

   (**Krävs av analys- och målgruppshantering**). Analys- eller Audience Management-servern, baserad på den överordnade noden. Den här variabeln ska fyllas i med serverdomänen, utan ett `"https://"`- eller `"https://"`-protokollprefix. Protokollprefixet hanteras automatiskt av biblioteket baserat på variabeln `ssl`.

   Om `ssl` är `true` skapas en säker anslutning till den här servern. Om `ssl`är `false` skapas en osäker anslutning till den här servern.

* **charset**

   Definierar den teckenuppsättning som du använder för data som skickas till Analytics. Teckenuppsättningen används för att konvertera inkommande data till UTF-8 för lagring och rapportering. Mer information finns i [s.charSet](https://docs.adobe.com/content/help/en/analytics/implementation/vars/config-vars/charset.html).

* **ssl**

   Aktiverar (`true`) eller inaktiverar (`false`) att skicka mätdata via SSL (`HTTPS`). Standardvärdet är `false`.

* **offlineEnabled**

   När det här alternativet är aktiverat (`true`) köas träffar när enheten är offline och skickas senare när enheten är online. Din rapportsvit måste vara tidsstämpelaktiverad för att du ska kunna använda offline-spårning.

   Om tidsstämplar är aktiverade för rapportsviten måste `offlineEnabled` konfigurationsegenskapen *vara* `true`. Om rapportsviten inte är tidsstämpelaktiverad måste `offlineEnabled` konfigurationsegenskapen *vara* `false`.

   Om detta inte är korrekt konfigurerat går data förlorade. Om du är osäker på om en rapportsserie är tidsstämplad eller inte kontaktar du Kundtjänst. Om du för närvarande rapporterar AppMeasurement-data till en rapportserie som även samlar in data från JavaScript, kan du behöva skapa en separat rapportserie för mobildata eller inkludera en anpassad tidsstämpel för alla JavaScript-träffar med variabeln `s.timestamp`.

   Standardvärdet är `false`.

* **lifecycleTimeout**

   Anger hur lång tid (i sekunder) som måste gå mellan det att programmet startas innan det betraktas som en ny session. Den här tidsgränsen gäller även när programmet skickas till bakgrunden och återaktiveras. Den tid som programmet lägger i bakgrunden inkluderas inte i sessionslängden.

   Standardvärdet är 300 sekunder.

* **batchLimit**

   Skicka träffar gruppvis.

   Om värdet till exempel är `50` köas träffar tills 50 lagras, skickas alla köade träffar. Kräver `offlineEnabled=true` och standardvärdet är `0` (ingen gruppering).

* **privacyDefault**

   Alternativen är:

   * `optedin` - träffar skickas omedelbart.
   * `optedout` - träffar tas bort.
   * `optunknown` - Om rapportsviten är tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla sig (träffar ignoreras). Om rapportsviten inte är tidsstämpelaktiverad ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

      Detta anger endast standardvärdet. Om det här värdet någonsin anges eller ändras i koden sparas det värde som anges av koden i det lokala lagret och används tills det ändras, eller så avinstalleras programmet och installeras sedan om.

      Standardvärdet är `optedin`.

* **poi**

   Varje POI-array innehåller POI-namnet, latituden, longituden och radien (i meter) för punktens område. POI-namnet kan vara vilken sträng som helst. När ett `trackLocation`-anrop skickas och de aktuella koordinaterna finns inom en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation`-anropet.

   * Här är kodexemplet för variabeln:

      ```js
       "poi" [ 
                ["san francisco",37.757144,-122.44812,7000], 
                ["santa cruz",36.972935,-122.01725,600] 
             ]
      ```

* **clientCode**

   (**Krävs av mål**) Din tilldelade klientkod.

* **timeout**

   Avgör hur långt målet väntar på ett svar.

Följande är ett exempel på en `ADBMobileConfig.json`-fil:

```js
{ 
    "version" : "1.0",
    "analytics" : {
        "rsids" : "coolApp",
        "server" : "my.CoolApp.com",
        "charset" : "UTF-8",
        "ssl" : true,
        "offlineEnabled" : true,
        "lifecycleTimeout" : 5,
        "privacyDefault" : "optedin",
        "poi" : [ 
                    ["san francisco",37.757144,-122.44812,7000],
                    ["santa cruz",36.972935,-122.01725,600]
                ]
    },
 "target" : {
  "clientCode" : "myTargetClientCode",
  "timeout" : 1
 },
 "audienceManager" : {
  "server" : "myServer.demdex.com"
 }
}
```
