---
description: Du kan dirigera användare till ett mål beroende på om de har appen installerad (en applänk) eller inte (till en webbplats eller en appbutik).
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Insticksannonser
topic-fix: Metrics
uuid: 7dce8ab2-2a5d-4384-ac1e-e31dfaa33654
exl-id: b6d4588f-4f28-4c1b-9291-f4b9154d84f7
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# Insticksannonser{#interstitials}

Du kan dirigera användare till ett mål beroende på om de har appen installerad (en applänk) eller inte (till en webbplats eller en appbutik). Användarna får bäst val av routning. Marknadsförarna kan erbjuda användaren valmöjligheter genom att konfigurera en interstitiell sida som visar vilka landningsdestinationer som är tillgängliga för användarna.

Så här konfigurerar du en interstititet när du skapar en marknadsföringslänk:

1. Klicka på **[!UICONTROL Edit Deep Link Interstitial]**.

   ![Interstitiell djuplänk](assets/interstitial2.png)

1. Skriv information i följande fält:

   * **[!UICONTROL Custom HTML]**

      Välj en anpassad interstitiell HTML-sida.

      Genom att använda anpassade interstitialer kan marknadsförarna anpassa interstitiella landningssidor med anpassade HTML/CSS/JS, som gör att ni kan märka upp era sidor.

      Här följer kraven för HTML:

      * Måste vara en HTML-fil.
      * Måste innehålla `%%DEST%%` och `%%FALLBACK%%` platshållare.
      * Det överförda HTML kommer att hanteras i en `<iframe>`.

         Du måste se till att länkmålen pekar på ett överordnat fönster. Du kan inkludera `<base target="_parent" />` in `<head>` eller ange en målegenskap för varje `<a/>` individuellt.

         >[!TIP]
         >
         >Om du överför anpassad HTML används inte de andra fyra alternativen i den här tabellen om du inte tar bort den överförda filen.
   * **[!UICONTROL Image URL]**

      Ange URL-adressen till en bildresurs.

   * **[!UICONTROL Body Text]**

      Ange brödtexten för interstitialen.

   * **[!UICONTROL Confirm Text]**

      Ange texten för textknappen.

   * **[!UICONTROL  Fallback Text]**

      Ange den reservtext som ska visas.

      Det här fältet uppdaterar textknappen om en djup länk misslyckas. Användarna uppmanas att prova den djupa länken innan de kan välja ett annat alternativ. En reservlösning kan till exempel vara till en appbutik för att hämta och installera appen eller ta användare till företagets webbplats. Med reservtexten kan användarna se att det finns ett annat alternativ om den djupa länken misslyckas.


1. (**Valfritt**) Klicka på ikonerna ovanför bilden för att se hur det interaktiva ser ut att rotera och på olika enheter.

   Du kan ändra eller redigera bilden utanför Mobile Services för att se till att den visas korrekt i olika situationer.
1. Klicka på **[!UICONTROL Save]**.
