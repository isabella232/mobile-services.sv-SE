---
description: I följande tabell beskrivs de olika appidentifierarna som används av Android SDK och Adobe Mobile-tjänsterna.
solution: Experience Cloud Services,Analytics
title: Program-ID
topic-fix: Developer and implementation
uuid: 3ac99489-6269-439e-a814-24102ef220b1
exl-id: 28358dd6-50dd-4ba9-9fb0-5271eae69d28
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Program-ID{#app-ids}

I följande tabell beskrivs de olika appidentifierarna som används av Android SDK och Adobe Mobile-tjänsterna.

| ID | Beskrivning |
|--- |--- |
| ID skickat med livscykelvärden | Detta är en kombination av appnamnet och paketversionen som skickas till appbutiken. Det här värdet används för Versions-rapporten i Adobe Mobile-tjänster och du kan filtrera med det här värdet för att segmentera efter en specifik version av din app. |
| App Store ID | Detta ID tilldelas till din app av appbutiken och tillhandahålls i Adobe Mobile-tjänster när du skapar värvningslänkar. |
| AppID i ADBMomobile JSON-konfiguration | Detta är ett unikt ID som tilldelas programinstansen av Adobe Mobile-tjänster för alla associerade metadata i systemet. Detta ID används för att skapa unika URL:er för anskaffningsspårning eller spårningslänk. Detta ID läggs automatiskt till i JSON-konfigurationsfilen för ADBMomobile när den här filen hämtas från användargränssnittet och finns i Hantera appinställningar under värvningsinställningarna för din app. |
