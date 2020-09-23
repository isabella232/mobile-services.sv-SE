---
description: Rapporten Åtgärdssökvägar baseras på sökvägsanalys och visar ett bandiagram som representerar de sökvägar som har tagits från ett läge till ett annat i appen.
keywords: mobile
seo-description: Rapporten Åtgärdssökvägar baseras på sökvägsanalys och visar ett bandiagram som representerar de sökvägar som har tagits från ett läge till ett annat i appen.
seo-title: Rapporten Handlingsvägar
solution: Experience Cloud,Analytics
title: Rapporten Handlingsvägar
topic: Reports,Metrics
uuid: a21e5d9e-fd57-4178-9d64-87181b7f988b
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# Rapporten Handlingsvägar{#action-paths}

Rapporten Åtgärdssökvägar baseras på sökvägsanalys och visar ett bandiagram som representerar de sökvägar som har tagits från ett läge till ett annat i appen.

Både **[!UICONTROL View Paths]** och **[!UICONTROL Action Paths]** rapporter är lappningsrapporter. I rapporten visas hur användare navigerar i appen från en skärm till nästa. **[!UICONTROL View Paths]** Rapporten visar **[!UICONTROL View Actions]** i vilken ordning användare utför åtgärder och händelser, t.ex. klickningar, markeringar, storleksändringar och så vidare.

>[!TIP]
>
>Du kan använda en trattrapport för att kombinera navigering och åtgärder i en rapport. Mer information finns i [Tratt](/help/using/usage/reports-funnel.md).

![](assets/action_paths.png)

Varje nod, i form av en ruta, representerar ett läge i användarnas sökvägar via en app. I bilden ovan representerar till exempel den översta noden antalet användare som startade appen och sedan valde ett foto från galleriet.

Om du vill visa alternativ för att ändra diagrammet klickar du på en nod och sedan på **[!UICONTROL Focus]** eller **[!UICONTROL Expand]**. Om du till exempel klickar på **[!UICONTROL PhotoPicked]** läget i den övre noden visas ikonerna **[!UICONTROL Focus]** och **[!UICONTROL Expand]** ikonerna.

![](assets/action_paths_icons.png)

Klicka på **[!UICONTROL +]** ikonen om du vill expandera. Det här alternativet visar de ytterligare sökvägar som kommer in i eller ut ur noden. I bilden nedan startar läge 1 appen, läge 2 väljer ett foto (det objekt du tidigare expanderade) och läge 3 omfattar de olika sökvägar som användarna tog:

* Markera ett objekt
* Lägga till ett objekt
* Dra ett objekt
* Skalförändra ett objekt

Att expandera ett läge liknar en tratt.

![åtgärdsbana expandera](assets/action_paths_expand.png)

Om du vill isolera noden och visa sökvägar som kommer in i och går ut ur den markerade noden klickar du på ![fokusikonen](assets/icon_focus.png) . I bilden nedan slutfördes följande banor **innan** användarna markerade ett foto:

* Rotera ett objekt
* Skalförändra ett objekt
* Dra ett objekt
* Ta bort ett objekt

Av de användare som har markerat ett foto fylldes följande sökvägar i **efter** att fotot har markerats:

* Markera ett objekt
* Lägga till ett objekt
* Dra ett objekt
* Skalförändra ett objekt

![åtgärdssökvägfokus](assets/action_paths_focus.png)

Du kan fokusera eller utöka flera noder för att få en detaljerad vy över sökvägar som användarna använder i din app. Exempel:

![åtgärdsbana flera](assets/action_paths_mult.png)

Du kan konfigurera följande alternativ för den här rapporten:

* **[!UICONTROL Time Period]**

   Klicka på **[!UICONTROL Calendar]** ikonen för att välja en egen punkt eller för att välja en förinställd tidsperiod i listrutan.

* **[!UICONTROL Customize]**

   Anpassa era rapporter genom att ändra **[!UICONTROL Show By]** alternativen, lägga till mätvärden och filter, lägga till ytterligare serier (mätvärden) med mera. Mer information finns i [Anpassa rapporter](/help/using/usage/reports-customize/reports-customize.md).

* **[!UICONTROL Filter]**

   Klicka **[!UICONTROL Filter]** för att skapa ett filter som spänner över olika rapporter för att se hur ett segment fungerar i alla mobilrapporter. Med ett klisterlappsfilter kan du definiera ett filter som ska användas på alla rapporter som inte är avsedda för målning. Mer information finns i [Lägga till ett klisterfilter](/help/using/usage/reports-customize/t-sticky-filter.md).

* **[!UICONTROL Download]**

   Klicka **[!UICONTROL PDF]** eller **[!UICONTROL CSV]** för att ladda ned eller öppna dokument och dela med användare som inte har tillgång till Mobile Services eller för att använda filen i presentationer.