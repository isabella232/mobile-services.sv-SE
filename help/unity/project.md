---
description: Bygga iOS-projekt
keywords: Unity
solution: Experience Cloud Services
title: Bygga ditt projekt
uuid: 5550a394-6f3f-4b87-b840-89621d8a0c1e
exl-id: 9da99392-b34e-4e36-b255-f3787e26015c
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 3%

---

# Bygga ditt projekt{#building-your-project}

## iOS

När du bygger för iOS skapas ett Xcode-projekt. Som standard är `ADBMobileWrapper.mm` och  `AdobeMobileLibrary.a` filer kommer att finnas i det nya projektets biblioteksgrupp. Utför följande manuella steg för att bygga din app:

1. Lägg till `ADBMobileConfig.json` till projektet.

   Se till att den är medlem i bygget om några mål behövs.

1. I **[!UICONTROL Build Phases]** Lägg till en länk till följande bibliotek på fliken i projektet:

   * `SystemConfiguration.framework`
(Det här biblioteket kan redan vara länkat.)

   * `libsqlite3.0.dylib`

>[!TIP]
>
>Om du vill använda lokala meddelanden i appen från SDK:n måste du ringa `ADBMobile.EnableLocalNotifications();` från startmetoden i din första Unity-scen.

## Android

När du skapar för Android `apk` filen innehåller redan `ADBMobileConfig.json` filen på rätt plats. Som standard är `AndroidManifest.xml` i `/Plugins/Android` används också.

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
