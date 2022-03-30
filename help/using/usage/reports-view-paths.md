---
description: Rapporten Visa sökvägar, som baseras på sökvägsanalys, visar ett bandiagram som representerar de sökvägar som har tagits mellan lägena i appen.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Visa rapport om sökvägar
topic-fix: Reports,Metrics
uuid: bc73edce-0cc0-4349-9a48-e0a40cbe1b67
exl-id: 475dbe01-fa4d-433c-ac77-68f2a6972c0c
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Visa rapport om sökvägar {#view-paths}

The **[!UICONTROL View Paths]** rapporten, som baseras på sökvägsanalys, visar ett målningsdiagram som representerar de sökvägar som har tagits mellan lägena i appen.

>[!TIP]
>
>The **[!UICONTROL View Paths]** och **[!UICONTROL View Action]** rapporter är likartade eftersom båda är pajrapporter. The **[!UICONTROL View Paths]** kan du se hur användarna navigerar i appen från en skärm till nästa. The **[!UICONTROL View Actions]** rapporten visar den åtgärdssekvens (händelser, t.ex. klick, markeringar, storleksändring o.s.v.) som användare utför i din app. Du kan använda en trattrapport för att kombinera navigering och åtgärder i en rapport. Mer information finns i [Tratt](/help/using/usage/reports-funnel.md).

![visa banor](assets/view_paths.png)

Varje nod, i form av en ruta, representerar ett läge i användarnas sökvägar via en app. I bilden ovan representerar till exempel den översta noden antalet användare som startade programmet och navigerade till huvudvyn.

När du klickar på en nod för att ange ytterligare alternativ för att ändra diagrammet, ytterligare alternativ som **[!UICONTROL Focus]** eller **[!UICONTROL Expand]** visas. När du till exempel klickar på **[!UICONTROL MainView]** i den övre noden, **[!UICONTROL Focus]** och **[!UICONTROL Expand]** visas ikoner.

Klicka på **[!UICONTROL +]** om du vill visa ytterligare sökvägar som kommer in i eller går från noden. I bilden nedan startar läge 1 appen, läge 2 visar programmets huvudsida och läge 3 innehåller följande sökvägar som användarna har tagit:

* Navigera till kamerarullen
* navigera till objektväljaren
* navigera till kameran
* navigera till objektinformationssidan

![](assets/view_paths_expand.png)

Klicka ![fokusikon](assets/icon_focus.png) för att isolera noden och visa sökvägarna som kommer in i och går ut ur den markerade noden. I bilden nedan gick följande sökvägar före användare som visade programmets huvudvy:

* objektinformation
* objektväljare
* Kamerarulle
* Kamera

![visa banfokus](assets/view_paths_focus.png)

Du kan fokusera eller utöka flera noder för att få en detaljerad vy över de sökvägar som användarna tar i appen. Exempel:

![visa bana flera](assets/view_paths_mult.png)

Du kan konfigurera följande alternativ för den här rapporten:

* **[!UICONTROL Time Period]**
Klicka på **[!UICONTROL Calendar]** om du vill välja en anpassad punkt eller välja en förinställd tidsperiod i listrutan.
* **[!UICONTROL Customize]**
Anpassa dina rapporter genom att ändra **[!UICONTROL Show By]** alternativ, lägga till mätvärden och filter, lägga till ytterligare serier (mätvärden) med mera. Mer information finns i [Anpassa rapporter](/help/using/usage/reports-customize/reports-customize.md).
* **[!UICONTROL Filter]**
Klicka **[!UICONTROL Filter]** för att skapa ett filter som spänner över olika rapporter för att se hur ett segment fungerar i alla mobilrapporter. Med ett klisterlappsfilter kan du definiera ett filter som ska användas på alla rapporter som inte är avsedda för målning. Mer information finns i [Lägg till anteckningsfilter](/help/using/usage/reports-customize/t-sticky-filter.md).
* **[!UICONTROL Download]**
Klicka **[!UICONTROL PDF]** eller **[!UICONTROL CSV]** för att ladda ned eller öppna dokument och dela med användare som inte har tillgång till Mobile Services eller för att använda filen i presentationer.
