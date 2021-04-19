---
description: Här finns information som hjälper dig att konfigurera Android-tillägget, som gör att du kan samla in data från Android-appen.
seo-description: Här finns information som hjälper dig att konfigurera Android-tillägget, som gör att du kan samla in data från Android-appen.
seo-title: Android Wearables Additional Notes
solution: Experience Cloud,Analytics
title: Android Wearables Additional Notes
topic-fix: Developer and implementation
uuid: 3bcf352b-4d46-4ab3-81ec-c27e86fe9be3
exl-id: ae8cf2d1-d2b0-456b-bbd3-3980e00bbc84
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Android Wearables: ytterligare anteckningar{#android-wearables-additional-notes}

Här finns information som hjälper dig att konfigurera Android-tillägget, som gör att du kan samla in data från Android-appen.

* Tillägget Adobe Mobile Android Wearables kräver Android version 4.4 (KitKat) eller senare.
* Det finns ytterligare ett kontextvärde, `A.RunMode`, som har lagts till för att ange om data kommer från behållarappen eller tillägget.

   * `RunMode` = `Application`

      Träffen kommer från handdatorappen.

   * `RunMode` =  `Extension`

      Träffen kommer från den bärkraftiga appen.

* SDK synkroniserar automatiskt statusen `aid`/`vid`/`visitor` `service id`/`privacy` från handdatorappen till den bärbara appen, så ring inte `setPrivacyStatus`/`setUserIdentifier`/`idSync` från den bärbara appen.
* [Meddelanden](/help/android/messaging-main/messaging/messaging.md) i appen,  [Target](/help/android/target-main/target.md) och  [Audience ](/help/android/audience-manager/audiencemgmt.md) Management har inaktiverats för den bärbara appen.
