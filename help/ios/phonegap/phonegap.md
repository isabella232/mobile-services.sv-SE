---
description: Med denna plugin kan du skicka iOS AppMeasurement-anrop från ditt PhoneGap-projekt.
keywords: phonegap
seo-description: Med denna plugin kan du skicka iOS AppMeasurement-anrop från ditt PhoneGap-projekt.
seo-title: PhoneGap-plugin
solution: Experience Cloud,Analytics
title: PhoneGap-plugin
topic: Developer and implementation
uuid: f88bcf10-1f9e-4c97-b348-40db797c9923
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---


# PhoneGap plug-in{#phonegap-plug-in}

Med denna plugin kan du skicka iOS AppMeasurement-anrop från ditt PhoneGap-projekt.

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK:er kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).


## Skapa ett PhoneGap-projekt

Information om hur du skapar ett PhoneGap-projekt finns i [PhoneGap](https://helpx.adobe.com/experience-manager/6-4/mobile/using/phonegap.html).

## Installera plugin-programmet med npm: {#section_43229E57C16944C0B51531CB92089189}

1. Kör följande kommando:

   ```
   cordova plugin add adobe-mobile-services
   ```

## Installera plugin-programmet manuellt {#section_D53BA60D488C4DB8AD2BDF90439C180A}

### Inkludera AppMeasurement-biblioteket

Så här inkluderar du AppMeasurement:

1. Dra `ADBMobile_PhoneGap.h` och `ADBMobile_PhoneGap.m` till **[!UICONTROL Plugins]** mappen i Xcode-projektet.
1. Ange följande inställningar:

   1. Välj **[!UICONTROL Copy items into destination group's folder (if needed)]**.
   1. Välj de mål där du vill använda AppMeasurement-kod.

1. Dra `ADB_Helper.js` till `www` mappen i projektet.
1. Öppna `res/xml` och registrera ett nytt plugin-program i `config.xml` mappen genom att lägga till följande:

   ```
   <feature name="ADBMobile_PhoneGap"> 
     <param name="ios-package" value="ADBMobile_PhoneGap" /> 
   </feature>
   ```

### Lägg till programbehörigheter

AppMeasurement-biblioteket kräver följande:

1. Starta Xcode IDE och öppna appen.
1. Dra **[!UICONTROL AdobeMobile]** mappen till Xcode-projektet och fyll i följande inställningar:

   1. Välj **[!UICONTROL Copy items into destination group's folder (if needed)]**.
   1. Välj **[!UICONTROL Create groups for any added folders]**.
   1. Markera de mål där du vill använda AppMeasurement-kod och klicka på **[!UICONTROL Finish]**.

   ![](assets/xcode-settings.png){width=&quot;672&quot;}

1. In the **[!UICONTROL Build Phases]** tab of your project’s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

   * `libsqlite3.dylib`
   * `SystemConfiguration.framework`

1. Bekräfta att appen byggs utan oväntade fel.

## Implementera anpassad spårning {#section_FD102B3CDAA4492FB04E56BF17E28663}

Lägg till följande i `html` -taggen i `<head>` filer där du vill använda spårning:

```html
<script type="text/javascript" charset="utf-8" src="ADB_Helper.js"></script>
```

