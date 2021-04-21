---
description: Bygga iOS-projekt
keywords: Unity
solution: Experience Cloud
title: Bygga ditt projekt
uuid: 5550a394-6f3f-4b87-b840-89621d8a0c1e
exl-id: 9da99392-b34e-4e36-b255-f3787e26015c
translation-type: tm+mt
source-git-commit: b9ee49ba26d4726b1f97ef36f5c2e9923361b1ee
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 3%

---

# Bygger ditt projekt{#building-your-project}

## iOS

När du skapar för iOS skapas ett Xcode-projekt. Som standard finns filerna `ADBMobileWrapper.mm` och `AdobeMobileLibrary.a` i det nya projektets biblioteksgrupp. Utför följande manuella steg för att bygga din app:

1. Lägg till din `ADBMobileConfig.json`-fil i projektet.

   Se till att den är medlem i bygget om några mål behövs.

1. Lägg till en länk till följande bibliotek på fliken **[!UICONTROL Build Phases]** i ditt projekt:

   * `SystemConfiguration.framework`
(Det här biblioteket kan redan vara länkat.)

   * `libsqlite3.0.dylib`

>[!TIP]
>
>Om du vill använda lokala meddelanden i appen från SDK måste du anropa `ADBMobile.EnableLocalNotifications();` från startmetoden i den första Unity-scenen.

## Android

När du skapar för Android innehåller `apk`-filen redan `ADBMobileConfig.json`-filen på rätt plats. Som standard används även `AndroidManifest.xml`-filen i din `/Plugins/Android`-mapp.

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
