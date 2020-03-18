---
description: I följande tabell beskrivs de olika appidentifierarna som används av iOS SDK och Adobe Mobile-tjänsterna.
seo-description: I följande tabell beskrivs de olika appidentifierarna som används av iOS SDK och Adobe Mobile-tjänsterna.
seo-title: Program-ID
solution: Marketing Cloud,Analytics
title: Program-ID
topic: Developer and implementation
uuid: 24ebc716-23c7-4ee8-8256-b534210367e0
translation-type: tm+mt
source-git-commit: 0e22d5e080b680ff6b23462f1bc12f27d99e6d42

---


# Program-ID {#app-ids}

I följande tabell beskrivs de olika appidentifierarna som används av iOS SDK och Adobe Mobile-tjänsterna.

| ID | Beskrivning |
|--- |--- |
| ID skickat med livscykelvärden | Detta är en kombination av appnamnet och paketversionen som skickas till appbutiken.  Det här värdet används för Versionsrapporten i Adobe Mobile-tjänster och du kan använda det här värdet för att filtrera resultaten efter en viss version av din app. |
| App Store-ID | Detta ID tilldelas till din app av appbutiken och tillhandahålls i Adobe Mobile Services när du skapar värvningslänkar. |
| AppID i ADBMomobile JSON-konfiguration | Detta ID är ett unikt ID som tilldelas programinstansen av Adobe Mobile Services för alla associerade metadata i systemet.  Detta ID används för att skapa unika URL:er för anskaffningsspårning eller spårningslänk, läggs automatiskt till i ADBMomobile JSON-konfigurationsfilen när den hämtas från användargränssnittet och finns i Hantera appinställningar under värvningsinställningarna för din app. |

