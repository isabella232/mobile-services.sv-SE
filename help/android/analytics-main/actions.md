---
description: Åtgärder är de händelser som inträffar i Android-appen och som du vill mäta.
solution: Experience Cloud Services,Analytics
title: Spåra appåtgärder
topic-fix: Developer and implementation
uuid: fe01c1df-f6bb-4b32-b3ef-959d2c724af6
exl-id: 495a6aa8-781d-4499-ad46-e19d57cccf40
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# Spåra appåtgärder {#track-app-actions}

Åtgärder är de händelser som inträffar i Android-appen och som du vill mäta.

Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan till exempel skicka en `trackAction` ring för varje ny prenumeration, varje gång en artikel visas eller varje gång en nivå har slutförts. Åtgärderna spåras inte automatiskt, så du måste ringa `trackAction` när en händelse som du vill spåra inträffar och mappa åtgärden till en anpassad händelse.

## Spåra åtgärder {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. När den åtgärd du vill spåra inträffar i appen ringer du `trackAction` om du vill skicka en träff för den här åtgärden:

   ```java
   Analytics.trackAction("myapp.ActionName", null);
   ```

1. I användargränssnittet för Mobile Services i Adobe väljer du din app och klickar på **[!UICONTROL Manage App Settings]**.
1. Klicka **[!UICONTROL Manage Variables and Metrics]** och klicka på **[!UICONTROL Custom Metrics]** -fliken.

1. Mappa till exempel kontextdatanamnet som definieras i koden `myapp.ActionName`, till en anpassad händelse.

   ![](assets/map-event-context-data.png)

Du kan också ange att en propp ska innehålla alla åtgärdsvärden genom att mappa en anpassad propp med ett namn som **[!UICONTROL Custom Actions]** och ange värdet till `a.action`.

![](assets/map-custom-prop.png)

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom åtgärdsnamnet kan du skicka ytterligare kontextdata med varje spårningsåtgärdsanrop:

```java
HashMap<String, Object> exampleContextData = new HashMap<String, Object>(); 
exampleContextData.put("myapp.social.SocialSource", "Twitter"); 
Analytics.trackAction("myapp.SocialShare", exampleContextData);
```

Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile-tjänster:

![](assets/map-variable-context-action.png)

## Åtgärdsrapportering {#section_0F6A54AB7A3F42C9BB042D86A0FC4630}

| Gränssnitt | Rapport |
|--- |--- |
| Adobe Mobile Services | **[!UICONTROL Action Paths]** rapport.  Visa den ordning i vilken åtgärder utförs i appen. Du kan också klicka **[!UICONTROL Customize]**  på en rapport om du vill visa åtgärder som rangordnats, trendats eller i en detaljrapport eller använda ett filter för att visa åtgärder för ett visst segment. |
| Marknadsföringsrapporter och analyser | **[!UICONTROL Custom Event]** rapport.  När en åtgärd har mappats till en anpassad händelse kan du visa mobilhändelser som liknar alla andra Analytics-händelser. |
| Ad hoc-analys | **[!UICONTROL Custom Event]** rapport.  När en åtgärd har mappats till en anpassad händelse kan du visa mobilhändelser som liknar alla andra Analytics-händelser. |
