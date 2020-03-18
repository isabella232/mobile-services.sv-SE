---
description: Den här informationen hjälper dig att felsöka meddelanden i appen.
keywords: mobile
seo-description: Den här informationen hjälper dig att felsöka meddelanden i appen.
seo-title: Felsöka meddelanden i appen
solution: Marketing Cloud,Analytics
title: Felsöka meddelanden i appen
topic: Metrics
uuid: 58533aa3-2eb2-4597-8525-77e4e5975e56
translation-type: tm+mt
source-git-commit: 1154bab39b5215e00d47ad8e66caeec15e4e98de

---


# Felsökning av meddelanden i appen{#troubleshooting-in-app-messaging}

Den här informationen hjälper dig att felsöka meddelanden i appen.

Om du har uppfyllt alla krav för meddelanden i appen, men meddelandena inte visas, kontrollerar du följande:

## Placerar du den nya konfigurationen och nya SDK i appen?

Kontrollera att SDK är version 4.2 eller senare och korrekt konfigurerad. Kontrollera att du har ett `Messages` avsnitt i konfigurationen (hämtad JSON-fil) eller en fjärrslutpunkt för Meddelanden, så att den kan hämtas från dynamisk tagghantering.

## Mitt helskärmsmeddelande i Android visas inte. Jag använder rätt SDK, konfiguration och mina utlösare uppfylls.

Uppdaterade du manifestfilen för att definiera helskärmsaktiviteten?

## Mitt lokala meddelande i Android fungerar inte.

Kontrollera att den lokala meddelandemottagaren har deklarerats i ditt manifest. Mer information finns i steg 2 i [Aktivera meddelanden](/help/android/messaging-main/messaging/messaging.md)i appen.

## Är meddelandet live?

Kontrollera listvyn på sidan Hantera meddelanden i appen i kolumnen Status och kontrollera om den är aktiv.

## Titta på *visa en gång*, *visa alltid*, *visa offlineinställningar* på fliken Målgrupp.

Kontrollera att inställningarna är som du vill ha dem. Granska dina **[!UICONTROL Audience]** alternativ på **[!UICONTROL Trigger]** fliken, där du kan ange hur ofta meddelandet ska visas.

## Om starthändelse används som utlösare..

Starta bara en ny session. Mer information om när en session påbörjas finns på `lifecycleTimeout` raden i JSON-konfigurationsfilen. Mer information finns i [ADBMomobile JSON Config](/help/ios/configuration/json-config/json-config.md).

## Jag har uppdaterat mitt meddelande på distans, men min app visar fortfarande det gamla meddelandet.

Gör något av följande:

* Dynamisk tagghantering kan ta några minuter att uppdatera slutpunkten med den nya definitionen.

   Vänta en stund och försök igen.

* Konfigurationen uppdateras endast vid en ny start.
Om appen startades om under tidsgränsen för livscykelsessionen kanske din nya konfiguration inte har hämtats.

   Mer information finns i [Livscykelvärden](/help/ios/metrics.md).

## Min bild passar inte in exakt i det utrymme som mallen ger.

Helskärmsmallen för meddelanden i appen stöder visning av en bild från en fjärrserver (Image URL) eller från programpaketet (Bundled Image). Bilden ska ha standardbildformat, t.ex. JPG, GIF eller PNG.

Eftersom enhetsskärmar har många olika dimensioner får bilden troligtvis inte plats exakt i det utrymme som mallen ger. Mallen fokuserar på att visa bildens mitt och, om bilden inte får plats, beskär (stående) eller tonar (liggande) sidorna.

Här följer de exakta placerings- och storleksreglerna för varje orientering:

* **Stående**:
   * Höjden 195 px för telefoner
   * En höjd på 529px för tabletter
   * Centrerad om bildens bredd är mindre än enhetens bredd.
   * Beskuren om bildbredden är större än enhetens bredd.

* **Liggande**:
   * Bilden skalades till 100 % av enhetens höjd.
   * Bredden är 75 % av enheten och tonas ut till höger.

Om du har problem med helskärmsmallen kan du hämta och använda den anpassade HTML-mallen. Den här mallen ger större flexibilitet för bilder och ger fullständig kontroll över mallen.

## Meddelanden i appen på en iPhone X visas inte i helskärmsläge.

Så här visar du meddelanden i appen i helskärmsläge på en iPhone X:

1. Lägg till `viewport-fit=cover` i meta-taggen.

   ```html
   <meta name="viewport" content="viewport-fit=cover">
   ```

1. Ställ in lämplig utfyllnad i CSS för det översta gränssnittselementet som:

   ```html
   topelement {
     padding-top:20px;
     /*Status bar height on iOS 11.0*/
     padding-top:constant(safe-area-inset-top);
     /*Status bar height on iOS 11+ */
     padding-top:env(safe-area-inset-top);
     } 
   ```

   De här inställningarna förhindrar att gränssnittselementen kolliderar med statusfältet.
