---
audience: end-user
user-guide-title: Android-guide för mobiltjänster
breadcrumb-title: Android-guide
source-git-commit: 78b7a623a7811cf0ede789c74b3ca7a80372c9f4
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 6%

---


# Android-guide för mobiltjänster{#android}

+ [Android SDK 4.x för Experience Cloud Solutions](overview.md)
+ [Versionsinformation](rel-notes.md)
+ Komma igång{#getting-started-android}
   + [Komma igång](getting-started/getting-started.md)
   + [Innan du börjar](getting-started/requirements.md)
   + [Kärnimplementering och livscykel](getting-started/dev-qs.md)
   + [Bearbetar regler och kontextdata](getting-started/proc-rules.md)
   + [Migrera till Android 4.x-biblioteket](getting-started/migration-v3.md)
+ Konfiguration{#configuration-android}
   + [Konfigurationsöversikt](configuration/configuration.md)
   + [ADBMomobile JSON-konfigurationsfil](configuration/json-config/json-config.md)
   + [Åsidosätt ADBMomobile JSON-konfigurationssökvägen](configuration/json-config/json-config-remote.md)
   + [Träffa](configuration/hit-batching.md)
   + [Konfigurationsmetoder](configuration/methods.md)
+ [Livscykelstatistik](metrics.md)
+ Analytics{#analytics-android} 
   + [Analytics - översikt](analytics-main/analytics-main.md)
   + [Spåra programtillstånd](analytics-main/states.md)
   + [Spåra appåtgärder](analytics-main/actions.md)
   + [Spåra programkrascher](analytics-main/crashes.md)
   + [Tidsbestämda åtgärder](analytics-main/timed-actions.md)
   + [Livslängd för besökare](analytics-main/lifetime-value.md)
   + Variabeln Produkter{#products-variable}
      + [Variabeln Produkter](analytics-main/products/products.md)
      + [Produktvariabel med eVars för försäljning och produktspecifika händelser](analytics-main/products/products-variable-evars-events.md)
   + [Händelseserialisering](analytics-main/event-serialization.md)
   + [Videoanalys](analytics-main/video-qs.md)
   + Eftersläpning{#postbacks}
      + [Översikt över återgång](analytics-main/postbacks/postbacks.md)
      + [Exempel på återgång](analytics-main/postbacks/postback-example.md)
      + [PII-eftersläpningar](analytics-main/postbacks/c-pii-postbacks.md)
   + [Analysmetoder](analytics-main/analytics-methods.md)
+ Förvärv{#acquisition-android}
   + [Översikt över förvärvet](acquisition-main/acquisition-main-android.md)
   + [Förvärva mobilappar](acquisition-main/acquisition.md)
   + [Anskaffningsmetoder](acquisition-main/acquisition-methods.md)
   + Spåra djuplänkar{#tracking-deep-links}
      + [Spåra djuplänkar](acquisition-main/tracking-deep-links/tracking-deep-links.md)
      + [Spåra fördröjda länkar från tredje part](acquisition-main/tracking-deep-links/c-tracking-3rd-party-deferred-deep-links.md)
   + [Testa Marketing Link-förvärv](acquisition-main/t-testing-marketing-link-acquisition.md)
   + [Testar förvärvet av V3](acquisition-main/t-testing-version-3-acquisition.md)
   + [Testa tidigare förvärv](acquisition-main/t-testing-acquisition.md)
   + [Felsöka förvärvningstestning](acquisition-main/troubleshoot-acquisition-testing.md)
+ Meddelanden{#messaging-android}
   + [Meddelandeöversikt](messaging-main/messaging-main-android.md)
   + Meddelanden i appen{#inapp-messaging}
      + [Meddelanden i appen](messaging-main/messaging/messaging.md)
      + [Felsöka meddelanden i programmet](messaging-main/messaging/in-apps-ts.md)
   + Push-meddelanden{#push-messaging}
      + [Push-meddelanden](messaging-main/push-messaging/push-messaging.md)
      + [Implementera push-meddelanden med djuplänkning](messaging-main/push-messaging/t-mob-impl-push-deeplinking-android-4x.md)
      + [Få omfattande push-meddelanden](messaging-main/push-messaging/c-set-up-rich-push-notif-android.md)
      + [Felsöka push-meddelanden](messaging-main/push-messaging/c-troubleshooting-push-messaging.md)
+ Plats{#location}
   + [Platsöversikt](location/location.md)
   + [Geografisk placering och intressepunkter](location/geo-poi.md)
   + [Beacon tracking](location/beacon.md)
+ Målgrupp{#target-android}
   + [Målöversikt](target-main/target-main.md)
   + [Målkonfiguration](target-main/target.md)
   + [Målmetoder](target-main/c-target-methods.md)
   + [Förhämta erbjudandeinnehåll i Android](target-main/c-mob-target-prefetch-android.md)
   + [Förhandsvisa mål på Android](target-main/c-mob-target-preview-android.md)
+ Experience Cloud{#experience-cloud-android}
   + [Experience Cloud - översikt](c-marketing-cloud/c-marketing-cloud.md)
   + [Experience Cloud ID-konfiguration](c-marketing-cloud/mcvid.md)
   + [Adobe Experience Platform Identity Service-metoder](c-marketing-cloud/mc-methods.md)
+ Audience Manager{#audience-manager-android}
   + [Översikt över Audience Manager](audience-manager/audience-manager.md)
   + [Audience Manager-konfiguration](audience-manager/audiencemgmt.md)
   + [Audience Manager-metoder](audience-manager/c-audience-manager-methods.md)
+ Wearables{#wearables-android}
   + [Översikt över wearables](wearables/wearables.md)
   + [Android Wearables: komma igång](wearables/android-wearable.md)
   + [Android Wearables: ytterligare anteckningar](wearables/c-android-wearables--additional-notes.md)
+ Android SDK-referens{#sdk-reference-android}
   + [Android SDK - referensöversikt](/help/android/reference/reference.md)
   + [Program-ID](/help/android/reference/app-ids.md)
   + [Spårning av besökare mellan en app och en mobil webbsajt](/help/android/reference/hybrid-app.md)
   + [Android-widgetar](/help/android/reference/widgets.md)
+ Sekretess och allmänna dataskyddsföreskrifter{#gdpr-privacy-android}
   + [Integritet och GDPR - översikt](c-mob-privacy-gdpr-android/c-mob-privacy-gdpr-android.md)
   + [Hämtar lagrade identifierare](c-mob-privacy-gdpr-android/c-mob-gdpr-ret-stored-ids-android.md)
   + [Ange användarens avanmälningsstatus](c-mob-privacy-gdpr-android/privacy.md)
+ PhoneGap-plugin{#phonegap-android}
   + [PhoneGap plug-in - översikt](phonegap/phonegap.md)
   + [PhoneGap plug-in-metoder](phonegap/phonegap-methods.md)
