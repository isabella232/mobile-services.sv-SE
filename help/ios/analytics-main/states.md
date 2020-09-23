---
description: Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, ska ett spårlägesanrop skickas. I iOS spåras ett läge vanligtvis i metoden viewDidnLoad för varje vy.
seo-description: Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, ska ett spårlägesanrop skickas. I iOS spåras ett läge vanligtvis i metoden viewDidnLoad för varje vy.
seo-title: Spåra applägen
solution: Experience Cloud,Analytics
title: Spåra applägen
topic: Developer and implementation
uuid: 12cca4eb-1f15-4cec-a58f-76b69eaff99d
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 2%

---


# Track app states {#track-app-states}

Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i programmet, till exempel när en användare navigerar från startsidan till nyhetsflödet, ska ett spårlägesanrop skickas. I iOS spåras ett läge vanligtvis i metoden viewDidnLoad för varje vy.

>[!TIP]
>
>Om du vill spåra lägen ringer du `trackState`. Lägen spåras inte automatiskt.

## Spårningslägen {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket.

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Anropa `trackState` att skicka en träff för den här statusvyn.

   ```objective-c
   [ADBMobile trackState:@"Login Screen"  
                    data:nil];
   ```

I Adobe Mobile-tjänster **[!UICONTROL State Name]** rapporteras variabeln i *`View State`* och en vy registreras för varje `trackState` anrop. I andra Analytics-gränssnitt **[!UICONTROL View State]** rapporteras som **[!UICONTROL Page Name]** och lägesvyer rapporteras som sidvyer.

## Skicka ytterligare data {#section_CFDB4F944496401786A145C209AB387C}

Förutom **[!UICONTROL State Name]** kan du skicka ytterligare kontextdata för varje spårningsåtgärd:

```objective-c
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 
[contextData setObject:@"logged in" forKey:@"myapp.login.LoginStatus"]; 
[ADBMobile trackState:@"Home Screen" data:contextData];
```

Kontextdatavärden måste mappas till anpassade variabler:

![](assets/map-variable-context-state.png)

## App-tillståndsrapportering {#section_0F6A54AB7A3F42C9BB042D86A0FC4630}

Lägen visas vanligtvis genom att använda en pausrapport så att du kan se hur användare navigerar i appen och vilka lägen som visas mest.

|  |  |
|--- |--- |
| Adobe Mobile Services | Rapporten **[!UICONTROL View States]** . Den här rapporten baseras på de sökvägar som användarna tog genom ditt program. En exempelbana är **[!UICONTROL Home]** > **[!UICONTROL Settings]** > **[!UICONTROL Feed]**. |
| Adobe Analytics | Lägen kan visas var som helst där sidor kan visas, till exempel **[!UICONTROL Pages]** rapporten, **[!UICONTROL Page Views]** rapporten och **[!UICONTROL Path]** rapporten. |
| Ad hoc-analys | Lägen kan visas var som helst Sidor kan visas med hjälp av **[!UICONTROL Page]** mått, **[!UICONTROL Page Views]** mått och **[!UICONTROL Path]** rapporter. |
