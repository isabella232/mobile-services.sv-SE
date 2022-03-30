---
description: 'Följande förvärvsmetoder finns i iOS-biblioteket '
solution: Experience Cloud Services,Analytics
title: Förvärvsmetoder
uuid: 6f88de57-793d-4d33-9a54-f6714289fd2c
exl-id: dd2721ae-b9a6-48b9-bc92-8e12ee551929
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 18%

---

# Anskaffningsmetoder {#acquisition-methods}

Följande förvärvsmetoder finns i iOS-biblioteket:

Följande metod stöds:

* **purchaseCampaignStartForApp:data:**

   Tillåter utvecklare att starta en app-anskaffningskampanj som om användaren hade klickat på en länk. Detta är praktiskt när du skapar länkar för manuell hämtning och hanterar omdirigering av appbutiken själv, till exempel med en `SKStoreView`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void)acquisitionCampaignStartForApp:(NSString *) appId data:(NSDictionary *)data; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile acquisitionCampaignStartForApp:@"0652024f-adcd-49f9-9bd7-2552a4564d2f" data:@{@"custom.key":@"value"}]; 
      ```
