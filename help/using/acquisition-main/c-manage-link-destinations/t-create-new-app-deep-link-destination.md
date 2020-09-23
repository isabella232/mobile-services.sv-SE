---
description: Du kan skapa ett nytt länkmål som dirigerar användarna till en webbsida eller en djup länk i appen.
keywords: mobile
seo-description: Du kan skapa ett nytt länkmål som dirigerar användarna till en webbsida eller en djup länk i appen.
seo-title: Skapa nytt länkmål
solution: Experience Cloud,Analytics
title: Skapa nytt länkmål
topic: Metrics
uuid: 390e3dea-0221-4f97-980d-a90ca9f162fa
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Skapa ett nytt länkmål {#create-new-link-destination}

Du kan skapa ett nytt länkmål som dirigerar användarna till en webbsida eller en djup länk i appen.

1. Klicka på i gränssnittet för mobila tjänster **[!UICONTROL Manage Apps]**.
1. Klicka på appens namn för att visa dess app informationssida.
1. Klicka på **[!UICONTROL Manage Link Destinations]**.
1. Klicka på **[!UICONTROL Create New]**.
1. Skriv information i följande fält:
   * **[!UICONTROL Title]**

      Ange ett beskrivande namn för applänkens mål. Titeln visas bara på sidan Hantera länkmål i användargränssnittet för Adobe Mobile Services. Ett beskrivande namn hjälper dig eller andra i organisationen att snabbt hitta ett specifikt länkmål och kan ge dig insikt i dess syfte.

   * **[!UICONTROL Link Type]**

      Här är en lista över tillgängliga länktyper:

      * **[!UICONTROL App Deep Link]**

         Ange en djup länk för URI-schema (till exempel `yourapp://section`). Destinationslänken för appen är djupa länkar i URI-scheman som dirigerar användare till en djup länk i appen. Du kan till exempel dirigera användare till en viss produktlinje i en onlinebutiks mobilapp.

      * **[!UICONTROL Web Link]**

         Skriv till exempel en webb-HTTP- eller HTTPS-URL`https://adobe.com`. Webblänksmål dirigerar användare till en URL. Du kan t.ex. dirigera användare till en produktlinje på en webbutik.

      * **[!UICONTROL Hybrid Link]**

         Skriv en iOS Universal Link eller en Android App Link (till exempel `https://yourwebsite.com`). Hybridlänkar har stöd för universella iOS-länkar eller Android-applänkar.
   * **[!UICONTROL App]**
Välj det program som är associerat med länken som du ska ange.

      >[!TIP]
      >
      >Den här informationen krävs bara om du har valt en App Deep Link (App Deep Link) eller en Hybrid Link (Hybrid Link) i **[!UICONTROL Link Type]**. Om appen inte visas i urvalslistan klickar du för **[!UICONTROL Add New App]** att referera till en ny app från en appbutik.

   * **[!UICONTROL Link type]**

      Skriv den faktiska URL-adressen för den länk du markerade. Etiketten för det här fältet varierar beroende på vilken typ av länk du har valt.

   * **[!UICONTROL Notes]**

      Ange valfria anteckningar för destinationen. Ytterligare anteckningar visas endast på sidan Hantera länkmål i användargränssnittet för Adobe Mobile Services. Ytterligare anteckningar kan hjälpa dig eller andra i organisationen att snabbt hitta ett specifikt länkmål och kan ge insikt i dess syfte, vilken kampanj det är knutet till eller något annat som du anser vara viktigt.


1. Klicka på **Spara**.
