---
description: Den här informationen hjälper dig att använda meddelanden i appen i dina iOS-appar.
solution: Experience Cloud,Analytics
title: Meddelanden i appen
topic-fix: Developer and implementation
uuid: 21fa6a94-bb7f-4c78-843b-a50f1974db22
exl-id: 70b0ade4-dcd1-4e00-9800-352f11c4001d
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Meddelanden i appen {#in-app-messaging}

Den här informationen hjälper dig att använda meddelanden i appen i dina iOS-appar.

Om du vill använda meddelanden i programmet måste du **ha SDK version 4.2 eller senare.**

Lite information att komma ihåg:

* Meddelanden och regler som definierar när meddelanden visas skapas i Adobe Mobile-tjänster. Mer information finns i [Skapa ett meddelande i appen](/help/using/in-app-messaging/t-in-app-message/t-in-app-message.md).
* Uppdateringarna som beskrivs i det här avsnittet måste göras i SDK för att meddelanden i appen ska kunna visas.

   >[!TIP]
   >
   >Du kan slutföra de här stegen även om inga meddelanden har definierats. När du har definierat meddelanden levereras de dynamiskt till din app och visas utan någon uppdatering för appbutiken.

## Aktivera meddelanden i programmet {#section_79F984271C3B4366B7B04F864F4FF8C2}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i ditt projekt* i [Core Implementation och Lifecycle](/help/ios/getting-started/requirements.md).

1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Kontrollera att filen `ADBMobileConfig.json` innehåller de inställningar som krävs för meddelanden i appen.
1. För att meddelanden i programmet ska uppdateras dynamiskt vid start måste `remotes`-objektet finnas och vara korrekt konfigurerat:

   ```js
   "messages": [ 
       { 
           "messageId": "de45c43c-37bf-441f-8cbd-cc3ba3469ebe", 
           "template": "fullscreen", 
           "showOffline": false, 
           "showRule": "always", 
           "endDate": 2524730400, 
           "startDate": 0, 
           "audiences": [], 
           "triggers": [], 
           "payload": { // contents change depending on template 
               "html": "<html>html code goes here</html>" 
           }, 
       }, 
       … 
   ] 
   "remotes" : { 
       "analytics.poi": "https://assets.adobedtm.com/…/yourfile.json", 
       "messages": "https://assets.adobedtm.com/…/yourfile.json" 
   }
   ```

   >[!TIP]
   >
   >`messages` eller  `remotes` krävs.

   Om dessa objekt inte har konfigurerats hämtar du en uppdaterad `ADBMobileConfig.json`-fil från Adobe Mobile-tjänster. Mer information finns i [Core Implementation and Lifecycle](/help/ios/getting-started/requirements.md).

## Spåra meddelanden i appen {#section_B85CDF6929564AAEA79338B55E5CB1E8}

SDK:erna för iOS-mobiltjänster spårar följande mått för dina meddelanden i appen:

* För meddelanden i helskärmsläge och aviseringsformat i appen:

   * **[!UICONTROL Impressions]**: när användaren utlöser ett meddelande i appen.
   * **[!UICONTROL Click throughs]**: när användaren trycker på  **[!UICONTROL Click-through]** knappen.
   * **[!UICONTROL Cancels]**: när användaren trycker på  **[!UICONTROL Cancel]** knappen.

* För anpassade meddelanden i helskärmsläge i appen måste HTML-innehållet i meddelandet innehålla rätt kod för att meddela SDK-spårning om följande knappar:

   * **[!UICONTROL Click-through]** (omdirigering) exempelspårning:  `adbinapp://confirm/?url=https://www.yoursite.com`
   * **[!UICONTROL Cancel]** (close) exempelspårning:  `adbinapp://cancel`

* För lokala (fjärranslutna) meddelanden:

   * **[!UICONTROL Impressions]**: när användaren utlöser meddelandet.
   * **[!UICONTROL Opens]**: när användaren öppnar programmet från meddelandet.

   Här är ett exempel på hur du inkluderar öppen spårning:

   ```objective-c
   - (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
     // handle local notification click-throughs for iOS 10 and older 
     NSDictionary *localNotificationDictionary = launchOptions[UIApplicationLaunchOptionsLocalNotificationKey]; 
     if ([localNotificationDictionary isKindOfClass:[NSDictionary class]]) { 
          [ADBMobile trackLocalNotificationClickThrough:localNotificationDictionary]; 
     } 
   } 
   - (void) application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification { 
      [ADBMobile trackLocalNotificationClickThrough:notification.userInfo]; 
   }
   ```

## Lokal reservbild {#section_DEACC1CE549B4573B556A44A52409941}

När du skapar ett helskärmsmeddelande i Adobe Mobile-tjänster kan du välja att ange en reservbild. Om det inte går att hämta den avsedda bilden från webben försöker SDK att läsa in bilden med samma namn från programpaketet. På så sätt kan du visa meddelandet i sin ursprungliga form även om användaren är offline eller om den förinställda bilden inte är tillgänglig.

Resursnamnet för reservbild anges när meddelandet konfigureras i Adobe Mobile-tjänster.

>[!IMPORTANT]
>
>Du måste se till att den angivna resursen är tillgänglig.
