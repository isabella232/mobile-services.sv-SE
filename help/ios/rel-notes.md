---
description: Versionsinformation och kända fel för iOS SDKs 4.x för Experience Cloud Solutions.
seo-description: Versionsinformation och kända fel för iOS SDKs 4.x för Experience Cloud Solutions.
seo-title: Versionsinformation
solution: Experience Cloud,Analytics
title: Versionsinformation
topic: Developer and implementation
uuid: e1613dc5-02a4-43a7-997a-29b4de98b4d1
translation-type: tm+mt
source-git-commit: b6c9154e925ce0a0530d4c8f0871a97198ecd840
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---


# Versionsinformation {#release-notes}

Här är versionsinformation, kända fel och snabbkorrigeringsinformation för iOS SDK 4.x för Experience Cloud Solutions:

**15 december 2020: Version 4.21.0**

* Allmänt - SDK distribueras nu med XCFrameworks för att stödja maskinvara med den nya Apple M1-arkitekturen samtidigt som stödet för den befintliga Intel-arkitekturen bibehålls.
   * VIKTIGT! För uppgradering till AdobeMobile XCFrameworks krävs Xcode 12.0 eller senare
   * VIKTIGT! Om du använder Cocoapods krävs Cocoapods 1.10.0 eller senare för uppgradering till AdobeMobile XCFrameworks

**4 november 2020: Version 4.20.0**

* Visitor ID-tjänst - En tillagd statusparameter för device_medgivande när setAdvertisingIdentifier anropas efter att annonsspårning har aktiverats/inaktiverats.
* Analys - Ett fel som fördröjde Analytics-träffar från att skickas på en installation när iAd.framework är länkat och enheten har Begränsad annonsuppspårning aktiverat har åtgärdats.

**16 juli 2020: Version 4.19.3**

* Allmänt - Korrigerade ett fel som förhindrade att URL:er med flera likhetstecken med frågeparam hanterades korrekt.

**24 mars 2020: Version 4.19.2**

* Allmänt - Åtgärdade vissa läckor i målkoden.

**12 mars 2020: Version 4.19.1**

* Allmänt - En potentiell krasch som uppstod när Swift-uppräkningar inkluderades i kontextdata för spårning av anrop har åtgärdats.
* Mål - Målsessions-ID läggs nu till som kontextdataparametern a.target.sessionId i den interna analysen för målträff som skickas till Adobe Analytics.

**4 februari 2020: Version 4.19.0**

* Livscykel - Ett nytt API, pauseCollectingLifecycleData, har lagts till för att minska den onormala sessionslängd som rapporterats från vissa gamla iOS-enheter.

**8 november 2019: Version 4.18.9**

* I App Messaging - Korrigerade ett fel där cachelagrade eller paketerade bilder inte kunde läsas in i helskärmsmeddelandena.

**20 september 2019: Version 4.18.8**

* I App Messaging:

   * På enheter som kör iOS 10 eller senare används `UserNotifications`-ramverket nu för att schemalägga lokala meddelanden för program som är länkade till `UserNotifications.framework`.
   * Helskärmsmeddelanden använder nu WKWebViews från `WebKit.framework`, som måste länkas i Xcode-projektet.
   * Korrigerade ett fel där Push click-through-nyttolasten inte kunde användas som egenskaper för meddelanden i appen.
   * Korrigerade ett kraschproblem.

* Allmänt - Korrigerade ett fel där SDK-data synkroniserades med den kopplade watchOS-appen i varje Analytics-anrop.

**2 augusti 2019: Version 4.18.7**

* Återställde en ändring som introducerades i version 4.18.6 som i vissa miljöer orsakade en krasch på enheter som kör en iOS-version som är äldre än 11.0.

* Adobe Target: Egenskapen `requestLocationParameters` har lagts till i `ADBTargetRequestObject`, vilket gör att intrycks-ID kan skickas med Target-begäranden.

**18 juli 2019: Version 4.18.6**

* Adobe Target: Alla begäranden inkluderar nu klienten och `sessionId` i URL-frågeparametrarna.
* Adobe Target: Korrigerade en minnesläcka.
* Tjänst för besökar-ID: API:erna `visitorAppendToURL` och `visitorGetUrlVariablesAsync` dubbelkodar inte längre sina returvärden.

   Den dubbla kodningen gjorde att returvärdena från dessa API:er flaggerades av vissa säkerhetsgranskningar.

**5 juni 2019: Version 4.18.5**

* Analys - Lägg till push-anmälningsstatus till livscykeldata när push-meddelanden är aktiverade.

**24 maj 2019: Version 4.18.4**

* Tjänst för besökar-ID - Ökade returtidsgränsen för
   `visitorGetUrlVariablesAsync` API till 30 sekunder.

* Visitor ID-tjänst - API-anropet `setPushIdentifier` skickar nu ett synkroniseringsanrop till besökar-ID-tjänsten varje gång det anropas.

Mer information om aktuell och tidigare versionsinformation för alla lösningar finns i [Adobe Experience Cloud Release Notes](https://docs.adobe.com/content/help/sv-SE/release-notes/experience-cloud/current.html).
