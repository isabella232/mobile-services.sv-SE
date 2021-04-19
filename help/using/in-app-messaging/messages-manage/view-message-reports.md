---
description: Du kan visa meddelanderapporter för meddelanden i programmet och push-meddelanden.
keywords: mobil
seo-description: Du kan visa meddelanderapporter för meddelanden i programmet och push-meddelanden.
seo-title: Visa meddelanderapporter
solution: Experience Cloud,Analytics
title: Visa meddelanderapporter
topic-fix: Metrics
uuid: 0ac73a81-388f-4dfd-84d5-21b8db4b8c83
exl-id: b8a2dd7a-02e1-47ce-9e8e-c1419b707b44
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Visa meddelanderapporter{#view-message-reports}

Du kan visa meddelanderapporter för meddelanden i programmet och push-meddelanden.

1. Klicka på ![rapportikonen](assets/icon_report.png) i **[!UICONTROL Report]**-kolumnen för ett meddelande.
1. (**Valfritt**) Skapa ett klisterfilter för rapporten eller ändra tidsperioden genom att klicka på ikonen **[!UICONTROL Calendar]**.

   Mer information om hur du skapar ett klisterfilter finns i [Lägga till ett klisterfilter](/help/using/usage/reports-customize/t-sticky-filter.md).

>[!TIP]
>
>Beroende på vilken typ av meddelande du visar kan rapporten variera.

## Meddelanden i appen {#section_90B79BA58E8141F78538C187EB1BF8C7}

Om du visar rapporter för ett meddelande i appen ser rapporten ut ungefär som på följande bild:

![rapportmeddelande](assets/report_message.png)

### Meddelandestatistik i appen

Här är en lista över de mätvärden som är tillgängliga för meddelanden i appen:

* **[!UICONTROL Impression]**, när ett meddelande utlöses.

* **[!UICONTROL Click through]**, när en användare trycker på  **[!UICONTROL Click Through]** knappen på ett varningsmeddelande eller helskärmsmeddelande och när en användare öppnar programmet från ett lokalt meddelande.

* **[!UICONTROL Cancel]** när en användare trycker på  **[!UICONTROL Cancel]** knappen på en varning eller ett helskärmsmeddelande.

* **[!UICONTROL Engagement Rate]**, ett beräknat mått från Adobe Analytics och är resultatet av antalet klickningar dividerat med antalet visningar.

## Push-meddelanden {#section_BEAFD858CA194185B6F88903446058E9}

Om du visar rapporter för ett push-meddelande ser rapporten ut ungefär som på följande bild:

![push-meddelande](assets/report_message_push.png)

Diagrammet överst visar antalet användare som öppnade meddelandet.

### Mätvärden för push-meddelanden

Här är en lista över de mätvärden som är tillgängliga för push-meddelanden:

* **[!UICONTROL Time]**

   Den tidpunkt då meddelandet skickades till enheter från Mobile Services.

* **[!UICONTROL Status]**

   Meddelandets status och tillgängliga statusvärden är:

   * **[!UICONTROL Cancelled]**
   * **[!UICONTROL Scheduled]**
   * **[!UICONTROL Executing]**
   * **[!UICONTROL Executed]**

* **[!UICONTROL Published]**

   Antalet enhetstoken som skickats till Apple Push Notification Service/Firebase Cloud Messaging (APNS/FCM) för att skicka meddelandet till användarenheterna.

* **[!UICONTROL Failed]**

   Antalet enhetstoken som inte kunde skickas till APNS/FCM. Några möjliga orsaker till fel:

   * Ett ogiltigt pushID

   * Den push-plattform (APNS, FCM o.s.v.) som gavs för att skicka till finns inte för jobbprogrammet. Plattformen kan till exempel samla in push-tokens för iOS, men har ingen APNS-tjänst konfigurerad.

   * Meddelandet kan ha misslyckats på grund av att push-tjänsten inte konfigurerats korrekt eller att Mobile Services-systemet är avstängt.
   >[!IMPORTANT]
   >
   >Om du har ett ovanligt stort antal fel kontrollerar du konfigurationen för push-tjänster. Om push-tjänster verkar vara rätt konfigurerade kontaktar du Adobe kundtjänst.

* **[!UICONTROL Blocklisted]**

   Antalet enhetstoken som inte längre är giltiga för att skickas till APNS eller FCM. Det innebär vanligtvis att programmet har avinstallerats från enheten eller att användaren har ändrat sina inställningar för att ta emot meddelanden. Android och iOS skiljer sig åt när variabler räknas som blocklist. Android-tokens visas omedelbart i antalet blockeringslista. iOS-tokens visas först som publicerade, men baserat på feedback från APNS visas som blocklist i efterföljande meddelanden.
