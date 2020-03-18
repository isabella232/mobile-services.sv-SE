---
description: Här är en lista över TVJS-metoder som tillhandahålls av tvOS-biblioteket.
seo-description: Här är en lista över TVJS-metoder som tillhandahålls av tvOS-biblioteket.
seo-title: TVJS-metoder
solution: Marketing Cloud,Analytics
title: TVJS-metoder
topic: Developer and implementation
uuid: a7bfa85a-0d6e-4f51-9a9e-70429c2a9806
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# TVJS-metoder {#tvjs-methods}

Här är en lista över TVJS-metoder som tillhandahålls av tvOS-biblioteket.

## Konfigurationsmetoder {#section_5F82FD2F6A0546B3B4E80DF832E11634}

* **version**

   Returnerar den aktuella versionen av Adobe Mobile-biblioteket.

   * Här är syntaxen för den här metoden:

      ```objective-c
      version()
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var sdkVersion = ADBMobile.version();
      ```

   * Returnerar: `String`

* **privacyStatus**

   Returnerar NSUInteger-representationen av den aktuella användarens sekretessstatusnummer.

   Här är alternativen:

   * `ADBMobilePrivacyStatusOptIn`: Träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut`: Träffar ignoreras.
   * `ADBMobilePrivacyStatusUnknown`: Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras).

      Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras till att anmäla sig. Standardvärdet anges i `ADBMobileConfig.json` filen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      privacyStatus()
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var privacyStatus = ADBMobile.privacyStatus();
      ```

   * Returnerar: `Number`

* **setPrivacyStatus**

   Anger sekretessstatus för den aktuella användaren till något av följande värden:

   * `ADBMobilePrivacyStatusOptIn`: Träffar skickas omedelbart.
   * `ADBMobilePrivacyStatusOptOut`: Träffar ignoreras.
   * `ADBMobilePrivacyStatusUnknown`: Om spårning offline är aktiverat sparas träffar tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla dig (träffar ignoreras).
   Om spårning offline inte är aktiverat ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

   * Här är syntaxen för den här metoden:

      ```objective-c
      setPrivacyStatus(privacyStatus)
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.setPrivacyStatus(ADBMobilePrivacyStatusOptIn);
      ```


* **lifeValue**

   Returnerar livstidsvärdet för den aktuella användaren. Standardvärdet är `0`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      lifetimeValue()
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var ltv = ADBMobile.lifetimeValue();
      ```

   * Returnerar: `Number`

* **userIdentifier**

   Returnerar användaridentifieraren om en anpassad identifierare har angetts. Returnerar noll om ingen anpassad identifierare har angetts. Standardvärdet är `nil`.

   >[!IMPORTANT]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas det tidigare anpassade eller automatiskt genererade besökar-ID:t och lagras som en anpassad användaridentifierare. Detta bevarar besöksdata mellan SDK-uppgraderingar. För nya installationer på 4.x SDK är användaridentifieraren noll tills den har angetts.

   * Här är syntaxen för den här metoden:

      ```objective-c
      userIdentifier()
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      var uid = ADBMobile.userIdentifier();
      ```

   * Returnerar: `String`

* **setUserIdentifier**

   Anger användaridentifieraren.

   * Här är syntaxen för den här metoden:

      ```objective-c
      setUserIdentifier(userId)
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.setUserIdentifier(‘myUserId’);
      ```

   * Returnerar: Ej tillämpligt

   * Parameter:  `userID`

      * Typ: Sträng
      * Ny identifierare för den här användaren.

* **setAdvertisingIdentifier**

   Anger IDFA i SDK, och om den har angetts i SDK skickas IDFA i livscykeln. IDFA kan också nås i Signals (Postbacks).

   >[!IMPORTANT]
   >
   >Hämta bara IDFA från Apple API:er om du använder en annonstjänst. Om du hämtar IDFA, och inte använder det på rätt sätt, kan din app refuseras.

   * Här är syntaxen för den här metoden:

      ```objective-c
      setAdvertisingIdentifier(idfa)
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.setAdvertisingIdentifier(‘myIdfa’);
      ```

   * Returnerar: Ej tillämpligt
   * Parameter: `idfa`
      * Typ: `String`
      * IDFA har hämtats från Apple API.

* **setDebugLogging**

   Anger inställningar för felsökningsloggning.

   * Här är syntaxen för den här metoden:

      ```objective-c
      setDebugLogging(logging)
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      `ADBMobile.setDebugLogging(true);
      ```

   * Returnerar: Ej tillämpligt
   * Parametrar: `logging`
      * Typ: `Bool`
      * Värde som anger om Adobe SDK ska logga in på felsökningskonsolen.


