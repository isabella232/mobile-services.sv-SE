---
description: Den här informationen hjälper dig att anpassa de inbyggda rapporterna genom att lägga till ytterligare filter (segment).
keywords: mobile
seo-description: Den här informationen hjälper dig att anpassa de inbyggda rapporterna genom att lägga till ytterligare filter (segment).
seo-title: Lägg till filter i rapporter
solution: Experience Cloud,Analytics
title: Lägg till filter i rapporter
topic: Reports,Metrics
uuid: 19c395cc-2e07-4588-825b-f2f8b10a87c1
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Lägg till filter i rapporter{#add-filters-to-reports}

Den här informationen hjälper dig att anpassa de inbyggda rapporterna genom att lägga till ytterligare filter (segment).

>[!IMPORTANT]
>
>Mätvärden för mobilappar finns också i marknadsföringsrapporter och -analyser, ad hoc-analyser, data warehouse och andra analysrapporteringsgränssnitt. Om det inte finns någon nedbrytning- eller rapporttyp i Adobe Mobile kan den genereras med ett annat rapporteringsgränssnitt.

I det här exemplet anpassar vi **[!UICONTROL Users & Sessions]** rapporten, men instruktionerna gäller för alla rapporter.

1. Öppna appen och klicka på **[!UICONTROL Usage]** > **[!UICONTROL Users & Sessions]**.

   ![](assets/customize1.png)

   Den här rapporten ger en fullständig övertidsöversikt över våra appanvändare. Mätvärden för både iOS- och Android-versionerna av appen samlas dock in i samma rapportserie. Vi kan segmentera användare med mobiloperativsystem genom att lägga till ett anpassat filter i användarens mått.

1. Klicka på **[!UICONTROL Customize]**.

   ![](assets/customize2.png)

1. Klicka under **[!UICONTROL Users]** och **[!UICONTROL Add Filter]** klicka **[!UICONTROL Add Rule]**.

1. Markera **[!UICONTROL Operating Systems]** och välj i listrutan **[!UICONTROL iOS]**.

   ![](assets/customize3.png)

   Om du vill lägga till Android som ett filter måste du upprepa det här steget.

1. Klicka **[!UICONTROL And]** på, välj **[!UICONTROL Operating Systems]** i listrutan och välj **[!UICONTROL Android]**.

   Filtren ska nu se ut som i följande exempel:

   ![](assets/customize4.png)

1. Klicka på **[!UICONTROL Update]**.
1. Klicka på **[!UICONTROL Run]** om du vill återskapa rapporten.

   Den här rapporten visar nu användare uppdelade efter operativsystem. Rapporttiteln ändrades så att den matchar de filter som tillämpades på rapporten.

   ![](assets/customize5.png)

   Du kan anpassa den här rapporten mer. Från iOS 8.3 kan du lägga till måttet First Launches med ett iOS 8.3-operativsystemsfilter för att se hur många iOS 8.3-kunder som uppgraderade sina appar och startade första gången.
1. Klicka **[!UICONTROL First Launches]** på **[!UICONTROL Add Filter]**, klicka **[!UICONTROL Add Rule]**, välj **[!UICONTROL Operating Systems]** i listrutan och välj **[!UICONTROL iOS]**.
1. Klicka **[!UICONTROL And]** på, välj **[!UICONTROL Operating System Versions]** i listrutan och välj **[!UICONTROL iOS 8.3]**.

   Filtren ska nu se ut som i följande exempel:

   ![](assets/customize6.png)

1. Klicka **[!UICONTROL Update]** och **[!UICONTROL Run]**.

   Den här rapporten visar nu användare med iOS 8.3 som har startat programmet för första gången.

   ![](assets/customize7.png)

   Testa de olika alternativen på rapportanpassningsmenyn och se till att du bokmärker dina favoriter. Rapports-URL:er i Adobe Mobile fungerar och kan skickas med e-post eller läggas till i dina favoriter.
