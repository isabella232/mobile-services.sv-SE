---
description: Du kan använda iOS PhoneGap Plug-in-metoder för att utföra en mängd olika åtgärder.
keywords: phonegap
seo-description: Du kan använda iOS PhoneGap Plug-in-metoder för att utföra en mängd olika åtgärder.
seo-title: PhoneGap Plug-in-metoder
solution: Marketing Cloud,Analytics
title: PhoneGap Plug-in-metoder
topic: Developer and implementation
uuid: bd830fe5-804a-4d0a-bbb6-99a6d8da6a03
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# PhoneGap plug-in-metoder {#phonegap-plug-in-methods}

Du kan använda iOS PhoneGap Plug-in-metoder för att slutföra en mängd olika åtgärder.

Lägg till följande i `html` -taggen i `<head>` filer där du vill använda spårning:

```html
<script type="text/javascript" charset="utf-8" src="ADB_Helper.js"></script>
```

## Konfigurationsmetoder {#section_CC429F68292D4601AEEF0A91445E1185}

* **getPrivacyStatus**

   Returnerar den aktuella användarens sekretessstatus. Här är de tillgängliga statusvärdena:

   * `ADB.optedIn`, där träffar skickas omedelbart.
   * `ADB.optedOut`, där träffar tas bort.
   * `ADB.optUnknown`Om rapportsviten **är** tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras). Om rapportsviten inte **är** tidsstämpelaktiverad, kommer träffar att tas bort tills sekretessstatusen ändras till att anmäla sig.\
      Standardvärdet anges i `ADBMobileConfig.json` filen.

      * Här är kodexemplet för den här metoden:

         ```javascript
         getPrivacyStatus(function (value){myTempVal = value;},function(){myTempVal = null;});
         ```

* **setPrivacyStatus**

   Anger sekretessstatus för den aktuella användaren till `status`. Du kan ange en av följande statusar:
   * `ADB.optedIn`, där träffar skickas omedelbart.
   * `ADB.optedOut`, där träffar tas bort.
   * `ADB.optUnknown` - Om rapportsviten **är** tidsstämpelaktiverad sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras).

      Om rapportsviten inte **är** tidsstämpelaktiverad, kommer träffar att tas bort tills sekretessstatusen ändras till att anmäla sig.

   * Här är kodexemplet för den här metoden:

      ```javascript
        ADB.setPrivacyStatus('ADB.optedIn'); 
      ```

* **getLifetimeValue**

   Returnerar livstidsvärdet för den aktuella användaren. Standardvärdet är 0.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.getLifetimeValue(function(value){myTempVal = value;},function(){myTempVal = null;});
      ```

* **setDebugLogging**

   Aktiverar (`true`) eller inaktiverar (`false`) visning av felsökningsinformation. Som standard är variabeln `false`.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.setDebugLogging(true);
      ```

* **getVersion**

   Hämtar biblioteksversionen.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.getVersion(function(value){versionNum = value;},function(){versionNum=1.0;}); 
      ```

* **trackingIdentifier**

   Returnerar den automatiskt genererade besökaridentifieraren. Detta är ett programspecifikt unikt besökar-ID som genereras när appen startas första gången och lagras och används från och med den tidpunkten. Detta ID bevaras mellan programuppgraderingar och tas bort när programmet avinstalleras.

   >[!TIP]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas det tidigare besökar-ID:t (anpassat eller automatiskt genererat) och lagras som en anpassad användaridentifierare (se `getUserIdentifier` nedan). Detta bevarar besöksdata mellan uppgraderingar av SDK. För nya installationer på 4.x SDK används användaridentifieraren `null`och spårningsidentifieraren.

   * Här är kodexemplet för den här metoden:

      ```javascript
       ADB.trackingIdentifier(function(value){myTempVal = value;},function(){myTempVal = null;}); 
      ```

* **getUserIdentifier**

   Returnerar den anpassade användaridentifieraren om en anpassad identifierare har angetts och returnerar `null` om ingen anpassad identifierare har angetts. Standardvärdet är `null`.

   * Här är kodexemplet för den här metoden:

      ```javascript
      getUserIdentifier(function(value){myTempVal = value;},function(){myTempVal = null;}); 
      ```

* **setUserIdentifier**

   Anger användaridentifieraren till `identifier`.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.setUserIdentifier('testUser');
      ```

