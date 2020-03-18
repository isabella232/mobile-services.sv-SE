---
description: Du kan använda den här informationen för att konfigurera alternativen för push-tjänster på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.
keywords: mobile
seo-description: Du kan använda den här informationen för att konfigurera alternativen för push-tjänster på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.
seo-title: Konfigurera push-meddelanden
solution: Marketing Cloud,Analytics
title: Konfigurera push-meddelanden
topic: Metrics
uuid: 6763858d-6046-4d36-87c0-cf3600a44fb1
translation-type: tm+mt
source-git-commit: 2c85c31d2fa54de26771553a6d349d3101e0048c

---


# Konfigurera push-meddelanden{#configure-push-messaging}

Du kan använda den här informationen för att konfigurera alternativen för push-tjänster på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.

Innan du konfigurerar push-meddelanden slutför du de nödvändiga åtgärderna i [Förutsättningar för att aktivera push-meddelanden](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/prerequisites-push-messaging.md).

* **Rapportera Suite-överväganden**

   Du kan konfigurera en app store-app för Apple och en för Google i varje rapportserie. Om du behöver ytterligare program, till exempel ett för en produktionsmiljö och ett för en utvecklingsmiljö, skapar du en ny app för appbutiken och en ny rapportsserie för varje miljö.

>[!IMPORTANT]
>
>Det går inte att flytta appen till en ny rapportserie. Om du migrerar till en ny rapportserie kan din push-konfiguration brytas och meddelanden kanske inte skickas.

1. Skriv information i följande fält under **[!UICONTROL Push Services]**:

   * Apple

      **[!UICONTROL Private Key]**

      Bläddra till och välj en giltig privat nyckel `.p12`eller `.key``.pen`.

      >[!IMPORTANT]
      >Om filen som du väljer för **[!UICONTROL Private Key]** indata även innehåller ett certifikat behöver du inte ange certifikatet.

   * **[!UICONTROL Certificate]**

      Ange ett giltigt certifikat. Det här alternativet är bara obligatoriskt när **[!UICONTROL Private Key]** indata **inte** innehåller något certifikat. Mer information om hur du hämtar SSL-certifikatet och den privata nyckeln finns i [Konfigurera appen att använda APNS eller FCM](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/configure-app-apns-gcm.md).

   * Google

      **[!UICONTROL API Key]**

      Ange en giltig API-nyckel. Mer information om hur du hämtar API-nyckeln finns i [Konfigurera appen att använda APNS eller FCM](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/configure-app-apns-gcm.md).

      Mer information finns i följande avsnitt:

      * [Push-meddelanden i Android](/help/android/messaging-main/push-messaging/push-messaging.md)
      * [Push Messaging i iOS](/help/ios/messaging-main/push-messaging/push-messaging.md)

1. Klicka på **[!UICONTROL Save]**.
