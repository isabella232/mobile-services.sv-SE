---
description: Versionsinformation och kända fel för Android SDK 4.x för Experience Cloud Solutions.
seo-description: Versionsinformation och kända fel för Android SDK 4.x för Experience Cloud Solutions.
seo-title: Versionsinformation
solution: Marketing Cloud,Analytics
title: Versionsinformation
topic: Developer and implementation
uuid: 16bb4de8-a216-47a8-928c-0b1e1421adcf
translation-type: tm+mt
source-git-commit: 712a1107b317f02216e4df8d75fddda67a6f1feb

---


# Versionsinformation {#release-notes}

Här är versionsinformation, kända fel och snabbkorrigeringsinformation för Android SDK 4.x för Experience Cloud Solutions:

**16 januari 2020: 4.18.0**

* Anskaffning - Ett nytt API har lagts till `Analytics.processGooglePlayInstallReferrerUrl(final String url)`som stöd för Google Play Install Reference-API:er.

   Mer information om Install Reference API:er finns i Använda InstallBroadcast [ändå? Växla till API:t Play Reference senast 1 mars 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html) .

**20 september 2019: Version 4.17.10**

* Allmänt: Fast generering av språksträngar för vissa regioner på Android API-nivå 21 eller senare.

**18 juli 2019: Version 4.17.8**

* Adobe Target: Alla begäranden inkluderar nu klienten och sessionId i URL-frågeparametrarna.
* Meddelanden i appen: Korrigerade ett problem där Android-appar kraschade när ett meddelande stals med en tom klickbar-URL.
* Tjänst för besökar-ID: API:erna `Visitor.appendToURL` och `Visitor.getUrlVariablesAsync` API:erna dubbelkodar inte längre sina returvärden.

   Den dubbla kodningen gjorde att returvärdena från dessa API:er flaggerades av vissa säkerhetsgranskningar.

**6 juni 2019: Version 4.17.7**

* Allmänt - Nätverksanrop på Android-API-nivåer som är lägre än 20 använder nu TLS 1.1 eller TLS 1.2.
* Analys - Utökad push-anmälningsstatus för livscykeldata när push-meddelanden är aktiverade.

**24 maj 2019: Version 4.17.6**

* besökar-ID-tjänsten -
   `setPushIdentifier` API-anrop skickar nu asynkrona anrop till besökar-ID-tjänsten varje gång det anropas.

* Visitor ID-tjänst - Ökade anslutnings- och avläsningstiderna från 2 sekunder till 5 sekunder.


Mer information om aktuell och tidigare versionsinformation för alla lösningar finns i [versionsinformationen](https://marketing.adobe.com/resources/help/en_US/whatsnew/)för Adobe Experience Cloud.