## Analysmetoder {#section_F3DB9BE225F84F86BE5F8D15164C0379}

* **trackStateData**

   Spårar ett apptillstånd med valfria kontextdata. Lägen är de vyer som är tillgängliga i appen, till exempel heminstrumentpanel, appinställningar, kundvagn och så vidare. Dessa lägen liknar sidor på en webbplats och trackState anropar stegvisa sidvyer.

   Om läget är tomt visas det som programnamnsprogramversion (build) i rapporter. Om du ser det här värdet i rapporter måste du ställa in läget för varje trackState-anrop.

   >[!TIP]
   >
   >Det här är det enda spårningsanropet som ökar sidvisningen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackStateData(stateName [, contextData])
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: `stateName`
         * Typ: `String`
         * Sidlägesnamn
      * Parameter: `contextData`
         * Typ: Objekt
         * Ytterligare kontextdata för den här träffen.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.trackStateData(‘homepage’, {‘userid’:12345});
      ```




* **trackActionData**

   Spårar en åtgärd i din app. Funktionsmakron är de saker som händer i appen som du vill mäta, till exempel inloggningar, banderollknappar, flödesprenumerationer och andra mätvärden.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackActionData(actionName [, contextData])
      ```

      * Returnerar: Ej tillämpligt
      * Parametrar: `actionName`
         * Typ: Sträng
         * Namnet på den åtgärd som spåras.
      * Parameter: `contextData`
         * Typ: Objekt
         * Ytterligare kontextdata för den här träffen.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.trackActionData(‘likeClicked’, {‘imageName’:’funnyKitty’});
      ```



* **trackLocationWithLatLonData**

   Skickar de aktuella latitud- och longitudkoordinaterna.

   I används även intressepunkter (POI) som definieras i `ADBMobileConfig.json` filen för att avgöra om platsen som du angav som parameter finns i någon av dina POI. Om de aktuella koordinaterna finns i en definierad POI fylls en kontextdatavariabel i och skickas med `trackLocation` anropet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackLocationWithLatLonData(lat, lon [, contextData]);
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: `lat`
         * Typ: Nummer
         * Platsens latitud.
      * Parameter: `lon`
         * Typ: Nummer
         * Platsens longitud.
      * Parameter: `contextData`
         * Typ: Objekt
         * Ytterligare kontextdata för den här träffen.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.trackLocationWithLatLonData(43.36, -116.12, null);
      ```




* **trackLifetimeValueIncreaseJsData**

   Lägger till ett belopp till användarens livstidsvärde.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackLifetimeValueIncreaseJsData(increaseAmount)
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: `increaseAmount`
         * Typ: Nummer
         * Belopp att lägga till i användarens aktuella livstidsvärde.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.trackLifetimeValueIncreaseJsData(5);
      ```


* **trackTimedActionStartData**

   Starta en tidsbestämd åtgärd med namnåtgärd. Om du anropar den här metoden för en åtgärd som redan har startats, skrivs den tidigare tidsåtgärden över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackTimedActionStartData(name [, contextData])
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: `name`
         * Typ: Sträng
         * Namnet på den tidsbestämda åtgärd som startas.
      * Parameter: `contextData`
         * Typ: Objekt
         * Ytterligare kontextdata för den här träffen.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.trackTimedActionStartData(‘level1’, {‘userId’:42423});
      ```


