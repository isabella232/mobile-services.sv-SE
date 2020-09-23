---
description: Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.
seo-description: Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.
seo-title: Eftersläpning
solution: Experience Cloud,Analytics
title: Översikt över återgång
uuid: 25e2a5fb-1203-40dd-96cd-b23e0f23376d
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Översikt över återgång {#postbacks}

Tack vare återkopplingar kan du skicka data som samlas in av SDK till en tredjepartsserver. Genom att utnyttja samma utlösare och egenskaper som du använder för att visa ett meddelande i appen kan du konfigurera SDK:n så att den skickar anpassade data till ett mål från en annan leverantör.

>[!IMPORTANT]
>
>Den här funktionen kräver SDK version 4.6.0 eller senare.

Återställningsmeddelanden köas och följer alla befintliga online-/offlineregler som styr insamling av analysdata. När ett meddelande matchar (som om det visas meddelanden) avbryts inte resten av meddelandena. På så sätt kan flera återanslående göras vid samma analysträff. Definitionen finns i *återställningsraden* i [ADBMomobile JSON Config](/help/ios/configuration/json-config/json-config.md).

## Malltillägg {#section_6758AD05A24C4E9E965F5253294C164A}

Malltillägg är tillgängliga i både `templateurl` - och `templatebody` -egenskaper. Mallobjekt har formen av `{key}`, där `key` är en kontextdatanyckel eller en traditionell datanyckel. De värden som är tillgängliga för mallexpansion är begränsade till [standardlistan](/help/ios/metrics.md)med livscykelvariabler, utöver anpassade data som är kopplade till träffen som utlöser meddelandet. Det finns för närvarande inga historiska eller segmentbaserade data.

Det finns också specifika, reserverade mallar som SDK automatiskt ersätter med interna data som är kända för SDK.

Denna lista innehåller följande:

| Tokennamn | Tokenbeskrivning |
|--- |--- |
| `{%sdkver%}` | Returnerar SDK-versionen. |
| `{%cachebust%}` | Matchar ett slumpmässigt tal mellan 1 och 10000000. |
| `{%adid%}` | Returnerar IDFA. Den här variabeln fungerar bara om du använder den `setAdvertisingIdentifier`. |
| `{%pushid%}` | Returnerar Push-identifierartoken. Den här variabeln fungerar bara om du använder den `setPushIdentifier`. |
| `{%timestampu%}` | Returnerar aktuell tidsstämpel i epok-tid. |
| `{%timestampz%}` | Returnerar den aktuella tidsstämpeln i JavaScript-format (ISO 8601). |