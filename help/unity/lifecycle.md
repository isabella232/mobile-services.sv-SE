---
description: Mät mätvärden och mått som kan mätas automatiskt av mobilbiblioteket
keywords: Unity
solution: Experience Cloud Services
title: Implementera livscykel
uuid: 7ff2c194-569c-42a6-922d-dccd2aa9eb8d
exl-id: eca0cebb-6c69-4b0f-b003-c7fc422d0383
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 2%

---

# Implementera livscykel{#implement-lifecycle}

Mer information om mått och mått som kan mätas automatiskt av mobilbiblioteket när livscykeln har implementerats finns i [Livscykelvärden i Android](/help/android/metrics.md) eller [Livscykel i iOS](/help/ios/metrics.md).

## iOS

Livscykelstatistik samlas automatiskt in i iOS.

## Android

I Unity-skriptet anger du programkontexten för Android SDK. Lägg till följande kod i `Awake()` funktion för din FIRST-scen:

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
