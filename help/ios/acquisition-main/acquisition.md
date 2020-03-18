---
description: Förvärvningslänkar med unika spårningskoder kan genereras i Adobes mobiltjänster. När en användare hämtar och kör en app från Apple App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar förvärvsdata till Adobe Mobile Services.
seo-description: Förvärvningslänkar med unika spårningskoder kan genereras i Adobes mobiltjänster. När en användare hämtar och kör en app från Apple App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar förvärvsdata till Adobe Mobile Services.
seo-title: Förvärva mobilappar
solution: Marketing Cloud,Analytics
title: Förvärva mobilappar
topic: Developer and implementation
uuid: 5fece619-e4b8-4d06-9250-dcb66fa32ce0
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Förvärva mobilappar {#mobile-app-acquisition}

Förvärvningslänkar med unika spårningskoder kan genereras i Adobes mobiltjänster. När en användare hämtar och kör en app från Apple App Store efter att ha klickat på den genererade länken, samlar SDK automatiskt in och skickar förvärvsdata till Adobe Mobile Services.

Om du vill använda förvärvet **måste** du ha SDK version 4.1 eller senare.

Förvärvningslänkar måste skapas i Adobes mobiltjänster. Mer information finns i [Anskaffning](/help/using/acquisition-main/acquisition-main.md).

Med informationen i det här avsnittet kan SDK skicka förvärvsdata från en länk.

## Spåra förvärv av mobilappar {#section_CEA30C652AC8470784B8054E299B80FA}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Kontrollera att `ADBMobileConfig.json` filen innehåller de hämtningsinställningar som krävs:

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

   Inställningarna `acquisition` genereras av Adobe Mobile Services och bör inte ändras. Mer information om hur du hämtar en anpassad `ADBMobileConfig.json` fil med förkonfigurerade `acquisition` inställningar finns i [Innan du börjar](/help/ios/getting-started/requirements.md).

När de här inställningarna har aktiverats skickas inhämtningsdata automatiskt med det första livscykelanropet efter att appen startades första gången.

>[!CAUTION]
>
>`referrerTimeout` måste anges till ett högre värde än 0 för att appinhämtning ska kunna aktiveras.

## Aktivera din iOS-app för universella länkar

Om du använder universallänkar i din app lägger du till domänen Adobe Marketing Links i listan Associated Domains för din app.

I Xcode lägger du till din Adobe Marketing Länks-domän i listan Associerade domäner:

1. Gå till projektmålet och klicka på **[!UICONTROL Capabilities]** fliken.
2. Bläddra ned till **[!UICONTROL Associated Domains]** avsnittet och aktivera det.
3. Lägg till en post i **[!UICONTROL Domains]** listan för din Marketing Links-domän från din Marketing Links URL.

Ditt tävlingsbidrag kommer att se ut ungefär som `applinks:5848561889a02a6996aea62b.c00.adobe.com`.