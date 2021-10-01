---
description: Den här informationen kan hjälpa dig att felsöka meddelanden i appen.
keywords: mobil
solution: Experience Cloud,Analytics
title: Felsöka meddelanden i appen
topic-fix: Metrics
uuid: 8813e8d8-bb1e-46ad-83cd-98ae68f73ce6
exl-id: 6be5beef-3bde-49f8-9ec0-c5d32bd43045
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Felsökning av meddelanden i appen{#troubleshooting-in-app-messaging}

Den här informationen kan hjälpa dig att felsöka meddelanden i appen.

Om du har uppfyllt alla krav för meddelanden i appen, men meddelanden inte visas, kontrollerar du följande:

## Placerar du den nya konfigurationen och nya SDK i appen?

* Kontrollera att SDK är version 4.2 eller senare och är korrekt konfigurerat.

* Kontrollera att du har ett [Meddelandeavsnitt](/help/using/in-app-messaging/in-app-messaging.md) i konfigurationen (den hämtade JSON-filen) eller en fjärrslutpunkt för Meddelanden, så att den kan hämtas från dynamisk tagghantering.

## Mitt helskärmsmeddelande i Android visas inte. Jag använder rätt SDK, konfiguration och mina utlösare uppfylls.

Uppdaterade du manifestfilen för att definiera helskärmsaktiviteten?

## Mitt lokala meddelande i Android fungerar inte.

Kontrollera att den lokala meddelandemottagaren har deklarerats i ditt manifest. Mer information finns i steg 1 i [Meddelanden i appen](/help/android/messaging-main/messaging/messaging.md).

## Är meddelandet live?

Kontrollera listvyn i kolumnen **[!UICONTROL Status]** på sidan Hantera meddelanden i appen och kontrollera om meddelandet är live.

## Titta på *visa en gång*, *visa alltid*, *visa offline*-inställningar på målsidan.

Kontrollera att de här inställningarna är korrekta. Granska alternativen på fliken **[!UICONTROL Trigger]** på sidan Målgrupp, där du kan ange hur ofta meddelandet ska visas.

## Om starthändelse används som utlösare..

Starta bara en ny session. Information om när en session börjar finns i `lifecycleTimeout` i filen [ADBMomobile JSON config](/help/ios/configuration/json-config/json-config.md).

## Jag har uppdaterat mitt meddelande på distans, men min app visar fortfarande det gamla meddelandet.

Gör något av följande:

* Dynamisk tagghantering kan ta några minuter att uppdatera slutpunkten med den nya definitionen.

   Ge den lite tid och försök igen.

* Konfigurationen uppdateras endast vid en ny start.

   Om appen startades om under tidsgränsen för livscykelsessionen kanske din nya konfiguration inte har hämtats.

## Min bild passar inte in exakt i det utrymme som mallen ger.

Helskärmsmallen för meddelanden i appen stöder visning av en bild från en fjärrserver (Image URL) eller från programpaketet (Bundled Image). Bilden ska ha standardbildformat, till exempel JPG, GIF eller PNG.

På grund av att enhetsskärmar har många olika dimensioner får bilden förmodligen inte plats exakt i det utrymme som mallen ger. Mallen fokuserar alltid på att visa bildens mitt och beskär (stående) eller tonar (liggande) sidorna om bilden inte får plats.

Här följer de exakta placerings- och storleksreglerna för varje orientering:

* **Stående**, där bilden skalas till höjden 195px för telefonen, 529px för surfplattan, centrerad om bildbredden är mindre än enhetsbredden och beskuren om bildbredden är större än enhetsbredden.

* **Liggande**, där bilden skalas till 100 % av enhetens höjd, är bredden 75 % av enheten och med en toning till höger.

   Om du har problem med helskärmsmallen kan du hämta och använda den anpassade HTML-mallen. Mallen Anpassad HTML ger större flexibilitet för bilder och ger fullständig kontroll över mallen.

## Mina meddelanden återspeglar inte ändringar/uppdateringar som jag har gjort i användargränssnittet.

SDK hämtar nya/uppdaterade meddelanden när en livscykel startas. Detta gäller endast när programmet stängs/bakomliggande under längre tid än tidsgränsen för livscykeln och sedan öppnas igen.

Utför följande steg:

1. Rulla URL:en för meddelanden i konfigurationsfilen för att verifiera att fjärrmeddelandet har uppdaterats (till exempel `curl "https://assets.adobedtm.com/b213090c5204bf94318f4ef0539a38b487d10368/scripts/satellite-542c62859662383b1a0008f4.json"`)
1. Stäng programmet.
1. Vänta en tidsperiod som är längre än `lifecycleTimeout` i konfigurationsfilen.
1. Öppna appen, navigera till den plats där meddelandet ska visas och kontrollera att det har uppdaterats.