* **setPushIdentifier**

   Anger enhetstoken för push-meddelanden.

   * Här är syntaxen för den här metoden:

      ```javascript
      ADB.setPushIdentifier(pushIdentifier,success,fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.setPushIdentifier('test_push_identifier',function(value){alert('success');},function(value){alert('fail');
      ```

* **keepLifecycleSessionAlive**

   Anger inställningen för att behålla livscykelsessionen.

   >[!IMPORTANT]
   >
   >Anrop `keepLifecycleSessionAlive` förhindrar att programmet startar en ny session nästa gång det återupptas från bakgrunden. Du bör bara använda den här metoden om programmet registrerar sig för meddelanden i bakgrunden.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.keepLifecycleSessionAlive();
      ```

* **trackingSendQueuedHits**

   Tvingar biblioteket att skicka alla köade träffar oavsett aktuella gruppalternativ.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.trackingSendQueuedHits();
      ```

* **trackingGetQueueSize**

   Hämtar eller ställer in antalet lagrade spårningsanrop i offlinekön.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.trackingGetQueueSize(function(value){myTempVal = value;},function(){myTempVal = null;}); 
      ```

* **trackingClearQueue**

   Tar bort alla lagrade spårningsanrop från offlinekön.

   >[!CAUTION]
   >
   >Var försiktig när du rensar kön manuellt eftersom den inte kan återföras.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.trackingClearQueue(function(value){myTempVal = value;},function(){myTempVal = null;}); 
      ```

* **keepLifecycleSessionAlive**

   Anger för SDK att nästa återupptagning från bakgrunden inte ska starta en ny session, oavsett värdet på tidsgränsen för livscykelsessionen i konfigurationsfilen.

   >[!IMPORTANT]
   >
   >Viktigt:  den här metoden är avsedd att användas för program som registrerar sig för meddelanden i bakgrunden och ska endast anropas från koden som körs medan programmet körs i bakgrunden.

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.keepLifecycleSessionAlive();
      ```

* **collectLifecycleData**

   Anger för SDK att livscykeldata ska samlas in för användning i alla lösningar i SDK. Mer information finns i [Livscykelstatistik](/help/ios/metrics.md).

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.collectLifecycleData(); 
      ```


## PII-metoder {#section_DB27270D2CEB4D369E0090FD9D1A7F81}

* **collectPII**

   Skickar en PII-samlingsbegäran.

   * Här är syntaxen för den här metoden:

      ```javascript
      ADB.collectPII(piiData,success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.collectPII({'k1':'v1','k2':'v2','k3':'v3'}, function (value) { alert('success'); },function (value) { alert('fail'); });
      ```

## Spårningsmetoder {#section_7946BB753A4446FE8A3ED728AEF97D04}

* **trackAdobeDeepLink**

   Spårar en Adobe Deep Link-klickning.

   >[!TIP]
   >
   >Om livscykelanropet är en starthändelse läggs Adobe Link-data till, annars skickas ett extra anrop.

   * Här är syntaxen för den här metoden:

      ```javascript
      ADB.trackAdobeDeepLink(deeplinkURL,success,fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.trackAdobeDeepLink('xyz-deeplink-url',function(value){alert('success');},function(value){alert('fail');}); 
      ```

* **trackPushMessageClickthrough**

   Spårar ett push-meddelande med klickfrekvens.

   * Här är syntaxen för den här metoden:

      ```javascrpt
      ADB.trackPushMessageClickthrough(userInfo,success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.trackPushMessageClickthrough({'k1':'v1','k2':'v2','k3':'v3'},function(value){alert('success');},function(value){alert('fail');}); 
      ```

