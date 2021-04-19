---
description: Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.
seo-description: Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.
seo-title: Spåra programkrascher
solution: Experience Cloud,Analytics
title: Spåra programkrascher
topic-fix: Developer and implementation
uuid: 3ab98c14-ccdf-4060-ad88-ec07c1c6bf07
exl-id: d8d59b4e-0231-446d-9ba1-8a9809be9c61
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Spåra programkrascher {#track-app-crashes}

Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.

>[!TIP]
>
>Programkrascher spåras som en del av livscykelmätvärden. Lägg till biblioteket i projektet och implementera livscykeln innan du kan spåra krascher. Mer information finns i *Lägg till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

När livscykelvärden implementeras anropas `Config.collectLifecycleData` i `OnResume`-metoden för varje aktivitet. I metoden `onPause` anropas `Config.pauseCollectingLifeCycleData`.

I `pauseCollectingLifeCycleData` är en flagga inställd på att ange en enkel avslutning. När appen startas igen eller återupptas kontrollerar `collectLifecycleData` den här flaggan. Om appen inte avslutas korrekt enligt flaggstatusen skickas en `a.CrashEvent`-kontextdata med nästa anrop och en kraschhändelse rapporteras.

För att få korrekt kraschrapportering måste du anropa `pauseCollectingLifeCycleData` i `onPause`-metoden för varje aktivitet. Här följer en illustration av livscykeln för Android-aktiviteten:

![](assets/android-lifecycle.png)

Mer information om Android-aktivitetens livscykel finns i [Aktiviteter](https://developer.android.com/guide/components/activities.html).

*Den här Android-livscykelbilden skapades och  [delades av Android Open Source ](https://source.android.com/) Project och används enligt villkoren i  [Creative Commons 2.5 Attribution License](https://creativecommons.org/licenses/by/2.5/).*

## Vad kan orsaka en falsk krasch?

1. Om du felsöker via en utvecklingsmiljö, till exempel Android Studio, och startar programmet igen från utvecklingsmiljön när programmet är i förgrunden, kraschar programmet.

   >[!TIP]
   >
   >Du kan undvika den här kraschen genom att göra en bakomliggande bakgrund av appen innan du startar den från utvecklingsmiljön igen.

1. Om den senaste förgrundsaktiviteten i din app är bakgrunden och inte anropar `Config.pauseCollectingLifecycleData();` i `onPause`, och din app stängs manuellt eller dödas av operativsystemet, kommer nästa start att resultera i en krasch.

## Hur ska fragment hanteras?

Fragment har programlivscykelhändelser som liknar aktiviteter. Ett fragment kan dock inte vara aktivt utan att vara kopplat till en aktivitet.

>[!IMPORTANT]
>
>Du måste förlita dig på de livscykelhändelser som de innehållande aktiviteterna kan köra koden mot. Detta hanteras av fragmentets överordnade vy.

## (Valfritt) Implementera återanrop för aktivitetens livscykel

Från och med API-nivå 14 tillåter Android globala återanrop under livscykeln för aktiviteter. Mer information finns i [Program](https://developer.android.com/reference/android/app/Application).

Du kan använda dessa återanrop för att säkerställa att alla aktiviteter anropar `collectLifecycleData()` och `pauseCollectingLifecycleData()`. Du behöver bara lägga till den här koden i din huvudaktivitet och andra aktiviteter där din app kan startas:

```js
import com.adobe.mobile.Config; 
  
public class MainActivity extends Activity { 
... 
    @Override 
    protected void onCreate(Bundle savedInstanceState) { 
        super.onCreate(savedInstanceState); 
        setContentView(R.layout.activity_main); 
  
        getApplication().registerActivityLifecycleCallbacks(new Application.ActivityLifecycleCallbacks() { 
            @Override 
            public void onActivityResumed(Activity activity) { 
                Config.setContext(activity.getApplicationContext()); 
                Config.collectLifecycleData(activity); 
            } 
  
            @Override 
            public void onActivityPaused(Activity activity) {     
                Config.pauseCollectingLifecycleData(); 
            } 
    
            // the following methods aren't needed for our lifecycle purposes, but are required to be implemented 
            // by the ActivityLifecycleCallbacks object 
            @Override 
            public void onActivityCreated(Activity activity, Bundle savedInstanceState) {} 
            @Override 
            public void onActivityStarted(Activity activity) {} 
            @Override 
            public void onActivityStopped(Activity activity) {} 
            @Override 
            public void onActivitySaveInstanceState(Activity activity, Bundle outState) {} 
            @Override 
            public void onActivityDestroyed(Activity activity) {} 
        }); 
    } 
... 
}
```

Om du vill skicka ytterligare kontextdata med ditt livscykelanrop genom att använda `Config.collectLifecycleData(Activity activity`, `Map<String`, `Object> contextData)`, måste du åsidosätta `onResume`-metoden för den aktiviteten och se till att du anropar `super.onResume()` manuellt efter att du har anropat `collectLifecycleData`.

```js
@Override 
protected void onResume() { 
    HashMap<String, Object> cdata = new HashMap<>(); 
    cdata.put("someKey", "someValue"); 
    Config.collectLifecycleData(this, cdata); 
  
    super.onResume(); 
}
```
