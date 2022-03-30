---
description: I följande tabell beskrivs de olika appidentifierare som används av iOS SDK och Adobe Mobile-tjänsterna.
solution: Experience Cloud Services,Analytics
title: Program-ID
topic-fix: Developer and implementation
uuid: 24ebc716-23c7-4ee8-8256-b534210367e0
exl-id: 82f0a097-b2eb-4313-8624-dd442e3da039
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 1%

---

# Program-ID {#app-ids}

I följande tabell beskrivs de olika appidentifierare som används av iOS SDK och Adobe Mobile-tjänsterna.

| ID | Beskrivning |
|--- |--- |
| ID skickat med livscykelvärden | Detta är en kombination av appnamnet och paketversionen som skickas till appbutiken.  Det här värdet används för Versions-rapporten i Adobe Mobile och du kan använda det här värdet för att filtrera resultatet efter en viss version av din app. |
| App Store ID | Detta ID tilldelas till din app av appbutiken och tillhandahålls i Adobe Mobile-tjänster när du skapar värvningslänkar. |
| AppID i ADBMomobile JSON-konfiguration | Detta ID är ett unikt ID som tilldelas programinstansen av Adobe Mobile-tjänster för alla associerade metadata i systemet.  Detta ID används för att skapa unika URL:er för anskaffningsspårning eller spårningslänk, läggs automatiskt till i ADBMomobile JSON-konfigurationsfilen när den hämtas från användargränssnittet och finns i Hantera appinställningar under värvningsinställningarna för din app. |
