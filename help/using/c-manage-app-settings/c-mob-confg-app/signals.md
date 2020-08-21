---
description: Tack vare återkopplingar kan du skicka data som samlats in av Adobe Mobile till en separat tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera Mobiltjänster så att anpassade data skickas till ett mål från en annan leverantör.
seo-description: Tack vare återkopplingar kan du skicka data som samlats in av Adobe Mobile till en separat tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera Mobiltjänster så att anpassade data skickas till ett mål från en annan leverantör.
seo-title: Konfigurera återanslag
title: Konfigurera återanslag
uuid: a026575c-057b-4868-b6c8-9514cbc32b4d
translation-type: tm+mt
source-git-commit: 7ae626be4d71641c6efb127cf5b1d3e18fccb907
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---


# Konfigurera återanslående {#configure-postbacks}

Tack vare återkopplingar kan du skicka data som samlats in av Adobe Mobile till en separat tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera Mobiltjänster så att anpassade data skickas till ett mål från en annan leverantör.

>[!IMPORTANT]
>
>Om du vill använda återanslående måste du installera 4.6 SDK eller senare. Mer information finns i [Android - Postback](/help/android/analytics-main/postbacks/postbacks.md) eller [iOS - Postback](/help/ios/analytics-main/postback/postback.md).

1. Klicka på namnet på det program du vill använda för att gå till sidan Hantera appinställningar och klicka på **[!UICONTROL Manage Postbacks]** länken längst upp till höger.
1. Klicka på **[!UICONTROL Create Postback]**.
1. Skriv följande information i fälten:

   * **[!UICONTROL Postback Type]**

      Välj **[!UICONTROL Custom]**. Mallar kommer att vara tillgängliga i framtiden.

   * **[!UICONTROL Name]**

      Ange ett beskrivande namn för återanslående.

   * **[!UICONTROL URL]**

      Ange en giltig slutpunkts-URL (med lämpliga frågeparametrar efter behov för GET-begäranden). Du får denna URL från den part som du skickar data till (annonsserver eller din egen slutpunkt). Exempel `https://my.server.com/?user=bob&amp;zip=90210&amp;c16=4.6.0-iOS&amp;c27=cln,132`.

   * **[!UICONTROL Context Variable]**

      Markera delar av URL-adressen och välj den önskade sammanhangsvariabeln i listrutan. Du kan också infoga kontextvariabler i URL-adressen och URL-adressen ersätter alla mallvariabler med värden från träffen.

   * **[!UICONTROL Add Post Body]**

      Ange eventuellt ytterligare innehåll för inlägg, t.ex. för en efterhandsbegäran. Om du anger postbrödtext anger du innehållstypen för postbrödtexten. Exempel, `application/json`.

   * **[!UICONTROL Timeout (in seconds)]**

      Ange hur lång tid (i sekunder) som du vill vänta på återanslående.

   * **[!UICONTROL Trigger(s)]**

      Ange en eller flera datataggar och villkor som utlöser återanslående. Du kan till exempel välja **[!UICONTROL Crashed]** som utlösare och **[!UICONTROL Exists]** som villkor för återanslående när programmet kraschar. Du kan också ange vilka mätvärden som aktiverar återanslående. Du kan till exempel välja **[!UICONTROL Device Name]** som utlösare **[!UICONTROL Equals]** och **[!UICONTROL iPhone 6 Plus]** som villkor för att aktivera återanslående när appen kraschar på iPhone 6 Plus-enheter.

   * **[!UICONTROL Trait(s)]**
   Ange vem som kan se meddelandet när det utlöses. Alternativen är **[!UICONTROL Session Length]**, **[!UICONTROL First Launch Date]**, och **[!UICONTROL App ID]**.

1. Klicka **[!UICONTROL Save]** för att skapa återanslående och lägga till det i **[!UICONTROL Manage Postbacks]** listan.

   Gör något av följande om du vill aktivera återanslående i framtiden:

   * Markera kryssrutan bredvid återanslående i **[!UICONTROL Manage Postbacks]** listan och klicka på **[!UICONTROL Activate Selected]**.
   * Klicka **[!UICONTROL Save & Activate]** för att spara ändringarna och omedelbart aktivera återanslående.
