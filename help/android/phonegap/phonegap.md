---
description: Med denna plugin kan du skicka Android AppMeasurement-anrop från ditt PhoneGap-projekt.
keywords: android;library;mobile;sdk
seo-description: Med denna plugin kan du skicka Android AppMeasurement-anrop från ditt PhoneGap-projekt.
seo-title: PhoneGap plug-in - översikt
solution: Marketing Cloud,Analytics
title: PhoneGap plug-in - översikt
topic: Developer and implementation
uuid: c5c32357-d8df-458a-b0e8-e0c56040241d
translation-type: tm+mt
source-git-commit: 1c387b063eedb41a52e044dc824df6a51f173ad2

---


# PhoneGap plug-in - översikt {#phonegap-plug-in}

Med denna plugin kan du skicka Android AppMeasurement-anrop från ditt PhoneGap-projekt. Information om hur du skapar ett PhoneGap-projekt finns i [PhoneGap](https://helpx.adobe.com/experience-manager/6-4/mobile/using/phonegap.html).

## Ny version av Adobe Experience Platform Mobile SDK

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för att få den senaste dokumentationen.

Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya SDK:er för Adobe Experience Platform Mobile kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* Gå till Adobe Experience Platform Launch för att komma igång.
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).


## Installera plugin-programmet med npm {#section_43229E57C16944C0B51531CB92089189}

Kör följande kommando:

```java
cordova plugin add adobe-mobile-services
```

## Installera plugin-programmet manuellt {#section_EA1FD59C484D44878AB509954DEE6037}

## Inkludera plugin-programmet

1. Dra `ADBMobile_PhoneGap.java` filen till din `src` mapp.

   Om du vill flytta den här filen klickar du på **[!UICONTROL OK]**.

1. Dra `ADB_Helper.js` filen till den mapp som innehåller `index.html` filen

   Om du vill flytta den här filen klickar du på **[!UICONTROL OK]**.

1. I `res/xml` mappen öppnar du `config.xml` filen och registrerar ett nytt plugin-program genom att lägga till följande:

   ```xml
   <feature name="ADBMobile_PhoneGap"> 
     <param name="android-package" value="[YOUR_PACKAGE_NAME].ADBMobile_PhoneGap" /> 
   </feature>
   ```

   Om ditt paket till exempel har namnet `com.example.phonegaptest`är ditt `android-package` värde följande:

   ```xml
   <param name="android-package" value="com.example.phonegaptest.ADBMobile_PhoneGap" />
   ```

## Inkludera AppMeasurement-biblioteket

1. Information om hur du hämtar AppMeasurement-biblioteket finns i [Hämta SDK](/help/android/getting-started/dev-qs.md).
1. Dra `adobeMobileLibrary.jar` filen till din `src` mapp.

   Om du vill flytta den här filen klickar du på **[!UICONTROL OK]**.

1. Högerklicka på filen adobeMobileLibrary.jar och välj **[!UICONTROL Add as Library]**.
1. Ange namn, nivå och plats för biblioteket utifrån kraven för ditt projekt.
1. Dra `ADBMobileConfig.json` filen till `assets` mappen i programmets rot.
1. Bekräfta att du har valt rotprogrammet och **inte** ett program i ett program.

   Om du vill flytta den här filen klickar du på **[!UICONTROL OK]**.

## Lägg till programbehörigheter

AppMeasurement-biblioteket kräver följande behörigheter för att skicka data och registrera anrop för offlinespårning:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Om du vill lägga till dessa behörigheter lägger du till följande rader i din `AndroidManifest.xml` fil, som finns i programmets projektkatalog:

```xml
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Så här aktiverar du meddelanden i appen:

Uppdatera AndroidManifest.xml för att deklarera helskärmsaktiviteten och aktivera meddelandehanteraren:

```java
<activity  
android:name="com.adobe.mobile.MessageFullScreenActivity"  
android:theme="@android:style/Theme.Translucent.NoTitleBar" /> 
<receiver android:name="com.adobe.mobile.MessageNotificationHandler" />
```

Om du väljer modal layout när du skapar ett meddelande i Adobes mobiltjänster väljer du något av följande teman:

* `Theme.Translucent.NoTitleBar.Fullscreen`
* `Theme.Translucent.NoTitleBar`
* `Theme.Translucent`

Exempel:

```java
<activity 
android:name="com.adobe.mobile.MessageFullScreenActivity" 
android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen" 
android:windowSoftInputMode="adjustUnspecified|stateHidden" /> 
<receiver android:name="com.adobe.mobile.MessageNotificationHandler" />
```

## Implementera anpassad spårning {#section_FD102B3CDAA4492FB04E56BF17E28663}

I `html` filer lägger du till följande till den `<head>` tagg där du vill använda spårning:

```
<script type="text/javascript" charset="utf-8" src="ADB_Helper.js"></script>
```