* **trackLocalNotificationClickThrough**

   Spårar en klickbar lokal meddelandehändelse.

   * Här är syntaxen för den här metoden:

      ```javascript
      ADB.trackLocalNotificationClickThrough(userInfo,success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.trackLocalNotificationClickThrough({'k1':'v1','k2':'v2','k3':'v3'},function(value){alert('success');},function(value){alert('fail');}); 
      ```

* **trackState**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i din app, till exempel `home dashboard`, `app settings`och `cart`så vidare. Dessa lägen liknar sidor på en webbplats och anropar `trackState` stegvisa sidvyer. cData är ett JSON-objekt med nyckelvärdepar som skickas i kontextdata.

   * Här är syntaxen för den här metoden:

      ```javascript
      ADB.trackState(stringstateName[,JSONcData]); 
      ```

   * Här är kodexemplen för den här metoden:

      ```javascript
      ADB.trackState("loginpage");
      ```

      ```javascript
        ADB.trackState("loginpage",{"user":"john","remember":"true"});
      ```

* **trackAction**

   Spårar en åtgärd i din app. Åtgärder är sådant som inträffar i appen och som du vill mäta, inkludera `logins`, `banner taps`och `feed subscriptions` andra mätvärden.

   * Här är syntaxen för den här metoden:

      ```javascript
      ADB.trackAction(stringaction[,JSONcData]);
      ```

   * Här är kodexemplen för den här metoden:

      ```javascript
      ADB.trackAction("login");
      ```

      ```javascript
      ADB.trackAction("login",{"user":"john","remember":"true"})
      ```

* **trackActionFromBackground**

   Spårar en åtgärd som inträffade i bakgrunden. Detta förhindrar att livscykelhändelser utlöses i vissa scenarier.

   * Här är syntaxen för den här metoden:

      ```javascript
      ADB.trackActionFromBackground(stringaction[,JSONcData]); 
      ```

   * Här är kodexemplen för den här metoden:

      ```javascript
      ADB.trackActionFromBackground("login");
      ```

      ```javascript
      ADB.trackActionFromBackground("login",{"user":"john","remember":"true"});
      ```

* **trackLocation**

   Skickar de aktuella x- och y-koordinaterna. Intressepunkterna som definierats i filen används också för att avgöra om platsen som angetts som en parameter finns i någon av dina POI:er. `ADBMobileConfig.json` Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation` anropet.

   * Här är syntaxen för den här metoden:

      ```javascript
       ADB.trackLocation(x,y[,JSONcData]);
      ```

   * Här är kodexemplet för den här metoden:

      ```javascript
      ADB.trackLocation('40.431596','-111.893713');
      ```

* **trackLifetime &#x200B; ValueIncrease**

   Lägger `amount` till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackLifetimeValueIncrease(amount[,JSONcData]);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackLifetimeValueIncrease('10.01');
      ```

* **trackTimed &#x200B; ActionStart**

   Starta en tidsbestämd åtgärd med namnet `action`. Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackTimedActionStart(action[,JSONcData]);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.trackTimedActionStart("cartToCheckout"); 
      ```

* **trackTimed &#x200B; ActionUpdate**

   Skicka in `cData` för att uppdatera kontextdata som är associerade med den angivna `action`. Den `cData` inskickade filen läggs till i befintliga data för den angivna åtgärden och skriver över data om samma nyckel redan har definierats för `action`.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackTimedActionUpdate(Stringaction[,JSONcData]);
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

   Returnerar om en tidsbestämd åtgärd pågår eller inte.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.trackingTimedActionExists(function(value){myTempVal = value;},function(){myTempVal = null;});
      ```


## Målmetoder {#section_C45D2FE54AE04EB5BD24D3508F8A3212}

