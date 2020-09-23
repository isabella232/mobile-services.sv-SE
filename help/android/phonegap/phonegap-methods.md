---
description: Du kan använda iOS PhoneGap Plug-in-metoder för att slutföra en mängd olika åtgärder.
keywords: android;library;mobile;sdk
seo-description: Du kan använda iOS PhoneGap Plug-in-metoder för att slutföra en mängd olika åtgärder.
seo-title: PhoneGap plug-in-metoder
solution: Experience Cloud,Analytics
title: PhoneGap plug-in-metoder
topic: Developer and implementation
uuid: bc3db9ce-81b7-45ec-88aa-6020c1db5d9c
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 34%

---


# PhoneGap plug-in-metoder{#phonegap-plug-in-methods}

Du kan använda Android PhoneGap Plug-in-metoder för att slutföra en mängd olika åtgärder.

Lägg till följande i `html` -taggen i `<head>` filer där du vill använda spårning:

```js
<script type="text/javascript" charset="utf-8" src="ADB_Helper.js"></script>
```

## Konfigurationsmetoder {#section_CC429F68292D4601AEEF0A91445E1185}

* **getPrivacyStatus**

   Returnerar den aktuella användarens sekretessstatus.

   Här är de tillgängliga statusvärdena:

   * `ADB.optedIn`: Träffarna skickas omedelbart.
   * `ADB.optedOut`: Träffarna är bortkastade.
   * `ADB.optUnknown`: Om rapportsviten **är** tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras). Om rapportsviten inte **är** tidsstämpelaktiverad, kommer träffar att tas bort tills sekretessstatusen ändras till att anmäla sig.

      Standardvärdet anges i `ADBMobileConfig.json` filen.

   * Här är kodexemplet för den här metoden:

      ```java
      getPrivacyStatus(function (value) { myTempVal = value; }, function () {myTempVal = null;}); 
      ```

* **setPrivacyStatus**

   Anger sekretessstatus för den aktuella användaren till `status`.

   Du kan ange en av följande statusar:

   * `ADB.optedIn`: Träffarna skickas omedelbart.
   * `ADB.optedOut`: Träffarna är bortkastade.
   * `ADB.optUnknown`: Om rapportsviten **är** tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras). Om rapportsviten inte **är** tidsstämpelaktiverad, kommer träffar att tas bort tills sekretessstatusen ändras till att anmäla sig.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.setPrivacyStatus('ADB.optedIn');
      ```

* **getLifetimeValue**

   Returnerar livstidsvärdet för den aktuella användaren. Standardvärdet är 0.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.getLifetimeValue(function (value) { myTempVal = value }, function () { myTempVal = null; }); 
      ```

* **setDebugLogging**

   Aktiverar (`true`) eller inaktiverar (`false`) visning av felsökningsinformation. Som standard är variabeln `false`.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.setDebugLogging(true);
      ```

* **getVersion**

   Hämtar biblioteksversionen.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.getVersion(function (value) { versionNum = value }, function () { versionNum = 1.0;});
      ```

* **trackingIdentifier**

   Returnerar den automatiskt genererade besökaridentifieraren.

   Detta är ett programspecifikt, unikt besökar-ID som genereras när appen startas första gången och som lagras och används från den tidpunkten. Detta ID bevaras mellan programuppgraderingar och tas bort när programmet avinstalleras.

   >[!TIP]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas och lagras det tidigare besökar-ID:t (anpassat eller automatiskt genererat) som en anpassad användaridentifierare. Mer information finns `getUserIdentifier` nedan. Detta ID bevarar besöksdata mellan SDK-uppgraderingar.

   För nya installationer på 4.x SDK används användaridentifieraren `null` och spårningsidentifieraren.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackingIdentifier(function (value) { myTempVal = value; }, function () { myTempVal = null; }); 
      ```

* **getUserIdentifier**

   Om en kundanvändaridentifierare har angetts returneras denna identifierare; om identifieraren inte har angetts returneras `null`. Standardvärdet är `null`.

   * Här är kodexemplet för den här metoden:

      ```java
      getUserIdentifier(function(value) { myTempVal = value; }, function () { myTempVal = null; });
      ```

* **setUserIdentifier**

   Anger användaridentifieraren till `identifier`.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.setUserIdentifier('testUser');
      ```

* **setPushIdentifier**

   Anger enhetstoken för push-meddelanden.

   ```java
   getUserIdentifier(function (value) { myTempVal = value; }, function () { myTempVal = null; });
   ```

   * Här är syntaxen för den här metoden:

      ```java
      ADB.setPushIdentifier(pushIdentifier, success, fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.setPushIdentifier('test_push_identifier',function (value) { alert('success'); },function (value) { alert('fail'); }); 
      ```

