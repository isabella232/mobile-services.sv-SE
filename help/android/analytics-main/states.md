---
description: Lägen är de olika skärmarna eller vyerna i ditt program.
solution: Experience Cloud Services,Analytics
title: Spåra applägen
topic-fix: Developer and implementation
uuid: 69c99d05-5816-4c86-97c5-d218dc26c129
exl-id: ee1ea716-ee72-4c28-92cb-26df1327f5c6
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Spåra programtillstånd {#track-app-states}

Lägen är de olika skärmarna eller vyerna i ditt program.

Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, visas en `trackState` samtal skickas. I Android `trackState` anropas vanligtvis varje gång en ny aktivitet läses in.

## Spårningslägen {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. I `onCreate` funktion, anrop `trackState` om du vill skicka en träff för den här vyn:

   ```java
   @Override 
   public void onCreate(Bundle savedInstanceState) { 
       super.onCreate(savedInstanceState); 
       setContentView(R.layout.main); 
   
       // Adobe - track when this state loads 
       Analytics.trackState("State Name", null); 
   }
   ```

The `"State Name"` rapporteras i `View State` variabel i Adobe Mobile och en vy registreras för varje `trackState` ring. I andra analysgränssnitt `View State` rapporteras som `Page Name`och `state views` rapporteras som `page views`.

## Skicka ytterligare data {#section_CFDB4F944496401786A145C209AB387C}

Förutom `"State Name"`kan du skicka ytterligare kontextdata för varje spårningsåtgärd:

```java
@Override 
public void onCreate(Bundle savedInstanceState) { 
    super.onCreate(savedInstanceState); 
    setContentView(R.layout.main); 
  
    // Adobe - track when this state loads 
    HashMap<String, Object> exampleContextData = new HashMap<String, Object>(); 
    exampleContextData.put("myapp.login.LoginStatus", "logged in"); 
    Analytics.trackState("Home Screen", exampleContextData); 
}
```

Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile-tjänster:

![](assets/map-variable-context-state.png)

## App-tillståndsrapportering {#section_0F6A54AB7A3F42C9BB042D86A0FC4630}

Lägen visas vanligtvis med hjälp av en målningsrapport, som gör att du kan se hur användare navigerar i din app och vilka lägen som visas oftast.

|  |  |
|--- |--- |
| Adobe Mobile Services | The **[!UICONTROL View States]** rapport. Den här rapporten baseras på de sökvägar som användarna tog genom ditt program. En exempelbana är  **[!UICONTROL Home]**  >  **[!UICONTROL Settings]**  > **[!UICONTROL Feed]**. |
| Adobe Analytics | Lägen kan visas var som helst där sidor kan visas, t.ex. **[!UICONTROL Pages]** rapporten, **[!UICONTROL Page Views]** och **[!UICONTROL Path]** rapport. |
| Ad hoc-analys | Lägen kan visas var som helst Sidor kan visas med **[!UICONTROL Page]** dimension, **[!UICONTROL Page Views]** Mätvärden. **[!UICONTROL Path]** rapporter. |