* **targetLoadRequest**

   Skickar begäran till den konfigurerade `Target` servern och returnerar erbjudandets strängvärde.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadRequest(success,fail,name,defaultContent,parameters); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetLoadRequest(function (value)
      {myTempVal = value;},function() {myTempVal = null;},'bannerOffer','none',{'hp':'hp_val_new','hp.company':'adobe','hp.val2':'hp_val2'}); 
      ```

* **targetLoadOrderConfirmRequest**

   Skickar en begäran till den konfigurerade målservern.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadOrderConfirmRequest(success,fail,name,orderId,orderTotal,productPurchaseId,parameters); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetLoadRequest(function(value){myTempVal=value;}
      ,function()
      {myTempVal = null; }
      ,'name','orderId','total','purchaseId'
      ,{'hp':'hp_val_new','hp.company':'adobe','hp.val2':'hp_val2'}
      ); 
      ```

* **targetClearCookies**

   Rensar målcookies från delad cookie-lagring.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetClearCookies();
      ```

* **targetLoadRequestWithNameWithLocationParameters**

   Bearbetar en Target-tjänstbegäran.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetLoadRequestWithNameWithLocationParameters(success,fail,name,defaultContent,profileParameters,orderParameters,mboxParameters,requestLocationParameters
      ); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetLoadRequestWithNameWithLocationParameters(function(){alert('success');},function(){alert('fail');},'bannerOffer','none',{'hp':'hp_val_new','hp.company':'adobe','hp.val2':'hp_val2'},{'hp':'hp_val_new','hp.company':'adobe','hp.val2':'hp_val2'},{'hp':'hp_val_new','hp.company':'adobe','hp.val2':'hp_val2'},{'hp':'hp_val_new','hp.company':'adobe','hp.val2':'hp_val2'}); 
      ```

