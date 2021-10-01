---
description: Lägen är de olika skärmarna eller vyerna i ditt program.
solution: Experience Cloud,Analytics
title: Spåra applägen
topic-fix: Developer and implementation
uuid: 69c99d05-5816-4c86-97c5-d218dc26c129
exl-id: ee1ea716-ee72-4c28-92cb-26df1327f5c6
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Spåra programtillstånd {#track-app-states}

Lägen är de olika skärmarna eller vyerna i ditt program.

Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, skickas ett `trackState`-anrop. I Android anropas vanligtvis `trackState` varje gång en ny aktivitet läses in.

## Spårningslägen {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. I funktionen `onCreate` anropar du `trackState` för att skicka en träff för den här tillståndsvyn:

   ```java
   @Override 
   public void onCreate(Bundle savedInstanceState) { 
       super.onCreate(savedInstanceState); 
       setContentView(R.layout.main); 
   
       // Adobe - track when this state loads 
       Analytics.trackState("State Name", null); 
   }
   ```

`"State Name"` rapporteras i variabeln `View State` i Adobe Mobile Services och en vy registreras för varje `trackState`-anrop. I andra analysgränssnitt rapporteras `View State` som `Page Name` och `state views` som `page views`.

## Skicka ytterligare data {#section_CFDB4F944496401786A145C209AB387C}

Förutom `"State Name"` kan du skicka ytterligare kontextdata med varje spårningsåtgärdsanrop:

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
| Adobe Mobile Services | Rapporten **[!UICONTROL View States]**. Den här rapporten baseras på de sökvägar som användarna tog genom ditt program. En exempelsökväg är **[!UICONTROL Home]** > **[!UICONTROL Settings]** > **[!UICONTROL Feed]**. |
| Adobe Analytics | Lägen kan visas var som helst där sidor kan visas, till exempel **[!UICONTROL Pages]**-rapporten, **[!UICONTROL Page Views]**-rapporten och **[!UICONTROL Path]**-rapporten. |
| Ad hoc-analys | Lägen kan visas var som helst Sidor kan visas med **[!UICONTROL Page]**-måtten **[!UICONTROL Page Views]**, **[!UICONTROL Path]**-rapporterna. |
