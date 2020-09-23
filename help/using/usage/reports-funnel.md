---
description: Trattrapporten identifierar var kunderna övergav en marknadsföringskampanj eller avvände från en definierad konverteringsväg när de interagerade med mobilappen. Du kan också använda Funnel-rapporten för att jämföra åtgärder för olika segment.
keywords: mobile
seo-description: Trattrapporten identifierar var kunderna övergav en marknadsföringskampanj eller avvände från en definierad konverteringsväg när de interagerade med mobilappen. Du kan också använda Funnel-rapporten för att jämföra åtgärder för olika segment.
seo-title: Trattrapport
solution: Experience Cloud,Analytics
title: Trattrapport
topic: Reports,Metrics
uuid: 268b4ab9-2e29-4423-9f79-ad93f5231ede
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Trattrapport{#funnel}

Rapporten identifierar **[!UICONTROL Funnel]** var kunderna övergav en marknadsföringskampanj eller avvände från en definierad konverteringsväg när de interagerade med mobilappen. Du kan också använda rapporten för att jämföra åtgärder för olika segment **[!UICONTROL Funnel]** .

Genom att få insyn i kundens beslut i varje steg får ni en förståelse för var de är avskräckta, vilken väg de tenderar att följa och när kunderna lämnar er app.

När du öppnar **[!UICONTROL Funnel]** rapporten måste du skapa en anpassad tratt. Mer information finns i [Anpassa rapporter](/help/using/usage/reports-customize/reports-customize.md).

>[!TIP]
>
>Spara URL:en när du har konfigurerat inställningarna och kör rapporten för att spara den anpassade tratten. Du kan dela URL-adressen eller spara den i ett dokument.

Här är ett exempel på den här rapporten:

![](assets/funnel_create.png)

För att demonstrera en enkel tratt finns inställningarna för en konfiguration som använder tre trattsteg och två trattjämförelser. Vi antar att en demoapp tillåter användare att lägga till ett objekt, till exempel ett foto, och sedan dela det.

I fönstret Anpassa finns det avsnitt som anger att användaren har startat appen, lagt till ett foto från ett galleri i appen, delat ett eller flera foton från appen på sociala medier, sms, e-post och så vidare. Med trattjämförelserna kan du jämföra nivåerna för att lägga till och dela foton mellan användare av iOS-appen och Android-appen.

Klicka på **[!UICONTROL Run]** för att generera rapporten.

Här är ett exempel på en genererad rapport:

![](assets/funnel.png)

Den första serien visar att 100 procent av användarna startade appen. Den andra serien visar att en högre andel Android-användare lade till ett foto från galleriet. Den tredje serien visar att nästan hälften av iOS-användarna delade fotot, men ingen av Android-användarna delade det. Detta kan tyda på ett problem med appen som behöver undersökas.

Om du vill visa ytterligare information för du musen över en stapel i diagrammet.

Du kan konfigurera följande alternativ för den här rapporten:

* **[!UICONTROL Time Period]**

   Klicka på **[!UICONTROL Calendar]** ikonen för att välja en egen punkt eller för att välja en förinställd tidsperiod i listrutan.
* **[!UICONTROL Customize]**

   Anpassa era rapporter genom att ändra **[!UICONTROL Show By]** alternativen, lägga till mätvärden och filter, lägga till ytterligare serier (mätvärden) med mera. Mer information finns i [Anpassa rapporter](/help/using/usage/reports-customize/reports-customize.md).
* **[!UICONTROL Filter]**

   Klicka **[!UICONTROL Filter]** för att skapa ett filter som spänner över olika rapporter för att se hur ett segment fungerar i alla mobilrapporter. Med ett klisterlappsfilter kan du definiera ett filter som ska användas på alla rapporter som inte är avsedda för målning. Mer information finns i [Lägg till anteckningsfilter](/help/using/usage/reports-customize/t-sticky-filter.md).
* **[!UICONTROL Download]**

   Klicka **[!UICONTROL PDF]** eller **[!UICONTROL CSV]** för att ladda ned eller öppna dokument och dela med användare som inte har tillgång till Mobile Services eller för att använda filen i presentationer.