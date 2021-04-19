---
description: Den här informationen hjälper dig att felsöka meddelanden i appen.
keywords: mobil
seo-description: Den här informationen hjälper dig att felsöka meddelanden i appen.
seo-title: Felsöka meddelanden i appen
solution: Experience Cloud,Analytics
title: Felsöka meddelanden i appen
topic-fix: Metrics
uuid: 39c3a21d-92c2-4004-b00f-99b6f91d3696
exl-id: 6c7d97ed-3b0a-48ff-b761-1485aea5e96d
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Felsöka meddelanden i programmet{#troubleshooting-in-app-messaging}

Den här informationen hjälper dig att felsöka meddelanden i appen.

Om du har uppfyllt alla krav för meddelanden i appen, men meddelandena inte visas, kontrollerar du följande:

## Placerar du den nya konfigurationen och nya SDK i appen?

Se till att du har ett [avsnitt i appmeddelanden](/help/android/messaging-main/messaging/messaging.md) i din konfiguration (hämtad JSON-fil) eller en fjärrslutpunkt för Meddelanden, så att den kan hämtas från dynamisk tagghantering.

## Mitt helskärmsmeddelande i Android visas inte. Jag använder rätt SDK, konfiguration och mina utlösare uppfylls.

Uppdaterade du manifestfilen för att definiera helskärmsaktiviteten?

## Mitt lokala meddelande i Android fungerar inte.

Kontrollera att den lokala meddelandemottagaren har deklarerats i ditt manifest. Mer information finns i steg 2 i *Aktivera meddelanden i appen* i [Meddelanden i appen](/help/android/messaging-main/messaging/messaging.md).

## Är meddelandet live?

Kontrollera meddelandelistan på sidan Hantera meddelanden i appen i kolumnen **[!UICONTROL Status]** för att verifiera om meddelandet är live.

## Titta på *visa en gång*, *visa alltid*, *visa offlineinställningar* på fliken Målgrupp.

Kontrollera att inställningarna är som du vill ha dem. Granska dina **[!UICONTROL Trigger]**-alternativ på fliken **[!UICONTROL Audience]**, där du kan ange hur ofta meddelandet ska visas.

## Om en starthändelse används som utlösare..

Starta bara en ny session. Mer information om när en session börjar finns i `lifecycleTimeout`-raden i [JSON Config](/help/android/configuration/json-config/json-config.md).

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
   Om du har problem med helskärmsmallen kan du hämta och använda den anpassade HTML-mallen. Den här mallen ger större flexibilitet för bilder och ger fullständig kontroll över mallen.