* **trackTimedActionUpdateData**

   Skicka data för att uppdatera kontextdata som är associerade med den angivna åtgärden.

   De data som skickas läggs till befintliga data för den angivna åtgärden, och om samma nyckel redan har definierats för åtgärden skrivs data över.

   >[!TIP]
   >
   >Det här samtalet skickar ingen träff.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackTimedActionUpdateData(name [, contextData])
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: `name`
         * Typ: Sträng
         * Namnet på den tidsbestämda åtgärd som uppdateras.
      * Parameter: `contextData`
         * Typ: Objekt
         * Ytterligare kontextdata för den här träffen.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.trackTimedActionUpdateData(‘level1’);
      ```



* **trackTimedActionEndJsLogic**

   Avsluta en tidsbestämd åtgärd.

   Om du anger en återanropsfunktion kan du komma åt de slutliga tidsvärdena. Om det inte finns något återanrop, eller om återanropet returnerar true, skickar Adobe SDK automatiskt en träff. När false returneras från återanropet ignoreras den tidsbestämda åtgärden.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackTimedActionEndJsLogic(name [, callback])
      ```

      * Returnerar: Ej tillämpligt
      * Parametrar: `name`
         * Typ: Sträng
         * Namnet på den tidsbestämda åtgärd som avslutas
      * Parameter: `callback`
         * Typ: `function(inAppDuration, totalDuration, data)`
         * Återanropsmetod som kommer att ha `inAppDuration` (tal), `totalDuration` (tal) och `data` (kontextdataobjekt) i sina parametrar.

            Du kan förhindra att den sista träffen skickas av SDK genom att returnera `false` din återanropsfunktion.
      * Här är kodexemplet för den här metoden:

         ```objective-c
         ADBMobile.trackTimedActionEndJsLogic(‘level1’, 
         function(inAppDuration, totalDuration, data) {
             // do something with final values
             return true;
             });
         ```



* **trackingTimedActionExistsJs**

   Returnerar om en tidsbestämd åtgärd pågår.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackingTimedActionExistsJs(name)
      ```

      * Returnerar: Bool
      * Parameter: `name`
         * Typ: `String`
         * Namnet på den tidsbestämda åtgärd som du måste kontrollera existensen för.
   * Här är kodexemplet för den här metoden:


      ```objective-c
      var actionExists = ADBMobile.trackTimedActionExistsJs(‘level1’);
      ```


* **trackingIdentifier**

   Returnerar den automatiskt genererade besökaridentifieraren.

   Detta är ett programspecifikt unikt besökar-ID som genereras av Adobes servrar. Om Adobes servrar inte kan nås vid tidpunkten för genereringen genereras ID:t med Apples CFUID. Värdet genereras vid den första starten och lagras och används från den tidpunkten. Detta ID bevaras mellan programuppgraderingar, sparas och återställs under standardprocessen för säkerhetskopiering av program och tas bort när programmet avinstalleras.

   >[!TIP]
   >
   >Om ditt program uppgraderar från Experience Cloud 3.x till 4.x SDK hämtas det tidigare anpassade eller automatiskt genererade besökar-ID:t och lagras som en anpassad användaridentifierare. Detta bevarar besöksdata mellan SDK-uppgraderingar. För nya installationer på 4.x SDK används användaridentifieraren `nil`och spårningsidentifieraren. Mer information finns på raden userIdentifier nedan.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackingIdentifier()
      ```

      * Returnerar: `String`
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var trackingId = ADBMobile.trackingIdentifier();
      ```


* **trackingSendQueuedHits**

   Tvingar biblioteket att skicka alla träffar i offlinekön oavsett hur många som står i kö.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackingSendQueuedHits()
      ```

      * Returnerar: Ej tillämpligt
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:


      ```objective-c
      ADBMobile.trackingSendQueuedHits();
      ```


