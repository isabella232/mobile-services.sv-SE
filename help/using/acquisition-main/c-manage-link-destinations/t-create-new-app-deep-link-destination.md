---
description: Du kan skapa ett nytt länkmål som dirigerar användarna till en webbsida eller en djup länk i appen.
keywords: mobil
seo-description: Du kan skapa ett nytt länkmål som dirigerar användarna till en webbsida eller en djup länk i appen.
seo-title: Skapa nytt länkmål
solution: Experience Cloud,Analytics
title: Skapa nytt länkmål
topic-fix: Metrics
uuid: 390e3dea-0221-4f97-980d-a90ca9f162fa
exl-id: 2d2f5938-1461-43e2-a375-45c18afc9d5a
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Skapa ett nytt länkmål {#create-new-link-destination}

Du kan skapa ett nytt länkmål som dirigerar användarna till en webbsida eller en djup länk i appen.

1. Klicka på **[!UICONTROL Manage Apps]** i gränssnittet för mobila tjänster.
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

         Skriv en webb-HTTP- eller HTTPS-URL, till exempel`https://adobe.com`. Webblänksmål dirigerar användare till en URL. Du kan t.ex. dirigera användare till en produktlinje på en webbutik.

      * **[!UICONTROL Hybrid Link]**

         Skriv en iOS Universal Link eller en Android App Link (till exempel `https://yourwebsite.com`). Hybridlänkar har stöd för universella iOS-länkar eller Android-applänkar.
   * **[!UICONTROL App]**
Välj det program som är associerat med länken som du ska ange.

      >[!TIP]
      >
      >Den här informationen krävs bara om du har valt en App Deep Link eller en Hybrid Link i **[!UICONTROL Link Type]**. Om appen inte visas i urvalslistan klickar du på **[!UICONTROL Add New App]** för att referera till en ny app från en appbutik.

   * **[!UICONTROL Link type]**

      Skriv den faktiska URL-adressen för den länk du markerade. Etiketten för det här fältet varierar beroende på vilken typ av länk du har valt.

   * **[!UICONTROL Notes]**

      Ange valfria anteckningar för destinationen. Ytterligare anteckningar visas endast på sidan Hantera länkmål i användargränssnittet för Adobe Mobile Services. Ytterligare anteckningar kan hjälpa dig eller andra i organisationen att snabbt hitta ett specifikt länkmål och kan ge insikt i dess syfte, vilken kampanj det är knutet till eller något annat som du anser vara viktigt.


1. Klicka på **Spara**.
