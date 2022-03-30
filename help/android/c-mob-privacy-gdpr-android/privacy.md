---
description: Den här informationen hjälper dig med en begäran om att ta bort GDPR-data.
solution: Experience Cloud Services,Analytics
title: Ange användarens avanmälningsstatus
topic-fix: Developer and implementation
uuid: f8a3e6be-44dd-494e-9cda-dbbac86d6772
exl-id: ef5160ac-5a73-4433-b217-1bd990f8456b
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Ange användarens avanmälningsstatus{#setting-the-user-s-opt-status}

Den här informationen hjälper dig med en begäran om att ta bort GDPR-data.

>[!IMPORTANT]
>
>Från och med Android SDK 4.15 anger du sekretessstatus till `unknown` innehåller träffar för Audience Manager och Experience Cloud.

Du kan kontrollera om aktiviteten Analytics, Target och Audience Manager tillåts på en enhet med följande inställningar:

* `privacyDefault` in [ADBMomobile JSON-konfiguration](/help/android/configuration/json-config/json-config.md).

   Den här inställningen styr den inledande inställningen som kvarstår tills den ändras i koden.

* The `Config.setPrivacyStatus` -metod.

   När sekretessinställningarna har ändrats med den här metoden fortsätter ändringen att gälla tills du ändrar den igen eller när du avinstallerar och installerar appen igen. Mer information om metoderna finns i [Konfigurationsmetoder](/help/android/configuration/methods.md).

I följande tabell beskrivs varje sekretessstatus:

* **Anmäl dig**

   * **Analyser**: Träffar skickas.
   * **Mål**: Mbox-begäranden skickas.
   * **Audience Manager**: Signaler och ID-synk skickas.
   * Värde i JSON-konfigurationsfilen: `optedin`
   * Värde i `setPrivacyStatus`: `MOBILE_PRIVACY_STATUS_OPT_IN`

* **Avanmäl dig**

   * **Analyser**: Träffar ignoreras.
   * **Mål**: Mbox-begäranden tillåts inte.
   * **Audience Manager**: Signaler och ID-synk tillåts inte.
   * Värde i JSON-konfigurationsfilen: `optedout`
   * Värde i `setPrivacyStatus`: `MOBILE_PRIVACY_STATUS_OPT_OUT`

* **Okänd**

   * **Analyser**: Om spårning offline **aktiverad**, träffar sparas tills sekretessstatusen ändras till att anmäla sig (träffar skickas) eller avanmäla dig (träffar ignoreras).

      Om spårning offline <b>är inte</b> aktiverat ignoreras träffar tills sekretessstatusen ändras till att anmäla sig.
   * **Mål**: Mbox-begäranden skickas.
   * **Audience Manager**: Signaler och ID-synk skickas.
   * Värde i JSON-konfigurationsfilen: `optunknown`
   * Värde i `setPrivacyStatus`: `MOBILE_PRIVACY_STATUS_UNKNOWN`

## Exempel {#section_128AC455EE024193B5D4E5A565B53D00}

```java
public void setOptIn(View view) { 
  Config.setPrivacyStatus(MobilePrivacyStatus.MOBILE_PRIVACY_STATUS_OPT_IN); 
 currentStatus = Config.getPrivacyStatus(); 
} 
public void setOptOut(View view) { 
 Config.setPrivacyStatus(MobilePrivacyStatus.MOBILE_PRIVACY_STATUS_OPT_OUT); 
 currentStatus = Config.getPrivacyStatus(); 
} 
public void setOptUnknown(View view) { 
  Config.setPrivacyStatus(MobilePrivacyStatus.MOBILE_PRIVACY_STATUS_UNKNOWN); 
 currentStatus = Config.getPrivacyStatus(); 
}
```
