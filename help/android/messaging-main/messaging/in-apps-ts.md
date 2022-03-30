---
description: Den här informationen hjälper dig att felsöka meddelanden i appen.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Felsöka meddelanden i appen
topic-fix: Metrics
uuid: 39c3a21d-92c2-4004-b00f-99b6f91d3696
exl-id: 6c7d97ed-3b0a-48ff-b761-1485aea5e96d
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Felsöka meddelanden i programmet{#troubleshooting-in-app-messaging}

Den här informationen hjälper dig att felsöka meddelanden i appen.

Om du har uppfyllt alla krav för meddelanden i appen, men meddelandena inte visas, kontrollerar du följande:

## Placerar du den nya konfigurationen och nya SDK i appen?

Se till att du har en [Meddelanden i appen](/help/android/messaging-main/messaging/messaging.md) -avsnittet i din konfiguration (hämtad JSON-fil) eller har en Messages-fjärrslutpunkt, så att den kan hämtas från dynamisk tagghantering.

## Mitt helskärmsmeddelande i Android visas inte. Jag använder rätt SDK, konfiguration och mina utlösare uppfylls.

Uppdaterade du manifestfilen för att definiera helskärmsaktiviteten?

## Mitt lokala meddelande i Android fungerar inte.

Kontrollera att den lokala meddelandemottagaren har deklarerats i ditt manifest. Mer information finns i steg 2 i *Aktivera meddelanden i appen* in [Meddelanden i appen](/help/android/messaging-main/messaging/messaging.md).

## Är meddelandet live?

Verifiera om ditt meddelande är live på sidan Hantera meddelanden i appen i **[!UICONTROL Status]** kontrollerar du listan med meddelanden.

## Titta på *visa en gång*, *visa alltid*, *visa offline*  på fliken Målgrupp.

Kontrollera att inställningarna är som du vill ha dem. På **[!UICONTROL Audience]** -flik, granska **[!UICONTROL Trigger]** så att du kan ange hur ofta meddelandet ska visas.

## Om en starthändelse används som utlösare..

Starta bara en ny session. Mer information om när en session påbörjas finns i `lifecycleTimeout` rad in [JSON-konfiguration](/help/android/configuration/json-config/json-config.md).

## Jag har uppdaterat mitt meddelande på distans, men min app visar fortfarande det gamla meddelandet.

Kom ihåg följande information:

* Dynamisk tagghantering kan ta några minuter att uppdatera slutpunkten med den nya definitionen. Vänta en stund och försök igen.
* Konfigurationen uppdateras endast vid en ny start. Om appen startades om under tidsgränsen för livscykelsessionen kanske din nya konfiguration inte har hämtats.

Mer information finns i [Livscykelvärden](/help/android/metrics.md).

## Min bild passar inte in exakt i det utrymme som mallen ger.

Helskärmsmallen för meddelanden i appen stöder visning av en bild från en fjärrserver (Image URL) eller från programpaketet (Bundled Image). Bilden ska ha standardbildformat, t.ex. JPG, GIF eller PNG. Eftersom enhetsskärmar har många olika dimensioner får bilden troligtvis inte plats exakt i det utrymme som mallen ger. Mallen fokuserar på att visa bildens mitt och, om bilden inte får plats, beskär (stående) eller tonar (liggande) sidorna.

Här följer de exakta placerings- och storleksreglerna för varje orientering:

* **Stående**
   * Höjden 195 pixlar för telefoner.
   * En höjd på 529px för tabletter.
   * Centrerad om bildens bredd är mindre än enhetens bredd.
   * Beskuren om bildbredden är större än enhetens bredd.

* **Liggande**
   * Bilden skalades till 100 % av enhetens höjd.
   * Bredden är 75 % av enheten och tonas ut till höger.
   Om du har problem med helskärmsmallen kan du hämta och använda mallen Egna HTML. Den här mallen ger större flexibilitet för bilder och ger fullständig kontroll över mallen.
