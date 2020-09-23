---
description: 'Följande förvärvsmetoder tillhandahålls av iOS-biblioteket '
seo-description: 'Följande förvärvsmetoder tillhandahålls av iOS-biblioteket '
seo-title: Förvärvsmetoder
solution: Experience Cloud,Analytics
title: Förvärvsmetoder
uuid: 6f88de57-793d-4d33-9a54-f6714289fd2c
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 16%

---


# Anskaffningsmetoder {#acquisition-methods}

Följande förvärvsmetoder finns i iOS-biblioteket:

Följande metod stöds:

* **purchaseCampaignStartForApp:data:**

   Tillåter utvecklare att starta en app-anskaffningskampanj som om användaren hade klickat på en länk. Detta är användbart när du vill skapa länkar för manuell hämtning och hantera omdirigering av appbutiken själv, till exempel med en `SKStoreView`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void)acquisitionCampaignStartForApp:(NSString *) appId data:(NSDictionary *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile acquisitionCampaignStartForApp:@"0652024f-adcd-49f9-9bd7-2552a4564d2f" data:@{@"custom.key":@"value"}]; 
      ```


