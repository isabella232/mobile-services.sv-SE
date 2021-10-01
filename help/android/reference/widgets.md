---
description: Android-widgetar kan spåras med samma metoder som din app. Widgetar delar programkontexten med din app, så träffordningen och besökaridentifieringen bevaras.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Android-widgetar
topic-fix: Developer and implementation
uuid: 1a3718ff-967b-4c8e-ae0b-ba15bddbda0a
exl-id: 229ea987-256a-45f4-a5ca-afe17dd596b8
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Android-widgetar {#android-widgets}

Android-widgetar kan spåras med samma metoder som din app. Widgetar delar programkontexten med din app, så träffordningen och besökaridentifieringen bevaras.

Följande riktlinjer hjälper dig att spåra Android-widgetar:

* Implementera inte livscykelmätvärden ( `startActivity`/ `stopActivity`) i widgeten.

* Om du vill spåra när en widget läggs till på startskärmen lägger du till ett `trackState`- eller `trackEvent`-anrop till metoden `onEnabled` för widgeten.

* Om du vill spåra när programmet startas från en widget lägger du till ett `trackState`- eller `trackEvent`-anrop innan du skapar metoden för att starta programmet.

* Om du vill spåra innehållet i en åtgärd kan du definiera en `ContextData`-variabel som ger möjlighet att segmentera varje åtgärd separat (till exempel `AppExperienceType="widget"` vs. `app`).