* **keepLifecycleSessionAlive**

   Anger inställningen för att behålla livscykelsessionen.

   >[!IMPORTANT]
   >
   >Anrop `keepLifecycleSessionAlive` förhindrar att programmet startar en ny session nästa gång det återupptas från bakgrunden. Du bör bara använda den här metoden om programmet registrerar sig för meddelanden i bakgrunden.

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.keepLifecycleSessionAlive(); 
      ```

* **trackingSendQueuedHits**

   Tvingar biblioteket att skicka alla köade träffar oavsett aktuella gruppalternativ.

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.trackingSendQueuedHits();
      ```

* **trackingGetQueueSize**

   Hämtar eller ställer in antalet lagrade spårningsanrop i offlinekön.

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.trackingGetQueueSize(function (value) { myTempVal = value;}, function () { myTempVal = null;}); 
      ```

* **trackingClearQueue**

   Tar bort alla lagrade spårningsanrop från offlinekön.

   >[!WARNING]
   >
   >Var försiktig när du rensar kön manuellt eftersom den inte kan återföras.

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.trackingClearQueue(function (value) { myTempVal = value; }, function () { myTempVal = null; }); 
      ```

## PII-metoder {#section_DB27270D2CEB4D369E0090FD9D1A7F81}

* **collectPII**

   Skickar en PII-samlingsbegäran.

   * Här är syntaxen för den här metoden:

   ```javascript
   ADB.collectPII(piiData,success, fail);
   ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.collectPII({'k1':'v1','k2':'v2','k3':'v3'}, function (value) { alert('success') },function (value) { alert('fail') ;});
      ```


## Spårningsmetoder {#section_7946BB753A4446FE8A3ED728AEF97D04}

* **trackAdobeDeepLink**

   Spårar en klickbar Adobe-länk.

   >[!TIP]
   >
   >Om Lifecycle-anropet är en starthändelse läggs Adobe Link-data till, i annat fall skickas ett extra anrop.

   * Här är syntaxen för den här metoden:

      ```js
      ADB.trackAdobeDeepLink(deeplinkURL, success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.trackAdobeDeepLink('xyz-deeplink-url',function (value) { alert('success'); },function (value) { alert('fail') }); 
      ```

* **trackState**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel `home dashboard`, `app settings`, `cart`och så vidare. Dessa lägen liknar sidor på en webbplats och anropar `trackState` stegvisa sidvyer.

   `cData`: JSON-objekt med nyckelvärdepar som ska skickas i kontextdata.

   * Här är syntaxen för den här metoden:

      ```js
      ADB.trackState(string stateName[,JSON cData]);
      ```

   * Här är kodexempel för den här metoden:

      ```js
        ADB.trackState("login&amp;nbsp;page"); 
      ```

      ```js
        ADB.trackState("login page", {"user":"john","remember":"true"});
      ```

* **trackAction**

   Spårar en åtgärd i din app. Åtgärderna omfattar `logins`, `banner taps`, `feed subscriptions`och andra mätvärden som finns i appen och som du vill mäta.

   * Här är syntaxen för den här metoden:

      ```js
      ADB.trackAction(string action[,JSON cData]); 
      ```

   * Här är kodexemplen för den här metoden:

      ```js
        ADB.trackAction("login");
      ```

      ```js
        ADB.trackAction("login", {"user":"john","remember":"true"}); 
      ```

* **trackLocation**

   Skickar de aktuella x y-koordinaterna. Intressepunkter som definierats i filen används också för att avgöra om den plats som angetts som en parameter finns i någon av dina POI-filer. `ADBMobileConfig.json` Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation` anropet.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackLocation(x, y[,JSON cData]); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackLocation('40.431596', '-111.893713'); 
      ```

* **trackLifetime &#x200B; ValueIncrease**

   Lägger `amount` till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackLifetimeValueIncrease(amount[,JSON cData]); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackLifetimeValueIncrease('10.01'); 
      ```

* **trackTimed &#x200B; ActionStart**

   Starta en tidsbestämd åtgärd med namnet `action`.

   Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackTimedActionStart(action[,JSON cData]);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackTimedActionStart("cartToCheckout"); 
      ```

* **trackTimed &#x200B; ActionUpdate**

   Skicka in `cData` för att uppdatera kontextdata som är associerade med `action`>.

   Det `cData` som skickas läggs till i befintliga data för åtgärden och, om samma nyckel redan har definierats för `action`, skriver över data.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackTimedActionUpdate(String action[,JSON cData]);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackTimedActionUpdate("cartToCheckout",{'SampleContextDataKey3':'SampleContextDataVal3','SampleContextDataKey4':'SampleContextDataVal4'});
      ```

* **trackTimed &#x200B; ActionEnd**

   Avsluta en tidsbestämd åtgärd.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackTimedActionEnd("cartToCheckout"); 
      ```

