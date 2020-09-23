---
description: Information som hjälper dig att ringa anrop till plugin-programmet från dina skript.
keywords: Xamarin
seo-description: Information som hjälper dig att ringa anrop till plugin-programmet från dina skript.
seo-title: Göra anrop till biblioteket
solution: Experience Cloud
title: Göra anrop till biblioteket
uuid: a480201a-4090-4662-8dd8-56f62144cd93
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Göra anrop till biblioteket{#making-calls-to-the-library}

Den här informationen hjälper dig att ringa anrop till plugin-programmet från dina skript.

När du vill anropa plugin-programmet från dina skript måste du importera namnutrymmet.

Genom att använda `Com.Adobe.Mobile`:

* **iOS**: När du har importerat namnutrymmet kan du anropa SDK direkt via de statiska metoderna i `ADBMobile` klasserna.

* **Android**: Du kan anropa SDK direkt via de statiska metoderna i `Config/Analytics/Target/AudienceManager/Media`klasserna.

