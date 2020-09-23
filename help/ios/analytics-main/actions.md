---
description: Åtgärder är de händelser som inträffar i programmet och som du vill mäta. Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan till exempel spåra en ny prenumeration varje gång en artikel visas eller varje gång en nivå är slutförd. Motsvarande mätvärden för dessa händelser konfigureras som prenumerationer, artiklar som läses och nivåer slutförda.
seo-description: Åtgärder är de händelser som inträffar i programmet och som du vill mäta. Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan till exempel spåra en ny prenumeration varje gång en artikel visas eller varje gång en nivå är slutförd. Motsvarande mätvärden för dessa händelser konfigureras som prenumerationer, artiklar som läses och nivåer slutförda.
seo-title: Spåra appåtgärder
solution: Experience Cloud,Analytics
title: Spåra appåtgärder
topic: Developer and implementation
uuid: 62017be1-5395-4d16-bde3-4c40a2c012d4
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---


# Track app actions {#track-app-actions}

Åtgärder är de händelser som inträffar i programmet och som du vill mäta. Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan till exempel spåra en ny prenumeration varje gång en artikel visas eller varje gång en nivå är slutförd. Motsvarande mätvärden för dessa händelser konfigureras som prenumerationer, artiklar som läses och nivåer slutförda.

Åtgärder spåras inte automatiskt, så för att spåra en händelse måste du ringa `trackAction`.

## Spåra åtgärder {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. När den åtgärd som du vill spåra inträffar i appen ska du ringa `trackAction` för att skicka en träff för den här åtgärden.

   ```objective-c
   [ADBMobile trackAction:@"myapp.ActionName"  
                     data:nil];
   ```

   >[!TIP]
   >
   >Om koden där du lägger till det här anropet kan köras medan programmet är i bakgrunden, ska du ringa `trackActionFromBackground` i stället för `trackAction`.

1. I användargränssnittet för Adobe-mobiltjänster väljer du din app och klickar på **[!UICONTROL Manage App Settings]**.

1. Klicka på **[!UICONTROL Manage Variables and Metrics]** och klicka på **[!UICONTROL Custom Metrics]** fliken.

1. Mappa kontextdatanamnet som definieras i koden, till exempel `a.action=myapp.ActionName`, till en anpassad händelse.

   ![](assets/map-event-context-data.png)

Du kan också ange att en prop ska innehålla alla åtgärdsvärden genom att mappa en anpassad prop med ett namn som **[!UICONTROL Custom Actions]** och ange värdet som `a.action`.

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

Om du spårar en åtgärd i koden som kan köras när programmet är i bakgrunden, ska du ringa `trackActionFromBackground` i stället för `trackAction`. Även om `trackActionFromBackground` innehåller ytterligare logik för att förhindra att livscykelanrop utlöses när de inte gör det, är parametrarna desamma.

## Åtgärdsrapportering {#section_0F6A54AB7A3F42C9BB042D86A0FC4630}

| Gränssnitt | Rapport |
|--- |--- |
| Adobe Mobile Services | **[!UICONTROL Action Paths]** rapport. Visa den ordning i vilken åtgärder utförs i appen. Du kan också klicka **[!UICONTROL Customize]** på en rapport om du vill visa åtgärder som rangordnats, trendats eller i en detaljrapport, eller använda ett filter om du vill visa åtgärder för ett visst segment. |
| Marketing reports and analytics | **[!UICONTROL Custom Event]** rapport.  När en åtgärd har mappats till en anpassad händelse kan du visa mobilhändelser som liknar alla andra Analytics-händelser. |
| Ad hoc-analys | **[!UICONTROL Custom Event]** rapport. När en åtgärd har mappats till en anpassad händelse kan du visa mobilhändelser som liknar alla andra Analytics-händelser. |