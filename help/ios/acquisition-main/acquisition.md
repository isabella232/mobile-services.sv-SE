---
description: Förvärvningslänkar med unika spårningskoder kan genereras i Adobe Mobile-tjänster. När en användare hämtar och kör en app från Apple App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar hämtningsdata till Adobe Mobile-tjänster.
solution: Experience Cloud Services,Analytics
title: Mobile appförvärv
topic-fix: Developer and implementation
uuid: 5fece619-e4b8-4d06-9250-dcb66fa32ce0
exl-id: a90dcb2f-babb-4c97-b67a-8468925ee5c8
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Mobile appförvärv {#mobile-app-acquisition}

Förvärvningslänkar med unika spårningskoder kan genereras i Adobe Mobile-tjänster. När en användare hämtar och kör en app från Apple App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar hämtningsdata till Adobe Mobile-tjänster.

Om du vill använda förvärvet **måste** har SDK version 4.1 eller senare.

Förvärvningslänkar måste skapas i Adobe Mobile-tjänster. Mer information finns i [Förvärv](/help/using/acquisition-main/acquisition-main.md).

Med informationen i det här avsnittet kan SDK skicka förvärvsdata från en länk.

## Spåra förvärv av mobilappar {#section_CEA30C652AC8470784B8054E299B80FA}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i projektet* in [Kärnimplementering och livscykel](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Verifiera att `ADBMobileConfig.json` filen innehåller de hämtningsinställningar som krävs:

   ```xml
   "acquisition": { 
      "server": "c00.adobe.com", 
      "appid": "0652024f-adcd-49f9-9bd7-2552a4565d2f" 
   }, 
   "analytics": { 
     "referrerTimeout": 5, 
     ...
   ```

   >[!IMPORTANT]
   >
   >Om du skickar data till flera rapportsviter använder du hämtningsinställningarna (hämtningsserver och appid) från appen som är associerad med den första rapportsviten i din lista över rapportsvits-ID:n.

   The `acquisition` inställningarna genereras av Adobe Mobile-tjänster och bör inte ändras. Mer information om hur du hämtar en anpassad `ADBMobileConfig.json` filen med `acquisition` förkonfigurerade inställningar, se [Innan du börjar](/help/ios/getting-started/requirements.md).

När de här inställningarna har aktiverats skickas inhämtningsdata automatiskt med det första livscykelanropet efter att appen startades första gången.

>[!CAUTION]
>
>`referrerTimeout` måste anges till ett högre värde än 0 för att appinhämtning ska kunna aktiveras.

## Aktivera din iOS-app för universallänkar

Om du använder universallänkar i din app lägger du till domänen Adobe Marketing Links i listan Associated Domains för din app.

I Xcode lägger du till domänen Adobe Marketing Links i listan Associated Domains:

1. Gå till ditt projektmål och klicka på **[!UICONTROL Capabilities]** -fliken.
2. Bläddra nedåt till **[!UICONTROL Associated Domains]** och aktivera det.
3. Lägg till en post i **[!UICONTROL Domains]** lista för din Marketing Links-domän från din Marketing Links URL.

Ditt tävlingsbidrag ser ut ungefär som  `applinks:5848561889a02a6996aea62b.c00.adobe.com`.
