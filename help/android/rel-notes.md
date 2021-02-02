---
description: Versionsinformation och kända fel för Android SDK 4.x för Experience Cloud Solutions.
seo-description: Versionsinformation och kända fel för Android SDK 4.x för Experience Cloud Solutions.
seo-title: Versionsinformation
solution: Experience Cloud,Analytics
title: Versionsinformation
topic: Developer and implementation
uuid: 16bb4de8-a216-47a8-928c-0b1e1421adcf
translation-type: tm+mt
source-git-commit: 8b5842068c602f3f9b1c020c1c9a686eb0e56b74
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---


# Versionsinformation {#release-notes}

Här är versionsinformation, kända fel och snabbkorrigeringsinformation för Android SDK 4.x för Experience Cloud Solutions:

**3 april 2020: 4.18.2**

* I App Messaging - Av säkerhetsskäl har WebViews som har skapats av SDK nu egenskapen setAllowFileAccess lika med false.

**12 mars 2020: 4.18.1**

* Mål - Målsessions-ID läggs nu till som kontextdataparametern a.target.sessionId i den interna Analytics-for-Target-träff som skickas till Adobe Analytics.

**16 januari 2020: 4.18.0**

* Förvärv - Ett nytt API, `Analytics.processGooglePlayInstallReferrerUrl(final String url)`, har lagts till som stöd för Google Play Install Reference-API:er.

   Mer information om Install Reference API:er finns i [Använder du fortfarande InstallBroadcast? Växla till API:t Play Reference senast 1 mars 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html).

**20 september 2019: Version 4.17.10**

* Allmänt: Fast generering av språksträngar för vissa regioner på Android API-nivå 21 eller senare.

**18 juli 2019: Version 4.17.8**

* Adobe Target: Alla begäranden inkluderar nu klienten och sessionId i URL-frågeparametrarna.
* Meddelanden i appen: Korrigerade ett problem där Android-appar kraschade när ett meddelande stals med en tom klickbar-URL.
* Tjänst för besökar-ID: API:erna `Visitor.appendToURL` och `Visitor.getUrlVariablesAsync` dubbelkodar inte längre sina returvärden.

   Den dubbla kodningen gjorde att returvärdena från dessa API:er flaggerades av vissa säkerhetsgranskningar.

**6 juni 2019: Version 4.17.7**

* Allmänt - Nätverksanrop på Android-API-nivåer som är lägre än 20 använder nu TLS 1.1 eller TLS 1.2.
* Analys - Utökad push-anmälningsstatus för livscykeldata när push-meddelanden är aktiverade.

**24 maj 2019: Version 4.17.6**

* besökar-ID-tjänsten -
   `setPushIdentifier` API-anrop skickar nu ett synkroniseringsanrop till besökar-ID-tjänsten varje gång det anropas.

* Tjänst för besökar-ID - Ökade anslutningen och läsningen
timeout från 2 sekunder till 5 sekunder.


Mer information om aktuell och tidigare versionsinformation för alla lösningar finns i [Adobe Experience Cloud Release Notes](https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html).
