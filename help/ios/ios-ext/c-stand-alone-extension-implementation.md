---
description: Från och med iOS 10 kan du med Apple skapa ett tillägg som kallas för ett fristående tillägg som kan distribueras utan ett innehållande program. Med det här tillägget behöver du ingen programgrupp eftersom det inte finns något program som du kan dela data med.
seo-description: Från och med iOS 10 kan du med Apple skapa ett tillägg som kallas för ett fristående tillägg som kan distribueras utan ett innehållande program. Med det här tillägget behöver du ingen programgrupp eftersom det inte finns något program som du kan dela data med.
seo-title: Implementering av fristående tillägg
solution: Marketing Cloud,Analytics
title: Implementering av fristående tillägg
topic: Developer and implementation
uuid: 9b47f082-b78f-4611-968d-014c32ede6bc
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Fristående implementering av tillägg {#stand-alone-extension-implementation}

Från och med iOS 10 kan du med Apple skapa ett tillägg som kallas för ett fristående tillägg som kan distribueras utan ett innehållande program. Med det här tillägget behöver du ingen programgrupp eftersom det inte finns något program som du kan dela data med.

>[!IMPORTANT]
>
>Om du vill använda fristående tillägg måste du ha Mobile SDK version 4.13.0 eller senare.

## Konfigurera ditt fristående tillägg för användning med SDK {#section_B7A84603BB9D4B48BB46BE8D3B9E3CF0}

Så här konfigurerar du ditt fristående tillägg:

1. Se till att `ADBMobileConfig.json` filen är medlem i tilläggets mål.
1. Länka följande bibliotek och ramverk:

   * `AdobeMobileLibrary_Extension.a`
   * `libsqlite3.tbd`
   * `SystemConfiguration.framework`

1. I huvudvykontrollanten för tillägget anger du tilläggstypen till `ADBMobileAppExtensionTypeStandAlone` i SDK innan du slutför några SDK-relaterade aktiviteter.

   ```objective-c
   [ADBMobile setAppExtensionType:ADBMobileAppExtensionTypeStandAlone];
   ```

1. Bekräfta att appen byggs utan oväntade fel.

## Ytterligare information {#section_1C9A55E2309A44BF842310F735702B3D}

Här är ytterligare information:

* Ytterligare ett kontextdatavärde har lagts till för att ange om data kommer från din app eller ditt tillägg: `a.RunMode`

   * `a.RunMode = Application`

      Det här värdet innebär att träffen kom från innehållsappen.
   * `a.RunMode = Extension`

      Detta värde innebär att träffen kom från tillägget.

* Inget livscykelanrop aktiveras för iOS-tilläggsprogram.

