---
description: I det här avsnittet beskrivs hur du kommer igång med att använda Xamarin-komponenter för mobila lösningar 4.x SDK.
keywords: Xamarin
seo-description: I det här avsnittet beskrivs hur du kommer igång med att använda Xamarin-komponenter för mobila lösningar 4.x SDK.
seo-title: Xamarin-komponenter för Experience Cloud Solutions 4.x SDK
solution: Marketing Cloud,Developer
title: Xamarin-komponenter för Experience Cloud Solutions 4.x SDK
uuid: e7a48107-bd0e-47d6-b49c-dfdae189ac37
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Xamarin-komponenter för Experience Cloud Solutions 4.x SDK {#xamarin-components-for-experience-cloud-solutions-x-sdk}

I det här avsnittet beskrivs hur du kommer igång med att använda Xamarin-komponenter för mobila lösningar 4.x SDK.

Senast uppdaterad: 10 **januari 2019**

## Komma igång {#section_59D434C30C8F4765A7DEFE877D5268D0}

>[!IMPORTANT]
>
>Adobe Mobile SDK är inte längre tillgängligt i Xamarin Components Store eller i NuGet Gallery. Om du vill hämta Xamarin-komponenterna går du till [GitHub](https://github.com/Adobe-Marketing-Cloud/mobile-services).


## Android {#section_9CAE1BFD359242568D8288C12A4B7A7D}

Importera ADBMomobile-komponenten till ditt Xamarin.Android-projekt:

1. Öppna Xamarin-projektet

1. Öppna **[!UICONTROL References]** och klicka på **[!UICONTROL .Net Assembly]** fliken.

1. Välj `ADBMobile.XamarinAndroidBinding.dll` från **[!UICONTROL lib/Android]** mappen.

1. Lägg till din `ADBMobileConfig.json` fil i **[!UICONTROL Assets]** projektmappen.

1. Lägg till behörigheter för:

   * `INTERNET`
   * `ACCESS_NETWORK_STATE`

   ```java
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   ```

1. Om du använder meddelanden i appen lägger du till följande aktivitet och mottagare:

   ```java
   <activity 
   android:name="com.adobe.mobile.MessageFullScreenActivity" 
   android:theme="@android:style/Theme.Translucent.NoTitleBar" />
   <receiver android:name="com.adobe.mobile.MessageNotificationHandler" />
   ```

1. Om du använder förvärv lägger du till följande mottagare:

   ```java
   <receiver android:name="com.your.package.name.GPBroadcastReceiver" android:exported="true">
   <intent-filter>
       <action android:name="com.android.vending.INSTALL_REFERRER" />
   </intent-filter>
   </receiver>
   ```

## iOS {#section_1531928DDE904D769B3987BF927D0E02}

Importera ADBMomobile-komponenten till Xamarin.iOS-projektet:

1. Öppna Xamarin-projektet.
1. Öppna **[!UICONTROL References]** och klicka på **[!UICONTROL .Net Assembly]** fliken.

1. Välj `ADBMobile.XamarinIOSBinding.dll` från **[!UICONTROL lib/ios-unified]** mappen.

1. Lägg till din `ADBMobileConfig.json` fil i projektet.


