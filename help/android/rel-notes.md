---
description: Versionsinformation och kända fel för Android SDK 4.x för Experience Cloud Solutions.
solution: Experience Cloud Services,Analytics
title: Versionsinformation
topic-fix: Developer and implementation
uuid: 16bb4de8-a216-47a8-928c-0b1e1421adcf
exl-id: 5cc3d031-5952-4e9b-b551-9402d3c05ccb
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---

# Versionsinformation {#release-notes}

Här är versionsinformation, kända fel och snabbkorrigeringsinformation för Android SDK 4.x för Experience Cloud Solutions:

## 3 april 2020: 4.18.2

* I App Messaging - Av säkerhetsskäl ställer nu WebViews som har skapats av SDK in egenskapen `setAllowFileAccess` till `false`.

## 12 mars 2020: 4.18.1

* Mål - Målsessions-ID har nu lagts till som en kontextdataparameter `a.target.sessionId` i den interna träffen Analytics-for-Target som skickas till Adobe Analytics.

## 16 januari 2020: 4.18.0

* Anskaffning - ett nytt API har lagts till, `Analytics.processGooglePlayInstallReferrerUrl(final String url)`, som har stöd för Google Play Install Reference API:er.

   Mer information om Install Reference API:er finns i [Använder du fortfarande InstallBroadcast? Växla till API:t Play Reference senast 1 mars 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html).

## 20 september 2019: Version 4.17.10

* Allmänt: Fast generering av språksträngar för vissa regioner på Android API-nivå 21 eller senare.

## 18 juli 2019: Version 4.17.8

* Adobe Target: Alla begäranden inkluderar nu klienten och sessionId i URL-frågeparametrarna.
* Meddelanden i appen: Korrigerade ett problem där Android-appar kraschade när ett meddelande utlöstes med en tom klickbar URL.
* Tjänst för besökar-ID: The `Visitor.appendToURL` och `Visitor.getUrlVariablesAsync` API:er dubbelkodar inte längre sina returvärden.

   Den dubbla kodningen gjorde att returvärdena från dessa API:er flaggerades av vissa säkerhetsgranskningar.

## 6 juni 2019: Version 4.17.7

* Allmänt - Nätverksanrop på Android-API-nivåer som är lägre än 20 använder nu TLS 1.1 eller TLS 1.2.
* Analys - Utökad push-anmälningsstatus för livscykeldata när push-meddelanden är aktiverade.

## 24 maj 2019: Version 4.17.6

* besökar-ID-tjänsten - `setPushIdentifier` API-anrop skickar nu ett synkroniseringsanrop till besökar-ID-tjänsten varje gång det anropas.
* Visitor ID Service - Ökade anslutnings- och lästiderna från 2 sekunder till 5 sekunder.

Mer information om aktuell och tidigare versionsinformation om alla lösningar finns i [Versionsinformation för Adobe Experience Cloud](https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html).
