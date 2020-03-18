---
description: 'På sidan Hantera appinställningar kan du göra följande typer av ändringar '
seo-description: 'På sidan Hantera appinställningar kan du göra följande typer av ändringar '
seo-title: Konfigurera din app
title: Konfigurera din app
uuid: c088e12d-73b6-40c4-b8cc-ec3bb3d3aa4a
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Konfigurera din app {#configuring-your-app}

På sidan Hantera appinställningar kan du göra följande typer av ändringar:

* **Appinformation**

   Det här avsnittet innehåller information om till exempel appens namn, apptyp, nyckeltal, livscykel och platsrapporter.

   * **Livscykelrapporter**

      >[!TIP]
      >
      >Om du har skapat rapportsviten i Adobe Analytics måste du aktivera livscykelrapporter. Om du har skapat rapportsviten i Adobe Mobile är det här alternativet aktiverat som standard.

      I den här rapporten kan du mäta följande mått:

      * **Förvärv**

         Spåra refererande URL:er för appnedladdningskampanjer. Mer information finns i [Anskaffning](/help/using/acquisition-main/acquisition-main.md).

      * **Livscykel**

         Spåra mätvärden och mått som kan mätas automatiskt av mobilbiblioteket när livscykeln är implementerad. Mer information finns i följande avsnitt:

         * [iOS SDK Lifecycle Metrics](/help/ios/metrics.md)
         * [Android Lifecycle Metrics](/help/android/metrics.md)
         * [Windows Lifecycle Metrics](/help/universal-windows/metrics.md)
         * [BlackBerry Lifecycle Metrics](/help/blackberry/metrics.md)
      * **Programåtgärder**

         Aktivera rapporter och kundvägar baserat på åtgärder i appen.

      * **Livstidsvärde**

         Förstå hur användarna får värde över tid genom att använda nyckeltal för appar, som inköp, annonsvisningar, videokompletteringar, sociala resurser, fotoöverföringar med mera.

      * **Timed Events**

         Mät hur lång tid som förflyter (i appen och total tid) mellan viktiga programåtgärder, till exempel tid före första köpet.


* **Platsrapporter**

   Med det här alternativet kan du aktivera rapporter för att spåra latitud och longitud och identifiera specifika intressepunkter (POI). Du kan också spåra bluetooth-fyrar (UUID, major, minor och närhet).

* **Program-SDK och Developer Tester Tools**

   >[!IMPORTANT]
   >
   >Innan du hämtar SDK:er och verktyg måste du konfigurera SDK Analytics-alternativen. Mer information finns i [Konfigurera SDK Analytics-alternativ](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-analytics/t-config-analytics.md).

   När du är redo att uppgradera till 4.x SDK:n, eller om du arbetar med en ny app, hämtar du de senaste SDK:erna och utvecklingsverktygen längst ned på sidan Hantera programinställningar.

   När konfigurationen är klar kan du skicka konfigurationsfilen till utvecklarna så att data kan samlas in på rätt sätt. Om du inte är redo att hämta SDK:er och verktyg nu klickar du på Hantera appinställningar och sedan på appen för att visa appinformationssidan när som helst.