* **trackingClearQueue**

   Tar bort alla träffar från offlinekön.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackingClearQueue()
      ```

      * Returnerar: Ej tillämpligt
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.trackingClearQueue();
      ```


* **trackingGetQueueSize**

   Hämtar antalet träffar som för närvarande finns i offlinekö.

   * Här är syntaxen för den här metoden:

      ```objective-c
      trackingGetQueueSize()
      ```

      * Returnerar: Nummer
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var queueSize = ADBMobile.trackingGetQueueSize();
      ```


## Audience Manager-metoder {#section_0155C4DF04644EDAAF6159C420A158DE}

* **publikVisitorProfil**

   Returnerar den besökarprofil som senast hämtades.

   Returnerar null om ingen signal har skickats ännu. Besökarprofilen sparas i `NSUserDefaults` så att du enkelt kan komma åt den när du startar appen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      audienceVisitorProfile()
      ```

      * Returnerar: Objekt
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var profile = ADBMobile.audienceVisitorProfile();
      ```


* **audiensDpid**

   Returnerar aktuellt DPID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      audienceDpid()
      ```

      * Returnerar: Sträng
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var dpid = ADBMobile.audienceDpid();
      ```


* **audiensDpuuid**

   Returnerar aktuellt DPUID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      audienceDpuuid()
      ```

      * Returnerar: `String`
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var dpuuid = ADBMobile.audienceDpuuid();
      ```


* **auditionSetDpidDpuuid**

   Ställer in dpid och dpuuid, och om de ställs in skickas de med varje signal.

   * Här är syntaxen för den här metoden:

      ```objective-c
      audienceSetDpidDpuuid(dpid, dpuuid)
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: `dpid`
         * Typ: `String`
         * DataProvider-ID för Audience Manager.
      * Parameter: `dpuuid`
         * Typ: `String`
         * Identifierare för kombinationen av användare och dataleverantör.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.audienceSetDpidDpuuid(‘myDpid’, ‘userDpuuid’);
      ```


* **audiensSignalWithDataJsCallback**

   Skickar en signal till Audience Manager med egenskaper och hämtar matchande segment som returneras i en callback-funktion.

   * Här är syntaxen för den här metoden:

      ```objective-c
      audienceSignalWithDataJsCallback(traits [, callback])
      ```

      * Parameter: `traits`
         * Typ: Objekt
         * Skräddarsydd ordlista för den här användaren.
      * Parameter: `callback`
         * Typ: function(profile)
         * Den profil som returneras från Audience Manager i parametern för callback-funktionen.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.audienceSignalWithDataJsCallback({‘trait’:’something’}, 
      function(profile) {
          //do something with the user’s segments found in profile
           });
      ```



* **audiensReset**

   Återställer Audience Manager UUID och tömmer den aktuella besökarprofilen.

   * Här är kodexemplet för den här metoden:

      ```objective-c
      audienceReset()
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.audienceReset();
      ```


## ID-tjänstmetoder {#section_BEB6DA612EA4423FB354B65ECC941335}

* **visitorMarketingCloudID**

   Hämtar Experience Cloud-ID:t från ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```objective-c
      visitorMarketingCloudID()
      ```

      * Returnerar: Sträng
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var mcid = ADBMobile.visitorMarketingCloudID();
      ```


* **visitorSyncIdentifiers**

   Förutom Experience Cloud-ID kan du ange ytterligare kund-ID:n som ska kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare, med en kundtypsidentifierare som avgränsar omfattningen av olika kund-ID:n. Den här metoden motsvarar setCustomerID:n i JavaScript-biblioteket.

   * Här är syntaxen för den här metoden:

      ```objective-c
      visitorSyncIdentifiers(identifiers)
      ```

      * Returnerar: Ej tillämpligt
      * Parameter: `identifiers`

         * Typ: `Object`
         * Identifierare som ska synkroniseras med ID-tjänsten för den här användaren.
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.visitorSyncIdentifiers({‘idType’:’idValue’});
      ```


