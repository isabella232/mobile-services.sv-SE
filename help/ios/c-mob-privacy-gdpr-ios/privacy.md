---
description: Den här informationen hjälper dig med en begäran om att ta bort GDPR-data.
solution: Experience Cloud Services,Analytics
title: Ange användarens alternativstatus
topic-fix: Developer and implementation
uuid: 44a09a25-93c6-4e1a-b69e-710018e8b6c3
exl-id: 8fd30bea-6316-46ac-9787-8ca594545d1b
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Ange användarens avanmälningsstatus {#setting-the-user-s-opt-status}

Den här informationen hjälper dig med en begäran om att ta bort GDPR-data.

>[!IMPORTANT]
>
>Börja med Experience Cloud iOS SDK 4.15 och ange sekretessstatus till `unknown` innehåller träffar för Audience Manager och Experience Cloud.

Du kan kontrollera om Analytics-, Target- och Audience Manager-aktivitet tillåts på en enhet med följande inställningar:

* `privacyDefault` in [ADBMomobile JSON-konfiguration](/help/ios/configuration/json-config/json-config.md).

   Den här inställningen styr den inledande inställningen som kvarstår tills den ändras i koden.

* `setPrivacyStatus` -metod.

   När sekretessinställningen har ändrats med den här metoden är ändringen permanent tills den ändras igen med den här metoden eller när du avinstallerar och installerar appen igen.

   Mer information om metoderna finns i [Konfigurationsmetoder](/help/ios/configuration/json-config/json-config.md).

Här är information om respektive sekretessstatus:

* **Anmäl dig**

   * Analyser: Träffar skickas.
   * Mål: Mbox-begäranden skickas.
   * Audience Manager: Signaler och ID-synk skickas.
   * Värde i JSON-konfigurationsfilen: `optedin`
   * Värde i `setPrivacyStatus`: `ADBMobilePrivacyStatusOptIn`

* **Avanmäl dig**

   * Analyser: Träffar ignoreras.
   * Mål: Mbox-begäranden tillåts inte.
   * Audience Manager: Signaler och ID-synk tillåts inte.
   * Värde i JSON-konfigurationsfilen: `optedout`
   * Värde i `setPrivacyStatus`: `ADBMobilePrivacyStatusOptOut`

* **Okänd**

   * Analyser: Om spårning offline **är** aktiverat sparas träffar tills sekretessstatusen ändras till anmälan (träffar skickas) eller avanmälan (träffar ignoreras).

      Om spårning offline **är inte** aktiverat ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.

   * Mål: Mbox-begäranden skickas.
   * Audience Manager: Signaler och ID-synk skickas.
   * Värde i JSON-konfigurationsfilen: `optunknown`
   * Värde i `setPrivacyStatus`: `ADBMobilePrivacyStatusUnknown`

## Exempel {#section_128AC455EE024193B5D4E5A565B53D00}

```objective-c
- (IBAction) setPrivacyOptIn { 
 [ADBMobile setPrivacyStatus:ADBMobilePrivacyStatusOptIn]; 
} 
- (IBAction) setPrivacyOptOut { 
 [ADBMobile setPrivacyStatus:ADBMobilePrivacyStatusOptOut]; 
} 
- (IBAction) setPrivacyOptUnknown { 
 [ADBMobile setPrivacyStatus:ADBMobilePrivacyStatusUnknown]; 
}
```
