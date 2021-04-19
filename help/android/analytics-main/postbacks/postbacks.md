---
description: Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.
keywords: android;bibliotek;mobil;sdk
seo-description: Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.
seo-title: Eftersläpning
solution: Experience Cloud,Analytics
title: Översikt över återgång
topic-fix: Developer and implementation
uuid: 8bfd4374-2767-421d-891d-e1e9a99b6977
exl-id: 318f6eab-ff71-4bfe-8eb7-51a35380b992
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Eftersläpning {#postbacks}

Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.

>[!IMPORTANT]
>
>Den här funktionen kräver SDK version 4.6.0 eller senare.

Återställningsmeddelanden köas och följer alla befintliga online-/offlineregler som styr insamling av analysdata. När ett meddelande matchar (som om det visas meddelanden) avbryts inte resten av meddelandena. På så sätt kan flera återanslående göras vid samma analysträff. Definitionen finns i raden *postback* i [ADBMomobile JSON Config](/help/android/configuration/json-config/json-config.md).

## Malltillägg {#section_6758AD05A24C4E9E965F5253294C164A}

Malltillägg är tillgängliga i egenskaperna `templateurl` och `templatebody`. Mallobjekt har formen `{key}`, där `key` är en kontextdatanyckel eller en traditionell datanyckel. Värdena som är tillgängliga för mallexpansion är begränsade till [Livscykelmåtten](/help/android/metrics.md), utöver eventuella anpassade data som är kopplade till träffen som utlöser meddelandet. Det finns för närvarande inga historik- eller segmentbaserade data.

Det finns också specifika, reserverade mallar som SDK automatiskt ersätter med interna data som är kända för SDK.

Denna lista innehåller följande:

| Tokennamn | Tokenbeskrivning |
|--- |--- |
| {%sdkver%} | Returnerar SDK-versionen. |
| {%cacheBust%} | Matchar ett slumpmässigt tal mellan 1 och 10000000. |
| {%adid%} | Returnerar Advertiser-ID för Android. Obs! Detta fungerar bara om du har använt `submitAdvertisingIdentifierTask`. |
| {%pushid%} | Returnerar Push-identifierartoken. Obs! Detta fungerar bara om du har använt `setPushIdentifier`. |
| {%timestampu%} | Returnerar aktuell tidsstämpel i epok-tid. |
| {%timestampz%} | Returnerar den aktuella tidsstämpeln i JavaScript-format (ISO 8601). |
