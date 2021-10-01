---
description: Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.
solution: Experience Cloud,Analytics
title: Översikt över återgång
uuid: 25e2a5fb-1203-40dd-96cd-b23e0f23376d
exl-id: c5aa0b99-2cb3-4dd7-9da8-e573241e864b
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Översikt över återgång {#postbacks}

Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.

>[!IMPORTANT]
>
>Den här funktionen kräver SDK version 4.6.0 eller senare.

Återställningsmeddelanden köas och följer alla befintliga online-/offlineregler som styr insamling av analysdata. När ett meddelande matchar (som om det visas meddelanden) avbryts inte resten av meddelandena. På så sätt kan flera återanslående göras vid samma analysträff. Definitionen finns i raden *postback* i [ADBMomobile JSON Config](/help/ios/configuration/json-config/json-config.md).

## Malltillägg {#section_6758AD05A24C4E9E965F5253294C164A}

Malltillägg är tillgängliga både i egenskaperna `templateurl` och `templatebody`. Mallobjekt har formatet `{key}`, där `key` är en kontextdatanyckel eller en traditionell datanyckel. De värden som är tillgängliga för mallexpansion är begränsade till [Lifecycle-variabellistan](/help/ios/metrics.md), förutom anpassade data som är kopplade till träffen som utlöser meddelandet. Det finns för närvarande inga historiska eller segmentbaserade data.

Det finns också specifika, reserverade mallar som SDK automatiskt ersätter med interna data som är kända för SDK.

Denna lista innehåller följande:

| Tokennamn | Tokenbeskrivning |
|--- |--- |
| `{%sdkver%}` | Returnerar SDK-versionen. |
| `{%cachebust%}` | Matchar ett slumpmässigt tal mellan 1 och 10000000. |
| `{%adid%}` | Returnerar IDFA. Denna token fungerar bara om du har använt `setAdvertisingIdentifier`. |
| `{%pushid%}` | Returnerar Push-identifierartoken. Denna token fungerar bara om du har använt `setPushIdentifier`. |
| `{%timestampu%}` | Returnerar aktuell tidsstämpel i epok-tid. |
| `{%timestampz%}` | Returnerar den aktuella tidsstämpeln i JavaScript-format (ISO 8601). |
