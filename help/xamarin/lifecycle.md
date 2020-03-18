---
description: Information som hjälper dig att implementera livscykelvärden för Android. Livscykelstatistik samlas in automatiskt för iOS.
keywords: Xamarin
seo-description: Information som hjälper dig att implementera livscykelvärden för Android. Livscykelstatistik samlas in automatiskt för iOS.
seo-title: Implementera livscykel
solution: Marketing Cloud,Developer
title: Implementera livscykel
uuid: 6dccc12e-8b57-4231-9c74-d47bc0ac93ba
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Implementera livscykel {#implement-lifecycle}

Den här informationen hjälper dig att implementera livscykelvärden för Android.

>[!TIP]
>
>Livscykelstatistik samlas in automatiskt för iOS.

Information om mått och mått som kan mätas automatiskt av mobilbiblioteket efter att livscykeln har implementerats finns i [Livscykelstatistik](/help/ios/metrics.md).

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
