---
description: Information som hjälper dig att implementera livscykelvärden för Android. Livscykelstatistik samlas in automatiskt för iOS.
keywords: Xamarin
solution: Experience Cloud
title: Implementera livscykel
uuid: 6dccc12e-8b57-4231-9c74-d47bc0ac93ba
exl-id: c76e63d1-48a5-4831-85d5-f3d3e9798a43
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# Implementera livscykel {#implement-lifecycle}

Den här informationen hjälper dig att implementera livscykelvärden för Android.

>[!TIP]
>
>Livscykelstatistik samlas in automatiskt för iOS.

Information om mått och mått som kan mätas automatiskt av det mobila biblioteket efter att livscykeln har implementerats finns i [Livscykelvärden](/help/ios/metrics.md).

## iOS

I iOS samlas livscykelvärden in automatiskt.

## Android

Ange programkontexten för Android SDK i huvudaktiviteten.

```java
protected override void OnCreate (Bundle bundle) 
{
    ... 
    Config.SetContext (Application.Context); 
    ... 
}
```

Implementera livscykelanrop i varje aktivitet.

```java
protected override void OnResume()
{
    ...
    Config.CollectLifecycleData (this);
    ...
}
protected override void OnPause() 
{
    ...
    Config.PauseCollectingLifecycleData ();
    ...
}
```
