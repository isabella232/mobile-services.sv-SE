---
description: I följande tabell beskrivs de olika appidentifierarna som används av iOS SDK och Adobe Mobile-tjänsterna.
seo-description: I följande tabell beskrivs de olika appidentifierarna som används av iOS SDK och Adobe Mobile-tjänsterna.
seo-title: Program-ID
solution: Experience Cloud,Analytics
title: Program-ID
topic: Developer and implementation
uuid: 24ebc716-23c7-4ee8-8256-b534210367e0
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Program-ID {#app-ids}

I följande tabell beskrivs de olika appidentifierarna som används av iOS SDK och Adobe Mobile-tjänsterna.

| ID | Beskrivning |
|--- |--- |
| ID skickat med livscykelvärden | Detta är en kombination av appnamnet och paketversionen som skickas till appbutiken.  Det här värdet används för Versions-rapporten i Adobe Mobile-tjänster, och du kan använda det här värdet för att filtrera resultaten efter en viss version av din app. |
| App Store-ID | Detta ID tilldelas till din app av appbutiken och tillhandahålls i Adobe Mobile-tjänster när du skapar värvningslänkar. |
| AppID i ADBMomobile JSON-konfiguration | Detta ID är ett unikt ID som tilldelas appinstansen av Adobe Mobile-tjänster för alla associerade metadata i systemet.  Detta ID används för att skapa unika URL:er för anskaffningsspårning eller spårningslänk, läggs automatiskt till i ADBMomobile JSON-konfigurationsfilen när den hämtas från användargränssnittet och finns i Hantera appinställningar under värvningsinställningarna för din app. |