* **targetLoadRequestWithName**

   Bearbetar en Target-tjänstbegäran.

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
      ADB.targetSessionID(success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
        ADB.targetSessionID(function(value){alert(value);},function(value){alert('fail');}); 
      ```

* **targetPcID**

   Hämtar värdet för den `PcID` cookie som returnerades för besökaren av målservern.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetPcID(success,fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetPcID(function(value){alert(value);},function(value){alert('fail');});
      ```

* **targetSetThirdPartyID**

   Anger det anpassade besökar-ID:t för Target.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetSetThirdPartyID(thirdPartyID,success,fail); 
      ```

   * Här är kodexemplet för den här gruppen:

      ```java
      ADB.targetSetThirdPartyID('test-third-party-id',function(value){alert('success');},function(value){alert('fail');}); 
      ```

* **targetThirdPartyID**

   Hämtar det anpassade besökar-ID:t för Target.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.targetThirdPartyID(success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.targetThirdPartyID(function(value){alert(value);},function(value){alert('fail');}); 
      ```

## Anskaffningsmetoder {#section_EDEA25C4B2884487827069E9257A0BA6}

* **purchaseCampaignStartForApp**

   Tillåter utvecklare att starta en app-anskaffningskampanj som om användaren hade klickat på en länk. Detta är användbart när du vill skapa länkar för manuell hämtning och hantera omdirigering av appbutiken själv (till exempel med en `SKStoreView`).

   * Här är syntaxen för den här metoden:

      ```java
      ADB.acquisitionCampaignStartForApp(appId,data,success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.acquisitionCampaignStartForApp('0652024f-adcd-49f9-9bd7-2552a4564d2f',{'extraDataKey':'extraDataValue'},success,fail); 
      ```


## Annonsidentifierare {#section_194607D101B047A19C51B19E176E1500}

I det `AppDelegate` som genereras av Cordova anropar du `[ADBMobile setAdvertisingIdentifier:]` i metoden `application:didFinishLaunchingWithOptions:` delegate. Mer information finns i [Konfigurationsmetoder](/help/ios/configuration/sdk-methods.md).

## Audience Manager-metoder {#section_1FD12B29A0AF41D3BEACBB3D624EA0E4}

* **audiensGetVisitorProfil**

   Hämtar besökarens profil.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceGetVisitorProfile();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.audienceGetVisitorProfile(function(value){profile = value;},function(){profile = null;}); 
      ```

* **audiensGetDpuuid**

   Returnerar DPUID.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceGetDpuuid(success,fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
       ADB.audienceGetDpuuid(function(value){dpuuid=value;},function(){dpuuid=null;}); 
      ```

* **audiensGetDpid**

   Returnerar DPID.

   * Här är syntaxen för den här metoden:

      ```java
       ADB.audienceGetDpid(success,fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.audienceGetDpid(function(value){dpid = value;},function(){dpid = null;}); 
      ```

* **auditionSetDpidAndDpuuid**

   Anger DPID och DPUID.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceSetDpidAndDpuuid(dpid,dpuuid,success,fail);
      ```

   * Här är kodexemplen för den här metoden:

      ```java
      ADB.audienceSetDpidAndDpuuid(‘dpid’,‘dpuuid’,function(){…},function(){…});
      ```

      ```java
      ADB.audienceSetDpidAndDpuuid(‘dpid’,‘dpuuid’);
      ```

* **audiensSignalWithData**

   Bearbetar en begäran om Audience Manager-tjänst.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.audienceSignalWithData(success,fail,data);
      ```

   * Här är kodexemplen för den här metoden:

      ```java
      ADB.audienceSignalWithData(function(){},function(){},{‘key1’:’value1’,‘key2’:‘value2’});
      ```

      ```java
      ADB.audienceSignalWithData({‘key1’:’value1’,‘key2’:‘value2’}); 
      ```

* **audiensReset**

   Återställer UUID för målgruppshanteraren och tömmer den aktuella besökarprofilen.

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.audienceReset(); 
      ```

## ID-tjänstmetoder {#section_840B4FAEA55B466F9754148ABA15EBDA}

* **visitorGetMarketingCloudId**

   Returnerar Experience Cloud-ID:t från ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorGetMarketingCloudId(success,fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorGetMarketingCloudId(function(value){mcid=value;},function(){mcid=null;}); 
      ```

* **visitorSyncIdentifiers**

   Synkroniserar de angivna identifierarna med ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorSyncIdentifiers(identifiers,success,fail);
      ```

   * Här är kodexemplen för den här metoden:

      ```java
      ADB.visitorSyncIdentifiers({‘key_id_1’:’value_id_1’},function(){…},function(){…})) 
      ```

      ```java
      ADB.visitorSyncIdentifiers({‘key_id_1’:‘value_id_1’});
      ```

* **visitorSyncIdentifiersWithAuthenticationState**

   Synkroniserar de angivna identifierarna med besökar-ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorSyncIdentifiersWithAuthenticationState(identifiers,authenticationState,success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorSyncIdentifiersWithAuthenticationState({'k1':'v1','k2':'v2','k3':'v3'},ADB.mobileVisitorAuthenticationStateAuthenticated,function(value){alert('success');},function(value){alert('fail');});
      ```

* **visitorSyncIdentifierWithType**

   Synkroniserar den angivna identifieraren med besökar-ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorSyncIdentifierWithType(identifierType,identifier,authenticationState,success,fail); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorSyncIdentifierWithType('test-identifier-type','test-identifier',ADB.mobileVisitorAuthenticationStateAuthenticated,function(value){alert('success');},function(value){alert('fail');}); 
      ```

* **visitorAppendToURL**

   Lägger till besökaridentifierare till den angivna URL:en.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorAppendToURL(urlToAppend,success,fail);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorAppendToURL('test_visitor_url',function(value){alert(value);},'');
      ```

* **visitorGetIDs**

   Returnerar alla `visitorIDs` som har synkroniserats.

   * Här är syntaxen för den här metoden:

      ```java
      ADB.visitorGetIDs(success,fail)
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      ADB.visitorGetIDs(function(value){alert(value);},function(value){alert('fail');}); 
      ```