* **visitorSyncIdentifiersAuthenticationState**

   Synkroniserar angivna identifierare till ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```objective-c
      visitorSyncIdentifiersAuthenticationState(identifiers, authState)
      ```

      * Returnerar: Ej tillämpligt
      * Parametrar: `identifiers`
         * Typ: `Object`
         * Identifierare som ska synkroniseras med ID-tjänsten för den här användaren.
      * Parameter: `authState`
         * Typ: ADBMobilVisitorAuthenticationState
         * Användarens autentiseringstillstånd och möjliga värden är:
            * `ADBMobileVisitorAuthenticationStateUnknown`
            * `ADBMobileVisitorAuthenticationStateAuthenticated`
            * `ADBMobileVisitorAuthenticationStateLoggedOut`
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.visitorSyncIdentifiersAuthenticationState({'myIdType':'valueForUser'}, ADBMobileVisitorAuthenticationStateLoggedOut)
      ```



* **visitorSyncIdentifierWithTypeIdentifierAuthenticationState**

   Synkroniserar angiven identifierartyp och angivet värde med ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```objective-c
      visitorSyncIdentifierWithTypeIdentifierAuthenticationState(idType, identifier, authState)
      ```

      * Retur: Ej tillämpligt
      * Parameter: `idType`
         * Typ: `String`
         * Typ av identifierare som du synkroniserar.
      * Parameter: `identifier`
         * Typ: `String`
         * Värdet på den identifierare som du synkroniserar.
      * Parameter: `authState`
         * Typ: Användarens ADBMobleVisitorAuthenticationStateAuthentication-tillstånd. Möjliga värden är:
            * `ADBMobileVisitorAuthenticationStateUnknown`
            * `ADBMobileVisitorAuthenticationStateAuthenticated`
            * `ADBMobileVisitorAuthenticationStateLoggedOut`
   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMobile.visitorSyncIdentifierWithTypeIdentifierAuthenticationState('myIdType', 'valueForUser', 
      ADBMobileVisitorAuthenticationStateAuthenticated);
      ```


* **visitorGetIDsJs**

   Hämtar en array med skrivskyddade ADBVisitorID-objekt. Följande kodexempel är ett exempel på ett VisitorID-objekt:

   ```js
   {
       idType: "abc",
       authenticationState: 1, 
       identifier: "123"
   }
   ```

   * Här är syntaxen för den här metoden:

      ```objective-c
      visitorGetIDsJs()
      ```

      * Returnerar: `Array [Object]`

      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var myVisitorIds = ADBMobile.visitorGetIDsJs();
      ```


## Målmetoder {#section_F9F7EC2B9B7C41AFBCA2458F9F138634}

* **targetThirdPartyID**

   Returnerar tredjeparts-ID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      targetThirdPartyID()
      ```

      * Returnerar: `String`
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var thirdPartyID = ADBMobile.targetThirdPartyID();
      ```


* **targetSetThirdPartyID**

   Anger ID för tredje part.

   * Här är syntaxen för den här metoden:

      ```objective-c
      targetSetThirdPartyID(thirdPartyID)
      ```

      * Returnerar: Ej tillämpligt
      * Parametrar: `thirdPartyID`
         * Typ: `String`
         * Tredjeparts-ID som ska användas för målbegäranden.
   * Här är kodexemplet för den här metoden:

   ```objective-c
   ADBMobile.targetSetThirdPartyID(‘thirdPartyID’);
   ```

* **targetPcID**

   Returnerar PcID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      targetPcID()
      ```

      * Returnerar: `String`
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var pcID = ADBMobile.targetPcID();
      ```


* **targetSessionID**

   Returnerar sessions-ID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      targetSessionID()
      ```

      * Returnerar: `String`
      * Parametrar: Ingen
   * Här är kodexemplet för den här metoden:

      ```objective-c
      var sessionID = ADBMobile.targetSessionID();
      ```
