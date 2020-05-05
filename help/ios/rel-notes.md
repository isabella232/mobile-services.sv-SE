---
description: Versionsinformation och kända fel för iOS SDK:er 4.x för Experience Cloud Solutions.
seo-description: Versionsinformation och kända fel för iOS SDK:er 4.x för Experience Cloud Solutions.
seo-title: Versionsinformation
solution: Marketing Cloud,Analytics
title: Versionsinformation
topic: Developer and implementation
uuid: e1613dc5-02a4-43a7-997a-29b4de98b4d1
translation-type: tm+mt
source-git-commit: 82b3dc38a0325b3aa733b491ddad9b59dbe84eaa

---


# Versionsinformation {#release-notes}

Här är versionsinformation, kända fel och snabbkorrigeringsinformation för iOS SDK 4.x för Experience Cloud Solutions:

**24 mars 2020: Version 4.19.2**

* Allmänt - Åtgärdade vissa läckor i målkoden.

**12 mars 2020: Version 4.19.1**

* Allmänt - En potentiell krasch som uppstod när Swift-uppräkningar inkluderades i kontextdata för spårning av anrop har åtgärdats.
* Mål - Målsessions-ID läggs nu till som kontextdataparametern a.target.sessionId i den interna analysen för Target-träff som skickas till Adobe Analytics.

**4 februari 2020: Version 4.19.0**

* Livscykel - Ett nytt API, pauseCollectingLifecycleData, har lagts till för att minska den onormala sessionslängd som rapporterats från vissa gamla iOS-enheter.

**8 november 2019: Version 4.18.9**

* I App Messaging - Korrigerade ett fel där cachelagrade eller paketerade bilder inte kunde läsas in i helskärmsmeddelandena.

**20 september 2019: Version 4.18.8**

* I App Messaging:

   * På enheter som kör iOS 10 eller senare används nu ramverket för att schemalägga lokala meddelanden för program som är länkade till `UserNotifications` `UserNotifications.framework`.
   * Helskärmsmeddelanden använder nu WKWebViews från `WebKit.framework`som måste länkas i Xcode-projektet.
   * Korrigerade ett fel där Push click-through-nyttolasten inte kunde användas som egenskaper för meddelanden i appen.
   * Korrigerade ett kraschproblem.

* Allmänt - Korrigerade ett fel där SDK-data synkroniserades med den kopplade watchOS-appen i varje Analytics-anrop.

**2 augusti 2019: Version 4.18.7**

* Återställde en ändring som introducerades i version 4.18.6 som i vissa miljöer orsakade en krasch på enheter som kör en iOS-version som är äldre än 11.0.

* Adobe Target: Egenskapen har lagts till i `requestLocationParameters` , `ADBTargetRequestObject`vilket gör det möjligt att skicka scriptId med Target-begäranden.

**18 juli 2019: Version 4.18.6**

* Adobe Target: Alla begäranden inkluderar nu klienten och klienten `sessionId` i URL-frågeparametrarna.
* Adobe Target: Korrigerade en minnesläcka.
* Tjänst för besökar-ID: API:erna `visitorAppendToURL` och `visitorGetUrlVariablesAsync` API:erna dubbelkodar inte längre sina returvärden.

   Den dubbla kodningen gjorde att returvärdena från dessa API:er flaggerades av vissa säkerhetsgranskningar.

**5 juni 2019: Version 4.18.5**

* Analys - Lägg till push-anmälningsstatus till livscykeldata när push-meddelanden är aktiverade.

**24 maj 2019: Version 4.18.4**

* Tjänst för besökar-ID - Ökade returtidsgränsen för
   `visitorGetUrlVariablesAsync` API till 30 sekunder.

* Visitor ID-tjänst - API-anropet skickar nu ett synkroniseringsanrop till besökar-ID-tjänsten varje gång det anropas. `setPushIdentifier`

Mer information om aktuell och tidigare versionsinformation för alla lösningar finns i [versionsinformationen](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)för Adobe Experience Cloud.
