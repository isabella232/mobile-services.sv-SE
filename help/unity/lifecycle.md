---
description: Mät mätvärden och mått som kan mätas automatiskt av mobilbiblioteket
keywords: Unity
solution: Experience Cloud
title: Implementera livscykel
uuid: 7ff2c194-569c-42a6-922d-dccd2aa9eb8d
exl-id: eca0cebb-6c69-4b0f-b003-c7fc422d0383
translation-type: tm+mt
source-git-commit: b9ee49ba26d4726b1f97ef36f5c2e9923361b1ee
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 2%

---

# Implementera livscykel{#implement-lifecycle}

Mer information om mått och mått som kan mätas automatiskt av det mobila biblioteket när livscykeln har implementerats finns i [Livscykelstatistik i Android](/help/android/metrics.md) eller [Livscykel i iOS](/help/ios/metrics.md).

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
