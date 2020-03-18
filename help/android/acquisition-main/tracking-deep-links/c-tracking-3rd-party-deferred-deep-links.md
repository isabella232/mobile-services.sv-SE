---
description: Använd Android SDK för att implementera spårning av fördröjda djuplänkar från tredje part.
seo-description: Använd Android SDK för att implementera spårning av fördröjda djuplänkar från tredje part.
seo-title: Spåra fördröjda djuplänkar från tredje part
title: Spåra fördröjda djuplänkar från tredje part
uuid: 4c798e47-7988-4a06-a191-6c4d05f6ee61
translation-type: tm+mt
source-git-commit: bf076aa8e59d5c3e634fc4ae21f0de0d4541a83f

---


# Spåra fördröjda länkar från tredje part{#tracking-third-party-deferred-deep-links}

Använd Android SDK för att implementera spårning av fördröjda djuplänkar från tredje part.

## Klassisk Adobe Mobile SDK-djuplänkning {#section_D114FA1EB9664EAA82E036A990694B26}

Adobe Mobile SDK har för närvarande stöd för djuplänkning där apputvecklaren förväntas använda `collectLifecycleData` SDK-API:t från den djupt länkade aktiviteten. SDK lägger till data för djuplänken från parametrar för djuplänkens URL-adress. Mer information om hur djuplänkning fungerar i Adobe Mobile SDK finns i [Spåra djuplänkar](/help/android/acquisition-main/tracking-deep-links/tracking-deep-links.md).

## Djuplänkning på Facebook {#section_6A9DACB54A2F4CDEBE9C744DEFADFDED}

En annonsskapare kan skapa en annons på Facebook som en länk. När användarna klickar på annonsen går den direkt till den information som de är intresserade av appen i. Den djupa länken är **inte** en fingerskrivars-URL. Under annonskonfigurationen finns det dock ett alternativ för att ange en webblänk-URL från tredje part. En apputvecklare som använder Adobe Mobile SDK:er och tjänster förväntas ange Adobe Mobile Service-konfigurerade URL:er för fingeravtrycksläsare i det här fältet. Om allt är korrekt konfigurerat skickar Facebook SDK den här URL:en till programmet när appen installeras eller startas.

## Konfigurera SDK:er {#section_834CD3109175432B8173ECB6EA7DE315}

Apputvecklaren utför följande uppgifter för att förbereda sig för att lägga till stöd för Facebook-djuplänkning med Adobe Mobile SDK:

* Kom igång med Android SDK

   Mer information finns i [Komma igång med Android SDK](https://developers.facebook.com/docs/android/getting-started) .

* Konfigurera djuplänkning

   Mer information finns i Konfigurera [djuplänkning](https://developers.facebook.com/docs/app-ads/deep-linking#os).

Om programmet är korrekt konfigurerat bör API:t göra det möjligt att samla in djuplänksinformation från Facebook-kampanjen och skicka den till Adobe Mobile Service. `trackAdobeDeepLink()` Om installationsträffen inte har skickats till Adobe Mobile Service vid första starten läggs den här informationen till i livscykelträffen. Annars skickas det som en Adobe-träff.

>[!TIP]
>
>Kontrollera att djuplänkens URL har en nyckel som heter `a.deeplink.id`. Om URL-adressen saknar parametern för djuplänk-ID läggs URL-parametrarna inte till i kontextdata.

Om länken kan tillskrivas ett förvärv lagrar Adobe Mobile SDK förvärvsuppgifterna från den djupa Facebook-länken som användes för att ringa `trackAdobeDeepLink()`. Dessa data kommer att vara tillgängliga för Adobe Mobile SDK i framtida starter. Om ett återanrop har registrerats används även Adobes återanrop för att skicka data tillbaka till klienten.

## Aktivera djuplänkning i ett Android-program {#section_64C15E269E89424B8E3D029F88094620}

1. Registrera programmet för att hantera djupa länkar.

   Mer information finns i [Tillåt andra program att starta aktiviteten](https://developer.android.com/training/basics/intents/filters.html).

1. Länka Facebooks SDK:er.

   Om du vill lägga till Facebook-övertoningsberoendet i appen följer du stegen i [Komma igång-Android SDK](https://developers.facebook.com/docs/android/getting-started).

1. Om du vill initiera Facebook SDK fyller du i instruktionerna i *installationsavsnittet* för Android Studio.
1. Ring `trackAdobeDeepLink()` från huvudaktiviteten.

   ```java
   @Override 
   protected void onResume() { 
      super.onResume(); 
      AppEventsLogger.activateApp(this); 
      /* 
       * Adobe Tracking - Config 
       * 
       * call collectLifecycleData() to begin collecting lifecycle data 
       * must be in the onResume() of every activity in your app 
       */ 
      Config.collectLifecycleData(this);
   
      AppLinkData.fetchDeferredAppLinkData(this, 
            new AppLinkData.CompletionHandler() { 
               @Override 
               public void onDeferredAppLinkDataFetched(AppLinkData appLinkData) { 
                  // Process app link data 
                  if (appLinkData != null) { 
                     Config.trackAdobeDeepLink(appLinkData.getTargetUri()); 
                  } 
               } 
            } 
      ); 
   }
   ```

