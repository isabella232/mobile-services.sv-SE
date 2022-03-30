---
description: Här finns information som hjälper dig att konfigurera Android-tillägget, som gör att du kan samla in data från Android-appen.
solution: Experience Cloud Services,Analytics
title: Android Wearables Additional Notes
topic-fix: Developer and implementation
uuid: 3bcf352b-4d46-4ab3-81ec-c27e86fe9be3
exl-id: ae8cf2d1-d2b0-456b-bbd3-3980e00bbc84
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Android Wearables: ytterligare anteckningar{#android-wearables-additional-notes}

Här finns information som hjälper dig att konfigurera Android-tillägget, som gör att du kan samla in data från Android-appen.

* Tillägget Adobe Mobile Android Wearables kräver Android version 4.4 (KitKat) eller senare.
* Det finns ytterligare ett kontextvärde, `A.RunMode`, som har lagts till för att ange om data kommer från innehållsappen eller tillägget.

   * `RunMode` = `Application`

      Träffen kommer från handdatorappen.

   * `RunMode` = `Extension`

      Träffen kommer från den bärkraftiga appen.

* SDK synkroniserar automatiskt `aid`/`vid`/`visitor` `service id`/`privacy` status från handdatorappen till den bärbara appen, så ring inte `setPrivacyStatus`/`setUserIdentifier`/`idSync` från den bärkraftiga appen.
* [Meddelanden i appen](/help/android/messaging-main/messaging/messaging.md), [Mål](/help/android/target-main/target.md)och [Audience Manager](/help/android/audience-manager/audiencemgmt.md) är inaktiverade för den bärbara appen.
