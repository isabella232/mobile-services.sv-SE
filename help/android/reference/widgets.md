---
description: Android-widgetar kan spåras med samma metoder som din app. Widgetar delar programkontexten med din app, så träffordningen och besökaridentifieringen bevaras.
keywords: android;library;mobile;sdk
seo-description: Android-widgetar kan spåras med samma metoder som din app. Widgetar delar programkontexten med din app, så träffordningen och besökaridentifieringen bevaras.
seo-title: Android-widgetar
solution: Marketing Cloud,Analytics
title: Android-widgetar
topic: Developer and implementation
uuid: 1a3718ff-967b-4c8e-ae0b-ba15bddbda0a
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Android-widgetar {#android-widgets}

Android-widgetar kan spåras med samma metoder som din app. Widgetar delar programkontexten med din app, så träffordningen och besökaridentifieringen bevaras.

Följande riktlinjer hjälper dig att spåra Android-widgetar:

* Implementera inte livscykelmätningsanrop ( `startActivity`/ `stopActivity`) i widgeten.

* Om du vill spåra när en widget läggs till på startskärmen lägger du till ett `trackState` eller `trackEvent` anrop till `onEnabled` widgetmetoden.

* Om du vill spåra när programmet startas från en widget lägger du till ett `trackState` eller `trackEvent` samtal innan du skapar metoden för att starta programmet.

* Om du vill spåra innehållet i ett funktionsmakro kan du definiera en `ContextData` variabel som ger möjlighet att segmentera varje funktionsmakro separat (till exempel `AppExperienceType="widget"` kontra. `app`).

