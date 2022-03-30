---
description: Åtgärder är de händelser som inträffar i programmet och som du vill mäta. Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan till exempel spåra en ny prenumeration varje gång en artikel visas eller varje gång en nivå är slutförd. Motsvarande mätvärden för dessa händelser konfigureras som prenumerationer, artiklar som läses och nivåer slutförda.
solution: Experience Cloud Services,Analytics
title: Spåra appåtgärder
topic-fix: Developer and implementation
uuid: 62017be1-5395-4d16-bde3-4c40a2c012d4
exl-id: ff317eff-1b8e-46e1-a305-a404979447cb
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Spåra appåtgärder {#track-app-actions}

Åtgärder är de händelser som inträffar i programmet och som du vill mäta. Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan till exempel spåra en ny prenumeration varje gång en artikel visas eller varje gång en nivå är slutförd. Motsvarande mätvärden för dessa händelser konfigureras som prenumerationer, artiklar som läses och nivåer slutförda.

Åtgärder spåras inte automatiskt, så för att spåra en händelse måste du anropa `trackAction`.

## Spåra åtgärder {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i projektet* in [Kärnimplementering och livscykel](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. När den åtgärd du vill spåra inträffar i appen ringer du `trackAction` för att skicka en träff för den här åtgärden.

   ```objective-c
   [ADBMobile trackAction:@"myapp.ActionName"  
                     data:nil];
   ```

   >[!TIP]
   >
   >Om koden där du lägger till det här anropet kan köras när programmet är i bakgrunden, ska du ringa `trackActionFromBackground` i stället för `trackAction`.

1. I användargränssnittet för Mobile-tjänster i Adobe väljer du din app och klickar på **[!UICONTROL Manage App Settings]**.

1. Klicka **[!UICONTROL Manage Variables and Metrics]** och klicka på **[!UICONTROL Custom Metrics]** -fliken.

1. Mappa till exempel kontextdatanamnet som definieras i koden `a.action=myapp.ActionName`, till en anpassad händelse.

   ![](assets/map-event-context-data.png)

Du kan också ange att en propp ska innehålla alla åtgärdsvärden genom att mappa en anpassad propp med ett namn som **[!UICONTROL Custom Actions]** och ange värdet till `a.action`.

![](assets/map-custom-prop.png)

## Skicka ytterligare data {#section_3EBE813E54A24F6FB669B2478B5661F9}

Förutom åtgärdsnamnet kan du skicka ytterligare kontextdata med varje spårningsåtgärdsanrop:

```objective-c
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
[contextData setObject:@"Twitter" forKey:@"myapp.social.SocialSource"]; 
[ADBMobile trackAction:@"myapp.SocialShare" data:contextData];
```

Kontextdatavärden måste mappas till anpassade variabler:

![](assets/map-variable-context-action.png)

## Spåra bakgrundsåtgärder {#section_AC13013F207D4FBAAF27E4412034251E}

Om du spårar en åtgärd i koden som kan köras när programmet är i bakgrunden, anropar du `trackActionFromBackground` i stället för `trackAction`. Fast `trackActionFromBackground` innehåller ytterligare logik för att förhindra att livscykelanrop utlöses när de inte gör det, parametrarna är desamma.

## Åtgärdsrapportering {#section_0F6A54AB7A3F42C9BB042D86A0FC4630}

| Gränssnitt | Rapport |
|--- |--- |
| Adobe Mobile Services | **[!UICONTROL Action Paths]** rapport. Visa den ordning i vilken åtgärder utförs i appen. Du kan också klicka **[!UICONTROL Customize]** på en rapport om du vill visa åtgärder som rangordnats, trendats eller i en detaljrapport eller använda ett filter för att visa åtgärder för ett visst segment. |
| Marketing reports and analytics | **[!UICONTROL Custom Event]** rapport.  När en åtgärd har mappats till en anpassad händelse kan du visa mobilhändelser som liknar alla andra Analytics-händelser. |
| Ad hoc-analys | **[!UICONTROL Custom Event]** rapport. När en åtgärd har mappats till en anpassad händelse kan du visa mobilhändelser som liknar alla andra Analytics-händelser. |
