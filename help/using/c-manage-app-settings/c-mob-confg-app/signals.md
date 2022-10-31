---
description: Tack vare återkopplingar kan du skicka data som samlats in av Adobe Mobile till en separat tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera Mobiltjänster så att anpassade data skickas till ett mål från en annan leverantör.
title: Konfigurera återanslag
uuid: a026575c-057b-4868-b6c8-9514cbc32b4d
exl-id: 99b27f16-303a-4853-bfdb-2066a53867bf
source-git-commit: 7cfaa5f6d1318151e87698a45eb6006f7850aad4
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# Konfigurera återanslående {#configure-postbacks}

{#eol}

Tack vare återkopplingar kan du skicka data som samlats in av Adobe Mobile till en separat tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera Mobiltjänster så att anpassade data skickas till ett mål från en annan leverantör.

>[!IMPORTANT]
>
>Om du vill använda återanslående måste du installera 4.6 SDK eller senare.

1. Klicka på namnet på det program du vill använda för att gå till sidan Hantera appinställningar och klicka på **[!UICONTROL Manage Postbacks]** på den övre högra sidan.
2. Klicka på **[!UICONTROL Create Postback]**.
3. Skriv följande information i fälten:

   * **[!UICONTROL Postback Type]**

      Välj **[!UICONTROL Custom]**. Mallar kommer att vara tillgängliga i framtiden.

   * **[!UICONTROL Name]**

      Ange ett beskrivande namn för återanslående.

   * **[!UICONTROL URL]**

      Ange en giltig slutpunkts-URL (med lämpliga frågeparametrar efter behov för GET-begäranden). Du får denna URL från den part som du skickar data till (annonsserver eller din egen slutpunkt). Exempel `https://example.com/?user=bob&amp;zip=90210&amp;c16=4.6.0-iOS&amp;c27=cln,132`.

   * **[!UICONTROL Context Variable]**

      Markera delar av URL-adressen och välj den önskade sammanhangsvariabeln i listrutan. Du kan också infoga kontextvariabler i URL-adressen och URL-adressen ersätter alla mallvariabler med värden från träffen.

   * **[!UICONTROL Add Post Body]**

      Ange eventuellt ytterligare innehåll för inlägg, t.ex. för en efterhandsbegäran. Om du anger postbrödtext anger du innehållstypen för postbrödtexten. Exempel, `application/json`.

   * **[!UICONTROL Timeout (in seconds)]**

      Ange hur lång tid (i sekunder) som du vill vänta på återanslående.

   * **[!UICONTROL Trigger(s)]**

      Ange en eller flera datataggar och villkor som utlöser återanslående. Du kan till exempel välja **[!UICONTROL Crashed]** som utlösare och **[!UICONTROL Exists]** som det villkor som utlöser återanslående när programmet kraschar. Du kan också ange vilka mätvärden som aktiverar återanslående. Du kan till exempel välja **[!UICONTROL Device Name]** som utlösare, **[!UICONTROL Equals]** och **[!UICONTROL iPhone 6 Plus]** som villkor för att aktivera återanslående när programmet kraschar på iPhone 6 Plus-enheter.

   * **[!UICONTROL Trait(s)]**
   Ange vem som kan se meddelandet när det utlöses. Alternativen inkluderar **[!UICONTROL Session Length]**, **[!UICONTROL First Launch Date]** och **[!UICONTROL App ID]**.

4. Klicka **[!UICONTROL Save]** för att skapa återanslående och lägga till det i dialogrutan **[!UICONTROL Manage Postbacks]** lista.

   Gör något av följande om du vill aktivera återanslående i framtiden:

   * Markera kryssrutan bredvid återanslående i dialogrutan **[!UICONTROL Manage Postbacks]** lista och klicka på **[!UICONTROL Activate Selected]**.
   * Klicka **[!UICONTROL Save & Activate]** för att spara ändringarna och omedelbart aktivera återanslående.
