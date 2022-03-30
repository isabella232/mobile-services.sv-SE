---
description: Konfigurera upplevelsealternativ för meddelanden i appen, inklusive typ (helskärm, varning eller meddelanden) och alternativ för visning, text och knappar.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Experience In-App Message
topic-fix: Metrics
uuid: 4c6d6756-47fb-4f1b-8338-0b0c9b0fceb0
exl-id: eeb1527d-c546-4951-9947-db810fdb8eee
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Upplevelse: meddelande i appen {#experience-in-app-message}

Konfigurera upplevelsealternativ för meddelanden i appen, inklusive typ (helskärm, varning eller meddelanden) och alternativ för visning, text och knappar.

1. Klicka på **[!UICONTROL Messaging]** > **[!UICONTROL Manage Messages]** > **[!UICONTROL Create Message]** > **[!UICONTROL Create In-App]**.
1. Skriv ett namn för meddelandet på Experience-sidan.
1. Fyll i fälten i **[!UICONTROL Type]** avsnitt:

   * **[!UICONTROL Type]**
Välj meddelandetyp för din kampanj i appen:

      * **[!UICONTROL Full Screen]**
      * **[!UICONTROL Alert]**
      * **[!UICONTROL Local Notification]**
   * **[!UICONTROL Template]**

      Anpassa en temamall för responsiva meddelanden för ditt innehåll.

      >[!TIP]
      >
      >Det här alternativet visas bara när du väljer **[!UICONTROL Full Screen]** meddelandetyp.

   * **[!UICONTROL Custom]**

      Läs in HTML-innehåll (endast helskärm). Du måste ange en klicklänk och en länk för att avbryta.

      1. Klicka **[!UICONTROL Browse]** och ladda ned en HTML-fil eller dra ett HTML-dokument till fönstret.
      1. Klicka **[!UICONTROL Download Example]** om du vill visa exempel på anpassat HTML-innehåll.

      >[!TIP]
      >
      >Det här alternativet visas bara när du väljer **[!FHelskärm]** meddelandetyp.



1. Fyll i fälten i **[!UICONTROL Display]** avsnitt:

   * **[!UICONTROL Theme]**

   Välj ett tema för meddelandet.

   * **[!UICONTROL Layout]**

      Välj programlayouten på enhetsskärmen.

   * **[!UICONTROL Image URL]**

      URL:en för en bild. Om du har problem med att ändra storlek när du använder helskärmsmallen finns mer information i *Min bild passar inte in exakt i det utrymme som mallen ger* in [Felsökning av meddelanden i appen](/help/using/in-app-messaging/t-in-app-message/in-apps-ts.md).

   * **[!UICONTROL Bundled Image]**

      Sökväg till en bild i programkodpaketet. Det här alternativet används när det inte finns någon bild. eller så är bilden inte tillgänglig. Tänk dig att det kanske inte går att komma åt om till exempel enheten är offline. Om du har problem med att ändra storlek när du använder helskärmsmallen finns mer information i *Min bild passar inte in exakt i det utrymme som mallen ger* in [Felsökning av meddelanden i appen](/help/using/in-app-messaging/t-in-app-message/in-apps-ts.md).


1. Fyll i fälten i **[!UICONTROL Text]** avsnitt:

   * **[!UICONTROL Header]**

      Skriv texten för meddelandehuvudet.

   * **[!UICONTROL Content]**

      Skriv texten för meddelandets innehåll.

1. Fyll i fälten i **[!UICONTROL Buttons]** avsnitt:

   * **[!UICONTROL Click-Through Button]**

      Etikett för **[!UICONTROL Click-Through]** -knappen. Om du trycker på den här knappen räknas det som en lyckad klickning. Användaren omdirigeras till målet.

   * **[!UICONTROL Destination]**

      Välj ett specifikt mål, till exempel en webb-, djup- eller hybridlänk, för att skicka användare när de klickar igenom meddelandet. Omdirigerings-URL för en lyckad klickning.

      Denna URL kan innehålla följande information:

      * `{userId}`, som ersätts med användaridentifieraren eller är tom när användaridentifieraren inte har angetts.
      * `{trackingId}`, som ersätts med stödet (korreleras med *s_vi* cookie).
      * `{messageId}`, som ersätts med det unika ID:t för meddelandet i appen.
      * `{lifetimeValue}`, som ersätts med livstidsvärdet eller 0 om det inte finns något livstidsvärde.

      Här följer ett exempel på hur du spårar användar-ID: `https://www.mysite.com?uid={userId}`.

      Om klicknings-URL:en använder `https://` eller `https://`öppnas URL:en i enhetens webbläsare utanför appen. Annars har varje plattform stöd för scheman som gör att du kan öppna eller referera till appen om appen har utvecklats för att stödja det anpassade schemat.

      >[!TIP]
      >
      >När du använder **[!UICONTROL Web Link]** eller **[!UICONTROL Custom Link]** måltyper, måltypen spåras inte. Endast **[!UICONTROL Deep Links]** spåras. Mer information finns i [Destinationer](/help/using/acquisition-main/c-create-destinations.md).


1. (Valfritt) Förhandsgranska layouten för meddelandet genom att klicka på följande ikoner:

   * **[!UICONTROL Summary]** döljer förhandsgranskningsfönstret.

      Klicka ![förhandsgranska](assets/icon_preview.png) för att visa förhandsgranskningsfönstret igen.

   * **[!UICONTROL Change the orientation]**

      Om du vill ändra orienteringen för förhandsvisningen från stående till liggande klickar du på ![orientering](assets/icon_orientation.png). För provkartor ändras orienteringen från en rund till en fyrkantig bevakningsyta.

   * **[!UICONTROL Preview on a user's watch]**

      Om du vill förhandsgranska meddelandet så som det kommer att visas på en användares bevakning klickar du på ![bevakningsikon](assets/icon_watch.png).

   * **[!UICONTROL Preview on a user's mobile phone]**

      Om du vill förhandsgranska meddelandet så som det kommer att visas på en användares mobiltelefon klickar du ![telefon, ikon](assets/icon_phone.png).

   * **[!UICONTROL Preview on a user's tablet]**

      Om du vill förhandsgranska meddelandet på en surfplatta klickar du på ![ikon för surfplatta](assets/icon_tablet.png).

      Längst ned i förhandsgranskningsfönstret kan du visa en beskrivning av målgruppen som du valde i föregående steg. Du kan även visa en beskrivning av den målgrupp du valde i det föregående steget längst ned i förhandsgranskningsfönstret.

1. Konfigurera [Schemaläggningsalternativ](/help/using/in-app-messaging/t-in-app-message/c-schedule-in-app-message.md).