* **trackingTimedActionExists**

   Returnerar om en tidsbestämd åtgärd pågår.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackingTimedActionExists(function (value) { myTempVal = value }, function () { myTempVal = null; }); 
      ```

## Beacon-metoder {#section_F9500D6BD95348E08E283C02B657019D}

* **trackBeacon**

   Spårar när en användare kommer in i närheten av en fyr.

   * Här är syntaxen för den här metoden:

      ```js
      ADB.trackBeacon(uuid, major, minor, proximity, cData) 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.trackBeacon('2F234454-CF6D-4A0F-ADF2-F4911BA9FFA6', 1, 2, 
      ADB.beaconUnknown, {'hp':'hp_val','hp.company':'adobe'}
      ```

* **clearCurrentBeacon**

   Rensar beacon-data efter att en användare har lämnat beacons närhet.

   * Här är syntaxen för den här metoden:

      ```js
      ADB.clearCurrentBeacon(success, fail)
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.clearCurrentBeacon(); 
      ```

## Målmetoder {#section_8670140C5A3F455E887830AFFDF91D59}

* **targetLoadRequest**

   Skickar en begäran till den konfigurerade `Target` servern och returnerar erbjudandets strängvärde.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadRequest(success, fail, name, defaultContent, parameters);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetLoadRequest(function&nbsp;(value)
      {myTempVal = value }, function () { myTempVal = null;},'bannerOffer', 'none', {'hp':'hp_val_new','hp.company':'adobe', 'hp.val2':'hp_val2'}); 
      ```

* **targetLoadOrderConfirmRequest**

   Skickar en begäran till den konfigurerade `Target` servern.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadOrderConfirmRequest(success, fail name orderId, orderTotal, productPurchaseId, parameters); 
      ```

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadRequest(function (value) { myTempVal = value }
      , function ()
      { myTempVal = null; } 
      , 'name' 'orderId' 'total', 'purchaseId',
      {'hp':'hp_val_new','hp.company':'adobe', 'hp.val2':'hp_val2'}
      ); 
      ```

* **targetClearCookies**

   Rensar `Target`cookies från delad cookie-lagring.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetClearCookies(); 
      ```

* **targetLoadRequestWithNameWithLocationParameters**

   Bearbetar en `Target` tjänstbegäran.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadRequestWithNameWithLocationParameters(
        success, fail, name, defaultContent, profileParameters, orderParameters, mboxParameters requestLocationParameters
        ); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetLoadRequestWithNameWithLocationParameters  (function () { alert('success'); }, function () { alert('fail'); }, ;'bannerOffer', 'none', {'hp':'hp_val_new','hp.company':'adobe', 'hp.val2':'hp_val2'}, {'hp':'hp_val_new','hp.company':'adobe', 'hp.val2':'hp_val2'},{'hp':'hp_val_new','hp.company':'adobe', 'hp.val2':'hp_val2'},{'hp':'hp_val_new','hp.company':'adobe', 'hp.val2':'hp_val2'});
      ```

* **targetLoadRequestWithName**

   Bearbetar en `Target` tjänstbegäran.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadRequestWithRequestName(success, fail, name, defaultContent, profileParameters, orderParameters, mboxParameters);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetLoadRequestWithName(
      function (value){ // handle target success} ,
      function() { // handle target failure }, 
      "mboxName",
      "defaultContent",
      {"profileParameters":"profileParametervalues"}
      {"orderId" : "32FGJ4XK" , "orderTotal" : "123.33" , "purchasedProductIds":"[46,34]" }
      {"mboxParameters":"mboxParametersvalues"}
      );
      ```

* **targetSessionID**

   Hämtar värdet för den `SessionID` cookie som returnerades för besökaren av målservern.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetSessionID (success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetSessionID(function (value) { alert(value) },function (value){ alert('fail'); });  
      ```

* **targetPcID**

   Hämtar värdet för den `PcID` cookie som returneras för den här besökaren av `Target` servern.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetPcID (success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetPcID(function  (value) { alert(value) },function (value) { alert('fail'); });
      ```

* **targetSetThirdPartyID**

   Anger det anpassade besökar-ID:t för Target.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetSetThirdPartyID(thirdPartyID, success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetSetThirdPartyID('test-third-party-id' function (value) { alert('success'); },function (value) { alert('fail'); }); 
      ```

* **targetThirdPartyID**

   Hämtar det anpassade besökar-ID:t för Target.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetThirdPartyID(success, fail);
      ```

   * Här följer ett kodexempel för den här metoden:

      ```java
       ADB.targetThirdPartyID(function (value) { alert(value); },function (value) { alert('fail')__;});
      ```

## Anskaffningsmetoder {#section_EDEA25C4B2884487827069E9257A0BA6}

* **purchaseCampaignStartForApp**

   Skickar en begäran till din konfigurerade målserver och returnerar erbjudandets strängvärde.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.acquisitionCampaignStartForApp(appId, data, success, fail); 
      ```

   * Här är kodexemplen för den här metoden:

      ```java
      ADB.acquisitionCampaignStartForApp(“appId”, {‘key’:‘value’}, function() {…}, function() {…}));
      ```

      ```java
      ADB.acquisitionCampaignStartForApp(“appId”, {‘key’:‘value’});  
      ```

## Annonsidentifierare {#section_194607D101B047A19C51B19E176E1500}

I huvudaktiviteten som genereras av Cordova anropar du `Config.submitAdvertisingIdentifierTask()` i `onResume()` metoden. Mer information finns i [Konfigurationsmetoder](/help/android/configuration/methods.md).

## Audience Manager-metoder {#section_1FD12B29A0AF41D3BEACBB3D624EA0E4}

* **audiensGetVisitorProfil**

   Hämtar besökarens profil.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceGetVisitorProfile(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.audienceGetVisitorProfile(function(value) { profile = value;}, function() { profile = null; }); 
      ```

* **audiensGetDpuuid**

   Returnerar DPUID.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceGetDpuuid(success fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.audienceGetDpuuid(function(value) { dpuuid = value;}, function(){dpuuid = null; }); 
      ```

* **audiensGetDpid**

   Returnerar DPID.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceGetDpid(success, fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.audienceGetDpid(function(value){dpid = value;}, function() {dpid =  null;}); 
      ```

* **auditionSetDpidAndDpuuid**

   Anger DPID och DPUID.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceSetDpidAndDpuuid(dpid, dpuuid, success, fail); 
      ```

   * Här är kodexemplen för den här metoden:

      ```java
      ADB.audienceSetDpidAndDpuuid(‘dpid’, ‘dpuuid’, function() {…}, function(){…};
      ```

      ```java
      ADB.audienceSetDpidAndDpuuid(‘dpid’, ‘dpuuid’); 
      ```

* **audiensSignalWithData**

   Bearbetar en tjänstbegäran i Audience Manager.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceSignalWithData(success, fail, data);
      ```

   * Här är kodexemplen för den här metoden:

      ```java
       ADB.audienceSignalWithData(function() {}, function() {} {‘key1’: ’value1’ ‘key2’: ‘value2’}); 
      ```

      ```java
      ADB.audienceSignalWithData({‘key1’: ’value1’, ‘key2’:‘value2’}); 
      ```

* **audiensReset**

   Audience Manager UUID och tömmer den aktuella besökarprofilen.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.audienceReset();
      ```

## ID-tjänstmetoder {#section_840B4FAEA55B466F9754148ABA15EBDA}

* **visitorGetMarketingCloudId**

   Returnerar Experience Cloud-ID från ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorGetMarketingCloudId(success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorGetMarketingCloudId(function (value) { mcid = value;},function (){ mcid = null;});
      ```

* **visitorSyncIdentifiers**

   Synkroniserar de angivna identifierarna med ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorSyncIdentifiers(identifiers, success, fail); 
      ```

   * Här är kodexemplen för den här metoden:

      ```java
      ADB.visitorSyncIdentifiers({‘key_id_1’:’value_id_1’}, function() {…}, function() {…}));
      ```

      ```java
      ADB.visitorSyncIdentifiers({‘key_id_1’: ‘value_id_1’});  
      ```

* **visitorSyncIdentifiersWithAuthenticationState**

   Synkroniserar de angivna identifierarna till ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorSyncIdentifiersWithAuthenticationState
      (identifiers, authenticationState, success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorSyncIdentifiersWithAuthenticationState({'k1':'v1','k2':'v2','k3':'v3'}, ADB.mobileVisitorAuthenticationStateAuthenticated, function (value) { alert('success'); },function (value) { alert('fail'); }); 
      ```

* **visitorSyncIdentifierWithType**

   Synkroniserar den angivna identifieraren med ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorSyncIdentifierWithType(identifierType, identifier authenticationState, success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorSyncIdentifierWithType('test-identifier-type', 'test-identifier', ADB.mobileVisitorAuthenticationStateAuthenticated, function (value) { alert('success') },function (value) { alert('fail'); }); 
      ```

* **visitorAppendToURL**

   Lägger till besökaridentifierare till den angivna URL:en.

   * Här är syntaxen för den här metoden:

      ```java
       ADB.visitorAppendToURL(urlToAppend, success, fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorAppendToURL('test_visitor_url', function (value) alert(value);},'');
      ```

* **visitorGetIDs**

   Returnerar alla `visitorID`synkroniserade objekt.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorGetIDs (success, fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorGetIDs(function (value) { alert(value); },function (value) { alert('fail') ;}); 
      ```
