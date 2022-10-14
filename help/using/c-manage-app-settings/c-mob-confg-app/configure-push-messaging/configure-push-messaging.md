---
description: Du kan använda den här informationen för att konfigurera alternativen för push-tjänster på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Konfigurera push-meddelanden
topic-fix: Metrics
uuid: 6763858d-6046-4d36-87c0-cf3600a44fb1
exl-id: d4989c31-2692-4062-8fae-d41c3e3c179b
source-git-commit: dbe3af75010fbf5195a3f93fc43cb696aaa32b65
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Konfigurera push-meddelanden{#configure-push-messaging}

Du kan använda den här informationen för att konfigurera alternativen för push-tjänster på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.

Innan du konfigurerar push-meddelanden slutför du de nödvändiga uppgifterna i [Krav för att aktivera push-meddelanden](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/prerequisites-push-messaging.md).

* **Rapportera Suite-överväganden**

   Du kan konfigurera en app för appbutiken för Apple och en för Google i varje rapportserie. Om du behöver ytterligare program, till exempel ett för en produktionsmiljö och ett för en utvecklingsmiljö, skapar du en ny app för appbutiken och en ny rapportsserie för varje miljö.

>[!IMPORTANT]
>
>Det går inte att flytta appen till en ny rapportserie. Om du migrerar till en ny rapportserie kan din push-konfiguration brytas och meddelanden kanske inte skickas.

1. Skriv information i följande fält under **[!UICONTROL Push Services]**:

   * Apple

      **[!UICONTROL Private Key]**

      Bläddra till och välj en giltig privat nyckel `.p12`, `.key`, eller `.pen`.

      >[!IMPORTANT]
      >Om filen som du väljer för **[!UICONTROL Private Key]** indata innehåller också ett certifikat. Du behöver inte ange certifikatet.

   * **[!UICONTROL Certificate]**

      Ange ett giltigt certifikat. Det här alternativet är endast obligatoriskt när **[!UICONTROL Private Key]** input does **not** innehåller ett certifikat. Mer information om hur du hämtar SSL-certifikatet och den privata nyckeln finns i [Konfigurera appen att använda APNS eller FCM](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/configure-app-apns-gcm.md).

   * Google

      **[!UICONTROL API Key]**

      Ange en giltig API-nyckel. Mer information om hur du hämtar API-nyckeln finns i [Konfigurera appen att använda APNS eller FCM](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/configure-app-apns-gcm.md).

2. Klicka på **[!UICONTROL Save]**.
