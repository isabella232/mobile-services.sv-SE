---
description: Med Adobe Mobile och Adobe Mobile SDK kan du skicka push-meddelanden till dina användare. Med SDK kan du även enkelt rapportera användare som har öppnat din app efter att ha klickat igenom ett push-meddelande.
seo-description: Med Adobe Mobile och Adobe Mobile SDK kan du skicka push-meddelanden till dina användare. Med SDK kan du även enkelt rapportera användare som har öppnat din app efter att ha klickat igenom ett push-meddelande.
seo-title: Push-meddelanden
solution: Marketing Cloud,Analytics
title: Push-meddelanden
topic: Developer and implementation
uuid: 729d4010-3733-4dff-b188-ad45bd3e7cc4
translation-type: tm+mt
source-git-commit: 17cb91a28966cf32f955a2cb724e89ab228de5b8

---


# Push-meddelanden {#push-messaging}

Med Adobe Mobile och Adobe Mobile SDK kan du skicka push-meddelanden till dina användare. Med SDK kan du även enkelt rapportera användare som har öppnat din app efter att ha klickat igenom ett push-meddelande.

Om du vill använda push-meddelanden **måste** du ha SDK version 4.6 eller senare.

>[!IMPORTANT]
>
>Ange inte Experience Cloud-ID:t i appen manuellt. Detta skapar en ny unik användare som inte får push-meddelanden på grund av sin anmälningsstatus. En användare har till exempel valt att ta emot push-meddelanden som loggar in i din app. När du har loggat in skapas en ny unik användare som inte har valt att ta emot push-meddelanden om du manuellt anger ID:t i appen. Den nya användaren kommer inte att få dina push-meddelanden.
>
>Det går inte att flytta appen till en ny rapportserie. Om du migrerar till en ny rapportserie kan din push-konfiguration brytas och meddelanden kanske inte skickas.

## Aktivera push-meddelanden {#section_CBD63C5B11FE4424BC2BF552C23F2BD9}

>[!TIP]
>
>Om ditt program redan är konfigurerat för att använda meddelanden via FCM (Firebase Cloud Messaging) kan vissa av följande steg redan vara slutförda.

1. Kontrollera att `ADBMobileConfig.json` filen innehåller de inställningar som krävs för push-meddelanden.

   Objektet måste ha sin `"marketingCloud"` `"org"` egenskap konfigurerad för push-meddelanden.

   ```js
   "marketingCloud": { 
     "org": <org-id-string> 
    }
   ```

1. Hämta registrerings-ID/token med Firebase Cloud Messaging-API:t (FCM).

   * Mer information om hur du konfigurerar FCM finns i [Konfigurera en Firebase Cloud Messaging-klientapp på Android](https://firebase.google.com/docs/cloud-messaging/android/client).

   ```js
   String token = FirebaseInstanceId.getInstance().getToken();
   ```

1. Registrerings-ID/-token måste skickas till SDK med hjälp av `Config.setPushIdentifier(final String registrationId)` metoden.

   ```js
   Config.setPushIdentifier(token); // token was obtained in step 2
   ```

1. Aktivera rapportering genom att skicka aktiviteten i `collectLifecycleData` metoden.

   Här följer kraven för att aktivera push-klickningsrapportering:

   * I din implementering av `FireBaseMessageService`måste det Bundle-objekt som innehåller meddelandedata, som skickas till `onMessageReceived` metoden med RemoteMessage-objektet, läggas till i den återgivning som används för att öppna målaktiviteten med en klickning. Detta kan göras med hjälp av `putExtras` metoden. Mer information finns i [putExtras](https://developer.android.com/reference/android/content/Intent.html#putExtras(android.os.Bundle))).

   ```java
   Intent intent = new Intent(this, MainActivity.class);
      intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
   // get the bundle from the RemoteMessage object
      intent.putExtras(message.toIntent().getExtras());
   ```

   * I målaktiviteten för klickningen måste aktiviteten skickas till SDK med `collectLifecycleData` anropet.

      Kom ihåg följande information:

      * Använd `Config.collectLifecycleData(this)` eller `Config.collectLifecycleData(this, contextData)`.

      * Använd **inte** `Config.collectLifecycleData()`.



