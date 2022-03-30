---
description: Information som hjälper dig att ringa anrop till plugin-programmet från dina skript.
keywords: Xamarin
solution: Experience Cloud Services
title: Göra anrop till biblioteket
uuid: a480201a-4090-4662-8dd8-56f62144cd93
exl-id: a5ec1e1b-e29a-42c9-bcc9-bee05c427044
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Göra anrop till biblioteket{#making-calls-to-the-library}

Den här informationen hjälper dig att ringa anrop till plugin-programmet från dina skript.

När du vill anropa plugin-programmet från dina skript måste du importera namnutrymmet.

Genom att använda `Com.Adobe.Mobile`:

* **iOS**: När du har importerat namnutrymmet kan du anropa SDK direkt via de statiska metoderna i `ADBMobile` klasser.

* **Android**: Du kan anropa SDK direkt via de statiska metoderna i `Config/Analytics/Target/AudienceManager/Media`klasser.
