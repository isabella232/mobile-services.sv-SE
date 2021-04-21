---
audience: end-user
user-guide-title: iOS-handbok för mobiltjänster
breadcrumb-title: iOS-guide
translation-type: tm+mt
source-git-commit: b9ee49ba26d4726b1f97ef36f5c2e9923361b1ee
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 3%

---


# iOS-handbok för mobiltjänster {#ios}

+ [iOS SDK 4.x för Experience Cloud Solutions](overview.md)
+ [Versionsinformation](rel-notes.md)
+ Komma igång {#getting-started-ios}
   + [Komma igång - översikt](getting-started/getting-started.md)
   + [Innan du börjar](getting-started/requirements.md)
   + [Kärnimplementering och livscykel](getting-started/dev-qs.md)
   + [Bearbetar regler och kontextdata](getting-started/proc-rules.md)
   + [Snabb integrering](getting-started/swift-integration.md)
   + [Migrera till iOS-biblioteket 4.x](getting-started/migration-v3.md)
+ Konfiguration {#config-ios}
   + [Konfigurationsöversikt](configuration/configuration.md)
   + [ADBMomobile JSON-konfiguration](configuration/json-config/json-config.md)
   + [Åsidosätt ADBMomobile JSON-konfigurationssökvägen](configuration/json-config/json-config-remote.md)
   + [Träffa](configuration/hit-batching.md)
   + [Konfigurationsmetoder](configuration/sdk-methods.md)
   + [Transportsäkerhet för appar](configuration/app-transport-security.md)
+ [Livscykelstatistik](metrics.md)
+ Analytics{#analytics-ios} 
   + [Analytics - översikt](analytics-main/analytics-main.md)
   + [Spåra programtillstånd](analytics-main/states.md)
   + [Spåra appåtgärder](analytics-main/actions.md)
   + [Spåra programkrascher](analytics-main/crashes.md)
   + [Tidsbestämda åtgärder](analytics-main/timed-actions.md)
   + [Livslängd för besökare](analytics-main/lifetime-value.md)
   + Produktvariabel {#products-variable}
      + [Variabeln Produkter](analytics-main/products/products.md)
      + [Produktvariabel med eVars för försäljning och produktspecifika händelser](analytics-main/products/products-variable-evars-events.md)
   + [Händelseserialisering](analytics-main/event-serialization.md)
   + [Videoanalys](analytics-main/video-qs.md)
   + Eftersläpning {#postbacks}
      + [Översikt över återgång](analytics-main/postback/postback.md)
      + [Exempel på återanslående](analytics-main/postback/postback-example.md)
      + [PII-återanslag](analytics-main/postback/c-pii-postbacks.md)
   + [Analysmetoder](analytics-main/analytics-methods.md)
+ Förvärv {#acquisition-ios}
   + [Översikt över förvärvet](acquisition-main/acquisition-main.md)
   + [Förvärva mobilappar](acquisition-main/acquisition.md)
   + [Anskaffningsmetoder](acquisition-main/c-acquisition-methods.md)
   + Spåra djupa länkar {#tracking-deep-links}
      + [Spåra djuplänkar](acquisition-main/tracking-deep-links/tracking-deep-links.md)
      + [Spåra fördröjda länkar från tredje part](acquisition-main/tracking-deep-links/c-tracking-3rd-party-deep-deferred-links.md)
   + [Testa Marketing Link-förvärv](acquisition-main/t-testing-marketing-link-acquisition.md)
   + [Testar förvärvet av V3](acquisition-main/t-testing-version-3-acquisition.md)
   + [Testa tidigare förvärv](acquisition-main/t-testing-acquisition.md)
   + [Apple Search Ads](acquisition-main/c-apple-search-ads.md)
+ Meddelanden {#messaging-ios}
   + [Meddelandeöversikt](messaging-main/messaging-main.md)
   + Meddelanden i appen {#in-app-messaging}
      + [Meddelanden i appen](messaging-main/messaging/messaging.md)
      + [Felsökning av meddelanden i appen](messaging-main/messaging/in-apps-ts.md)
   + Push-meddelanden {#push-messaging}
      + [Push-meddelanden](messaging-main/push-messaging/push-messaging.md)
      + [Implementera push-meddelanden med djuplänkning](messaging-main/push-messaging/t-mob-imp-push-deeplinking-ios-4x.md)
      + [Få omfattande push-meddelanden](messaging-main/push-messaging/c-set-up-rich-push-notif-ios.md)
      + [Felsöka push-meddelanden](messaging-main/push-messaging/c-troubleshooting-push-messaging.md)
+ Plats {#location-ios}
   + [Platsöversikt](location/location.md)
   + [Geografisk placering och intressepunkter](location/geo-poi.md)
   + [Spårning av iBeacon](location/ibeacon.md)
+ Målgrupp {#target-ios}
   + [Målöversikt](target-main/target-main.md)
   + [Målmetoder](target-main/c-target-methods.md)
   + [Förhämta innehåll i iOS](target-main/c-mob-target-prefetch-ios.md)
   + [Förhandsvisa mål på iOS](target-main/c-mob-target-preview-ios.md)
+ Experience Cloud {#exp-cloud-ios}
   + [Experience Cloud - översikt](marketing-cloud/marketing-cloud.md)
   + [Experience Cloud ID](marketing-cloud/mcvid.md)
   + [Adobe Experience Platform Identity Service-metoder](marketing-cloud/mc-methods.md)
   + [Experience Cloud Device Co-op](marketing-cloud/t-mob-mc-device-coop-ios-.md)
+ [Audience Manager-metoder](amm/aam-methods.md)
+ Apple TV-implementering med tvOS {#apple-tv-implementation-tvos-ios}
   + [Apple TV-implementering med tvOS](apple-tv-implementation-tvos/apple-tv-implementation-tvos.md)
   + [Adobe Target for TVML/TVJS](apple-tv-implementation-tvos/target-for-tvml-tvjs.md)
   + [TVJS-metoder](apple-tv-implementation-tvos/tvjs-methods.md)
+ Implementering av iOS-tillägg {#ios-ext}
   + [Implementering av iOS-tillägg](ios-ext/ios-ext.md)
   + [Fristående implementering av tillägg](ios-ext/c-stand-alone-extension-implementation.md)
+ [Apple Watch-implementering med WatchOS 2](apple-watch-implementation-watchkit.md)
+ iOS SDK-referens {#sdk-reference-ios}
   + [iOS SDK-referens](reference/reference.md)
   + [Program-ID](reference/app-ids.md)
   + [Spårning av besökare mellan en app och en mobil webbsajt](reference/hybrid-app.md)
   + [iOS-enhetsversioner](reference/device-versions.md)
+ Sekretess och allmänna dataskyddsföreskrifter{#privacy-gdpr-ios}
   + [Sekretess och allmänna dataskyddsföreskrifter](c-mob-privacy-gdpr-ios/c-mob-privacy-gdpr-ios.md)
   + [Hämtar lagrade identifierare](c-mob-privacy-gdpr-ios/c-mob-gdpr-ret-stored-ids-ios.md)
   + [Ange användarens avanmälningsstatus](c-mob-privacy-gdpr-ios/privacy.md)
+ PhoneGap Plug-in {#phonegap-ios}
   + [PhoneGap plug-in](phonegap/phonegap.md)
   + [PhoneGap plug-in-metoder](phonegap/phonegap-methods.md)
