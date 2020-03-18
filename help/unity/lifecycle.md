---
description: 'null'
keywords: Unity
seo-description: 'null'
seo-title: Implementera livscykel
solution: Marketing Cloud,Developer
title: Implementera livscykel
uuid: 7ff2c194-569c-42a6-922d-dccd2aa9eb8d
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Implementera livscykel{#implement-lifecycle}

Mer information om mått och mått som kan mätas automatiskt av mobilbiblioteket när livscykeln har implementerats finns i [Livscykelvärden i Android](/help/android/metrics.md) eller [Livscykel i iOS](/help/ios/metrics.md).

## iOS

Livscykelstatistik samlas automatiskt in i iOS.

## Android

I Unity-skriptet anger du programkontexten för Android SDK. Lägg till följande kod i funktionen `Awake()` för FIRST-scenen:

```java
void Awake()
 {
  ...
  ADBMobile.SetContext();
  ...
 }
```

Om du vill samla in livscykelvärden lägger du till följande kod i alla dina scenskript:

```java
void OnEnable()
 {
  ...
  ADBMobile.CollectLifecycleData (); 
  ...
 }
 
 void OnDisable()
 {
  ...
  ADBMobile.PauseCollectingLifecycleData (); 
  ...
 }
  
 void OnApplicationPause(bool isPaused) 
 {
  ...
  if (isPaused) {
   ADBMobile.PauseCollectingLifecycleData (); 
  }  
  else {
   ADBMobile.CollectLifecycleData(); 
  }
  ...
 }
```

