---
description: Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, ska ett spårlägesanrop skickas. I iOS spåras ett läge vanligtvis i metoden viewDidnLoad för varje vy.
seo-description: Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, ska ett spårlägesanrop skickas. I iOS spåras ett läge vanligtvis i metoden viewDidnLoad för varje vy.
seo-title: Spåra applägen
solution: Experience Cloud,Analytics
title: Spåra applägen
topic-fix: Developer and implementation
uuid: 12cca4eb-1f15-4cec-a58f-76b69eaff99d
exl-id: 1b7d2fbb-d2df-4063-b923-e59fa3582830
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 2%

---

# Spåra programtillstånd {#track-app-states}

Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, ska ett spårlägesanrop skickas. I iOS spåras ett läge vanligtvis i metoden viewDidnLoad för varje vy.

>[!TIP]
>
>Om du vill spåra lägen ringer du `trackState`. Lägen spåras inte automatiskt.

## Spårningslägen {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i ditt projekt* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Ring `trackState` för att skicka en träff för den här tillståndsvyn.

   ```objective-c
   [ADBMobile trackState:@"Login Screen"  
                    data:nil];
   ```

I Adobe Mobile-tjänster rapporteras **[!UICONTROL State Name]** i variabeln *`View State`* och en vy registreras för varje `trackState`-anrop. I andra analysgränssnitt rapporteras **[!UICONTROL View State]** som **[!UICONTROL Page Name]**, och lägesvyer rapporteras som sidvyer.

## Skicka ytterligare data {#section_CFDB4F944496401786A145C209AB387C}

Förutom **[!UICONTROL State Name]** kan du skicka ytterligare kontextdata med varje spårningsåtgärdsanrop:

```objective-c
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
[contextData setObject:@"logged in" forKey:@"myapp.login.LoginStatus"]; 
[ADBMobile trackState:@"Home Screen" data:contextData];
```

Kontextdatavärden måste mappas till anpassade variabler:

![](assets/map-variable-context-state.png)

## Appstatusrapportering {#section_0F6A54AB7A3F42C9BB042D86A0FC4630}

Lägen visas vanligtvis genom att använda en pausrapport så att du kan se hur användare navigerar i appen och vilka lägen som visas mest.

|  |  |
|--- |--- |
| Adobe Mobile Services | Rapporten **[!UICONTROL View States]**. Den här rapporten baseras på de sökvägar som användarna tog genom ditt program. En exempelsökväg är **[!UICONTROL Home]** > **[!UICONTROL Settings]** > **[!UICONTROL Feed]**. |
| Adobe Analytics | Lägen kan visas var som helst där sidor kan visas, till exempel **[!UICONTROL Pages]**-rapporten, **[!UICONTROL Page Views]**-rapporten och **[!UICONTROL Path]**-rapporten. |
| Ad hoc-analys | Lägen kan visas var som helst Sidor kan visas med **[!UICONTROL Page]**-måtten **[!UICONTROL Page Views]**, **[!UICONTROL Path]**-rapporterna. |
