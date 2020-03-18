---
description: Den här informationen hjälper dig att använda meddelanden i appen i dina iOS-appar.
seo-description: Den här informationen hjälper dig att använda meddelanden i appen i dina iOS-appar.
seo-title: Meddelanden i appen
solution: Marketing Cloud,Analytics
title: Meddelanden i appen
topic: Developer and implementation
uuid: 21fa6a94-bb7f-4c78-843b-a50f1974db22
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Meddelanden i appen {#in-app-messaging}

Den här informationen hjälper dig att använda meddelanden i appen i dina iOS-appar.

Om du vill använda meddelanden i programmet **måste** du ha SDK version 4.2 eller senare.

Lite information att komma ihåg:

* Meddelanden och regler som definierar när meddelanden visas skapas i Adobe Mobile-tjänster. Mer information finns i [Skapa ett meddelande](/help/using/in-app-messaging/t-in-app-message/t-in-app-message.md)i appen.
* Uppdateringarna som beskrivs i det här avsnittet måste göras i SDK för att meddelanden i appen ska kunna visas.

   >[!TIP]
   >
   >Du kan slutföra de här stegen även om inga meddelanden har definierats. När du har definierat meddelanden levereras de dynamiskt till din app och visas utan någon uppdatering för appbutiken.

## Aktivera meddelanden i programmet {#section_79F984271C3B4366B7B04F864F4FF8C2}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägga till SDK- och konfigurationsfilen i projektet* i [Core Implementation och Lifecycle](/help/ios/getting-started/requirements.md).

1. Importera biblioteket:

   ```objective-c
   #import "ADBMobile.h"
   ```

1. Kontrollera att `ADBMobileConfig.json` filen innehåller de inställningar som krävs för meddelanden i appen.
1. För att meddelanden i appen ska uppdateras dynamiskt vid start måste objektet vara `remotes` närvarande och korrekt konfigurerat:

   ```js
   “messages”: [ 
       { 
           “messageId”: “de45c43c-37bf-441f-8cbd-cc3ba3469ebe”, 
           “template”: “fullscreen”, 
           “showOffline”: false, 
           “showRule”: “always”, 
           “endDate”: 2524730400, 
           “startDate”: 0, 
           “audiences”: [], 
           “triggers”: [], 
           “payload”: { // contents change depending on template 
               “html”: “<html>html code goes here</html>” 
           }, 
       }, 
       … 
   ] 
   “remotes” : { 
       “analytics.poi”: “https://assets.adobedtm.com/…/yourfile.json”, 
       “messages”: “https://assets.adobedtm.com/…/yourfile.json” 
   }
   ```

   >[!TIP]
   >
   >`messages` eller `remotes` krävs.

   Om dessa objekt inte är konfigurerade hämtar du en uppdaterad `ADBMobileConfig.json` fil från Adobe Mobile Services. Mer information finns i [Core Implementation och Lifecycle](/help/ios/getting-started/requirements.md).

## Spåra meddelanden i appen {#section_B85CDF6929564AAEA79338B55E5CB1E8}

SDK:erna för iOS-mobiltjänster spårar följande mått för dina meddelanden i appen:

* För meddelanden i helskärmsläge och aviseringsformat i appen:

   * **[!UICONTROL Impressions]**: när användaren utlöser ett meddelande i appen.
   * **[!UICONTROL Click throughs]**: när användaren trycker på **[!UICONTROL Click-through]** knappen.
   * **[!UICONTROL Cancels]**: när användaren trycker på **[!UICONTROL Cancel]** knappen.

* För anpassade meddelanden i helskärmsläge i appen måste HTML-innehållet i meddelandet innehålla rätt kod för att meddela SDK-spårning om följande knappar:

   * **[!UICONTROL Click-through]** (omdirigering) exempelspårning: `adbinapp://confirm/?url=https://www.yoursite.com`
   * **[!UICONTROL Cancel]** (close) exempelspårning: `adbinapp://cancel`

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

När du skapar ett helskärmsmeddelande i Adobe Mobile Services kan du välja att ange en reservbild. Om det inte går att hämta den avsedda bilden från webben försöker SDK att läsa in bilden med samma namn från programpaketet. På så sätt kan du visa meddelandet i sin ursprungliga form även om användaren är offline eller om den förinställda bilden inte är tillgänglig.

Resursnamnet för reservbilden anges när meddelandet konfigureras i Adobe Mobile Services.

>[!IMPORTANT]
>
>Du måste se till att den angivna resursen är tillgänglig.

