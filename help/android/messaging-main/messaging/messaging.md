---
description: Ni kan leverera meddelanden i appen som triggas av alla analysdata eller händelser. Efter implementeringen levereras meddelanden dynamiskt till programmet och kräver ingen koduppdatering.
solution: Experience Cloud Services,Analytics
title: Meddelanden i appen
topic-fix: Developer and implementation
uuid: 351ee3d2-80b9-4f2d-9696-21f274d89f5a
exl-id: ca9414d1-86e6-4bb2-a2d6-57df37df2403
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 3%

---

# Meddelanden i appen {#in-app-messaging}

Ni kan leverera meddelanden i appen som triggas av alla analysdata eller händelser. Efter implementeringen levereras meddelanden dynamiskt till programmet och kräver ingen koduppdatering.

## Ny Adobe Experience Cloud SDK-version

Letar du efter information och dokumentation om Adobe Experience Platform Mobile SDK? Klicka [här](https://aep-sdks.gitbook.io/docs/) för vår senaste dokumentation.

>[!IMPORTANT]
>
>Från om med september 2018 har vi släppt en ny större version av SDK. Dessa nya Adobe Experience Platform Mobile SDK kan konfigureras via [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* För att komma igång, gå till [Starta](https://launch.adobe.com/).
* Om du vill se vad som finns i Experience Platform SDK-databaserna går du till [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
> Om du använder Adobe Experience Platform Mobile SDK:er med Adobe Launch ska du **måste** installera även Adobe Analytics Mobile Services-tillägget om du vill använda Adobe Mobile Services-funktioner som meddelanden i appen och push-meddelanden. Mer information finns i [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services). Mer information om hur du använder push-meddelanden och meddelanden i appen med SDK:n för Experience Cloud finns i [Konfigurera push-meddelanden](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-push-messaging) och [Konfigurera meddelanden i appen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-in-app-messaging).

>[!IMPORTANT]
>
>Om du vill använda meddelanden i appen **måste** har SDK version 4.2 eller senare.

Du kan skapa meddelanden och regler i Adobe Mobile-tjänster som definierar när meddelanden ska visas. Mer information finns i [Skapa ett meddelande i appen](/help/using/in-app-messaging/t-in-app-message/t-in-app-message.md). Om du vill visa meddelanden i programmet måste SDK uppdateras. Du kan slutföra de här stegen även om du ännu inte har definierat några meddelanden. När du har definierat meddelanden levereras de dynamiskt till din app och visas utan någon uppdatering för appbutiken.

## Aktivera meddelanden i programmet {#section_380DF56C4EE4432A823940E4AE4C9E91}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och Config-filen i IntelliJ IDEA- eller Eclipse-projektet* in [Kärnimplementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Uppdatera `AndroidManifest.xml` för att deklarera helskärmsaktiviteten och aktivera meddelandehanteraren:

   ```java
   <activity  
   android:name="com.adobe.mobile.MessageFullScreenActivity"  
   android:theme="@android:style/Theme.Translucent.NoTitleBar" /> 
   <receiver android:name="com.adobe.mobile.MessageNotificationHandler" />
   ```

   Om du har valt en modal layout väljer du ett av följande teman för meddelandet:

   * `Theme.Translucent.NoTitleBar.Fullscreen`
   * `Theme.Translucent.NoTitleBar`
   * `Theme.Translucent`

   Exempel:

   ```java
   <activity 
   android:name="com.adobe.mobile.MessageFullScreenActivity" 
   android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen" 
   android:windowSoftInputMode="adjustUnspecified|stateHidden" /> 
   <receiver android:name="com.adobe.mobile.MessageNotificationHandler" />
   ```

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. I varje `collectLifecycleData` anrop, skicka `this` för att ge en referens till din aktuella aktivitet:

   ```java
   @Override 
   public void onResume() { 
       Config.collectLifecycleData(this); 
   }
   ```

1. Verifiera att `ADBMobileConfig.json` filen innehåller de inställningar som krävs för meddelanden i appen.

   >[!IMPORTANT]
   >
   >`messages` eller `remotes` krävs.

   För att meddelanden i appen ska uppdateras dynamiskt vid start finns `remotes` objektet måste finnas och vara korrekt konfigurerat:

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

   Om det här objektet inte har konfigurerats hämtar du en uppdaterad `ADBMobileConfig.json` fil från Adobe Mobile-tjänster. Mer information finns i [Innan du börjar](/help/android/getting-started/requirements.md).

## Spåra meddelanden i appen {#section_B85CDF6929564AAEA79338B55E5CB1E8}

Android Mobile SDK:er håller reda på följande mått för dina meddelanden i appen:

* För meddelanden i helskärmsläge och aviseringsformat i appen:

   * **Impressions**: när användaren utlöser ett meddelande i appen.
   * **Klicka igenom**: när användaren trycker **[!UICONTROL Click through]**.
   * **Avbryter**: när användaren trycker **[!UICONTROL Cancel]**.

* För anpassade meddelanden i helskärmsläge i appen måste HTML-innehållet i meddelandet innehålla rätt kod för att meddela SDK-spårning om följande knappar:

   * **Klicka igenom** (omdirigering) exempelspårning:

      `adbinapp://confirm/?url=https://www.yoursite.com`
   * **Avbryt** (close) exempelspårning:

      `adbinapp://cancel`

## Lokal reservbild {#section_DEACC1CE549B4573B556A44A52409941}

När du skapar ett helskärmsmeddelande kan du välja att ange en reservbild. Om det inte går att hämta den avsedda bilden från webben försöker SDK att läsa in bilden med samma namn från programmets resursmapp. På så sätt kan du visa meddelandet i sin ursprungliga form, även om användaren är offline eller om den förinställda bilden inte är tillgänglig.

>[!IMPORTANT]
>
>Resursnamnet för reservbilden anges när du konfigurerar meddelandet i Adobe Mobile-tjänster och du måste se till att den angivna resursen är tillgänglig.

## Konfigurera meddelandeikoner {#section_DDA28BDBCBB748BCBECF3AB50A177D48}

Följande metoder använder du för att konfigurera de små och stora ikoner som visas i meddelandeområdet och den stora ikonen som visas när meddelanden visas i meddelandelådan.

* **Config.setSmallIconResourceId(int resourceId)**

   Ange den lilla ikon som ska användas för meddelanden som skapas av SDK:n. Den här ikonen visas i statusfältet och är den sekundära bilden som visas när användaren ser det fullständiga meddelandet i meddelandecentret.

   * Här är syntaxen för den här metoden:

      ```java
      public static void setSmallIconResourceId(final int resourceId); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.setSmallIconResourceId(R.drawable.appIcon);
      ```

* **Config.setLargeIconResourceId(int resourceId)**

   Ange den stora ikon som ska användas för meddelanden som skapas av SDK. Den här ikonen är den primära bild som visas när användaren ser det fullständiga meddelandet i meddelandecentret.

   * Här är syntaxen för den här metoden:

      ```java
      public static void setLargeIconResourceId(final int resourceId); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Config.setLargeIconResourceId(R.drawable.appIcon); 
      ```
