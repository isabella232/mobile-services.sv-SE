---
description: 'null'
keywords: Unity
seo-description: 'null'
seo-title: Bygga ditt projekt
solution: Marketing Cloud,Developer
title: Bygga ditt projekt
uuid: 5550a394-6f3f-4b87-b840-89621d8a0c1e
translation-type: tm+mt
source-git-commit: 0d50c7e6674de33b8190e74c113ae010ff226e97

---


# Bygga ditt projekt{#building-your-project}

## iOS

När du skapar för iOS skapas ett Xcode-projekt. Som standard finns filerna `ADBMobileWrapper.mm` och `AdobeMobileLibrary.a` filerna i det nya projektets biblioteksgrupp. Utför följande manuella steg för att bygga din app:

1. Lägg till din `ADBMobileConfig.json` fil i projektet.

   Se till att den är medlem i bygget om några mål behövs.

1. Lägg till en länk till följande bibliotek på fliken **[!UICONTROL Build Phases]** i projektet:

   * `SystemConfiguration.framework`
(Det här biblioteket kan redan vara länkat.)

   * `libsqlite3.0.dylib`

>[!TIP]
>
>Om du vill använda lokala meddelanden i appen från SDK måste du anropa `ADBMobile.EnableLocalNotifications();` från startmetoden i den första Unity-scenen.

## Android

När du skapar för Android innehåller filen redan den `apk` på rätt plats `ADBMobileConfig.json` i filen. Som standard används även filen `AndroidManifest.xml` i din `/Plugins/Android` mapp.

Om du behöver använda en egen anpassad manifestfil bör följande ändringar läggas till.

Lägg till behörigheter för:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Om du använder meddelanden i appen lägger du till följande aktivitet och mottagare:

```java
<activity android:name="com.adobe.mobile.MessageFullScreenActivity"  
android:theme="@android:style/Theme.Translucent.NoTitleBar" />
<receiver android:name="com.adobe.mobile.MessageNotificationHandler" />
```
