---
description: Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.
solution: Experience Cloud Services,Analytics
title: Spåra programkrascher
topic-fix: Developer and implementation
uuid: 3ab98c14-ccdf-4060-ad88-ec07c1c6bf07
exl-id: d8d59b4e-0231-446d-9ba1-8a9809be9c61
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Spåra programkrascher {#track-app-crashes}

Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.

>[!TIP]
>
>Programkrascher spåras som en del av livscykelmätvärden. Lägg till biblioteket i projektet och implementera livscykeln innan du kan spåra krascher. Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

När livscykelvärden implementeras anropas `Config.collectLifecycleData` i `OnResume` metod för varje aktivitet. I `onPause` metod, ett anrop görs till `Config.pauseCollectingLifeCycleData`.

I `pauseCollectingLifeCycleData`, är en flagga inställd för att indikera en enkel avslutning. När appen startas igen eller återupptas `collectLifecycleData` kontrollerar den här flaggan. Om appen inte avslutas korrekt enligt flaggstatusen kan du `a.CrashEvent` kontextdata skickas med nästa anrop och en krasch rapporteras.

För att få korrekt kraschrapportering måste du ringa `pauseCollectingLifeCycleData` i `onPause` metod för varje aktivitet. Här följer en illustration av livscykeln för Android-aktiviteten:

![](assets/android-lifecycle.png)

Mer information om Android-aktivitetens livscykel finns i [Verksamhet](https://developer.android.com/guide/components/activities.html).

*Den här Android-livscykelbilden skapades och [delas av Android Open Source Project](https://source.android.com/) och används enligt villkoren i [Creative Commons 2.5 Attribution License](https://creativecommons.org/licenses/by/2.5/).*

## Vad kan orsaka en falsk krasch?

1. Om du felsöker via en utvecklingsmiljö, till exempel Android Studio, och startar programmet igen från utvecklingsmiljön när programmet är i förgrunden, kraschar programmet.

   >[!TIP]
   >
   >Du kan undvika den här kraschen genom att göra en bakomliggande bakgrund av appen innan du startar den från utvecklingsmiljön igen.

1. Om den sista förgrundsaktiviteten i din app är bakgrundsbelagd och inte anropas `Config.pauseCollectingLifecycleData();` in `onPause`, och din app stängs manuellt eller stoppas av operativsystemet, kommer nästa start att resultera i en krasch.

## Hur ska fragment hanteras?

Fragment har programlivscykelhändelser som liknar aktiviteter. Ett fragment kan dock inte vara aktivt utan att vara kopplat till en aktivitet.

>[!IMPORTANT]
>
>Du måste förlita dig på de livscykelhändelser som de innehållande aktiviteterna kan köra koden mot. Detta hanteras av fragmentets överordnade vy.

## (Valfritt) Implementera återanrop för aktivitetens livscykel

Från och med API-nivå 14 tillåter Android globala återanrop under livscykeln för aktiviteter. Mer information finns i [Program](https://developer.android.com/reference/android/app/Application).

Du kan använda dessa återanrop för att säkerställa att alla aktiviteter anropas korrekt `collectLifecycleData()` och `pauseCollectingLifecycleData()`. Du behöver bara lägga till den här koden i din huvudaktivitet och andra aktiviteter där din app kan startas:

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

Skicka ytterligare kontextdata med ditt livscykelanrop genom att använda `Config.collectLifecycleData(Activity activity`, `Map<String`, `Object> contextData)`måste du åsidosätta `onResume` metod för aktiviteten och se till att du anropar `super.onResume()` efter manuell anrop `collectLifecycleData`.

```js
@Override 
protected void onResume() { 
    HashMap<String, Object> cdata = new HashMap<>(); 
    cdata.put("someKey", "someValue"); 
    Config.collectLifecycleData(this, cdata); 
  
    super.onResume(); 
}
```
