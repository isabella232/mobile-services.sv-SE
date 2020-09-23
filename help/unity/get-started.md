---
description: Med denna plugin kan du skicka Adobe Analytics-samtal från Unity-program.
keywords: Unity
seo-description: Med denna plugin kan du skicka Adobe Analytics-samtal från Unity-program.
seo-title: Unity Plug-in för iOS och Android 4.x SDK
solution: Experience Cloud
title: Unity Plug-in för iOS och Android 4.x SDK
uuid: 83289a73-982d-4472-a8c8-00b562dc80f5
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 3%

---


# Unity Plug-in för iOS och Android 4.x SDK {#unity-plug-in-for-the-ios-and-android-x-sdks}

Med denna plugin kan du skicka Adobe Analytics-samtal från Unity-program.

Senaste uppdatering: **10 mars 2020**
* [Unity-v4.19.0](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases/tag/v4.19.0-Unity)

## Komma igång {#section_246D1F9B32ED47EABC41BDA8D0BD0CC7}

Hämta ADBMomobile.unitypackage-filen från GitHub.

Nedan finns innehållet i `ADBMobile.unitypackage` filen:

* Resurser (rot)

   * ADBMomobile

   * Plugins

      * ADBMobile.cs
      * Android

         * adobeMobileLibrary-{version}.jar
         * AndroidManifest.xml
         * resurser

            * ADBMobileConfig.json
      * iOS

         * ADBMobile.h
         * ADBMobileConfig.json
         * ADBMobileWrapper.h
         * ADBMobileWrapper.mm
         * AdobeMobileLibrary.a


**Valfria mappar**: Mappen *Demo* innehåller Unity-scener och exempelkod.

## Importera ADBMomobile-plugin-programmet till Unity-projektet {#section_35FB6DAE49FB4FA1ACB749A1F9480FE0}

1. Öppna Unity-projektet.
1. Dubbelklicka **[!UICONTROL ADBMobile.unitypackage]**.
1. Markera de mappar som du vill importera.
