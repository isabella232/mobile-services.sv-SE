---
description: Ni kan definiera och konfigurera målgruppsalternativ för push-meddelanden, inklusive datumintervallalternativ, analyssegment och anpassade segment.
keywords: mobil
solution: Experience Cloud,Analytics
title: Målgrupper Definiera och konfigurera målgruppssegment för push-meddelanden
topic-fix: Metrics
uuid: efd410e7-3b6c-4cf4-a26f-b11688adc491
exl-id: d1062a76-2e72-4649-8497-58617a7a47cb
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# Målgrupp: push-meddelanden{#audience-define-and-configure-audience-segments-for-push-messages}

Ni kan definiera och konfigurera målgruppsalternativ för push-meddelanden, inklusive datumintervallalternativ, analyssegment och anpassade segment.

## Definiera målgruppssegment {#section_7C4D2393CF7441959FE2381A02867CAC}

När ett målgruppssegment för push-meddelanden skapas kan segmentet omfatta användare från en eller flera appar, eftersom rapportsviter eller virtuella rapportsviter kan innehålla data från en eller flera appar. Mer information om virtuella rapportsviter finns i [Virtuella rapportsviter](/help/using/manage-apps/c-mob-vrs.md).

I Adobe Mobile Services kan marknadsförarna bara pusha till en app per plattform. Om marknadsförarna försöker skicka till segment som innehåller användare från flera appar visas en varning om att om man fortsätter kan det leda till allvarliga push-fel och att användare blocklist. Om du får ett push-fel läser du *Lösa push-fel* i [Felsöka push-meddelanden](/help/using/in-app-messaging/t-create-push-message/c-schedule-push-message.md).

Information om hur du använder Audience Manager i segmentdefinitionen finns i [Audience Analytics](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html).

>[!IMPORTANT]
>
>Om appanvändare är blocklist kan marknadsförarna **aldrig** skicka push-meddelanden till de berörda användarna igen.

Om du väljer ett målgruppssegment som innehåller användare i flera appar kan du se följande varning:

![flera appnamn](assets/multiple_appname.png)

Appnamnet baseras på den parade nedåtversionen av appId, som automatiskt skickas till Adobe Analytics av Mobile Services SDK i formatet `<app name> <version number> (<bundle id>)`.

>[!TIP]
>
>Versionsnumret är valfritt.

Upp till 6 sifferuppsättningar för versionen och 5 sifferuppsättningar för paket-ID tas bort.

Exempel:

* `Bea[rd]cons 1.0 (123)` visas som  `Bea[rd]cons`
* `Bea[rd]cons 1.2 (1.2)` visas som  `Bea[rd]cons`
* `Bea[rd]cons 1.2.3.4.5.6.7 (1111)` visas som  `Bea[rd]cons .7`
* `Bea[rd]cons 1.2.3. (1.2.3.4.5.6)` visas som  `Bea[rd]cons (.6)`

Om du vill fortsätta skicka push-meddelandet till de angivna apparna markerar du kryssrutan **[!UICONTROL Yes, I want to proceed.]** och klickar på **[!UICONTROL Send]**.

## God praxis

Här är några tips att komma ihåg:

* **Undvik** att definiera virtuella rapportsviter för mobilappar som innehåller data från flera appar för att minska förvirringen.
* Använd ett unikt program-ID som en del av ett målgruppssegment **varje** gång du vill skicka ett push-meddelande.
Detta garanterar att push-meddelanden skickas till ett målgruppssegment som endast tillhör **en app.**

### Exempel

Här är några exempel som hjälper dig att förstå hur du definierar segment på rätt sätt:

**Gör**: Marketern tillhandahåller push-certifikat för iOS- och Android-versionerna av ett program, till exempel för Adobe Photoshop. Marknadsföraren kan skicka ett push-meddelande till ett användarsegment som sträcker sig över båda plattformarna.

**Gör inte**: Marknadsförarna tillhandahåller push-certifikat för iOS- och Android-versioner av ett program, till exempel för Adobe Photoshop. Om marknadsföraren skapar och push-ar till ett segment med *alla aktiva användare de senaste 30 dagarna*, får endast användare av Adobe Photoshop iOS- och Android-appen push-funktionen, och alla Adobe Illustrator iOS- och Android-appanvändare blocklist. Mer information finns i *Lösa push-meddelandefel* i [Troubleshooting Push Messaging](/help/using/in-app-messaging/t-create-push-message/c-troubleshooting-push-messaging.md).

## Konfigurera målgruppssegment {#section_A92C60885A30421B8150820EC1CCBF13}

1. Gå till målgruppssidan för ett nytt push-meddelande.

   Mer information finns i [Skapa ett push-meddelande](/help/using/in-app-messaging/t-create-push-message/t-create-push-message.md).

   Kom ihåg följande **viktig** information när du konfigurerar målgruppsalternativen:

   * **[!UICONTROL Estimated Opt-In Audience]** är det antal enheter som matchar Adobe Analytics-segmentet **och** antalet enheter som är anslutna.

      Du kan visa en uppskattning av antalet användare i dina valda segment som har valt att ta emot meddelanden och som kommer att ta emot push-meddelandet. Det totala antalet appanvändare visas under uppskattningen, oavsett anmälningsstatus.

   * **[!UICONTROL Total]** är antalet enheter som matchar Adobe Analytics-segmentet.

   * Push-meddelanden skickas till de enheter som ingår i ett definierat Adobe Analytics-segment **och** som har valt att skicka push-meddelanden.

      Det innebär att SDK har skickat värdet `True` för push-meddelandets Opt-In-var.

   * Även om enheten har en giltig enhetstoken skickas inte meddelandet till enheten, såvida inte Adobe Analytics har angett den valda flaggan.

   * Mer information om felsökning av push-meddelanden finns i:

      * [Push-meddelanden i iOS](/help/ios/messaging-main/push-messaging/push-messaging.md)
      * [Push-meddelanden i Android](/help/android/messaging-main/push-messaging/push-messaging.md)

2. Skriv information i följande fält:

   * **[!UICONTROL During The]**

      Skriv in tidsramen som ska användas för den beräknade målgruppen. Välj ett alternativ i listrutan **[!UICONTROL During The]**:

   * **[!UICONTROL Last]** Med kan du välja en relativ tidsram (t.ex. de senaste 7 dagarna, de senaste 30 dagarna eller de senaste 60 dagarna) från den tidpunkt då meddelandet schemaläggs att skickas.

      Om du t.ex. markerar de senaste 30 dagarna och schemalägger meddelandet att skickas den 31 oktober, är den beräknade målgruppen antalet användare som har valt att ta emot push-meddelanden 30 dagar före den 31 oktober.

   * **[!UICONTROL Static Range]** Med kan du välja ett statiskt intervall genom att välja start- och slutdatum för det uppskattade målgruppsintervallet.

      Om du i det föregående exemplet väljer ett datumintervall från 1 oktober till 15 oktober men schemalägger att meddelandet ska skickas 31 oktober, är den beräknade målgruppen det antal användare som har valt att ta emot push-meddelanden i det statiska datumintervall som du har angett (1 oktober till 15 oktober).

   * **[!UICONTROL Analytics Segments]**

      Markera ett befintligt Adobe Analytics-segment i listrutan. Mer information finns i [Segmentbyggaren](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) i Adobe Analytics-dokumentationen.

   * **[!UICONTROL Custom Segments]**

      Välj ett mått eller en variabel i listrutan (till exempel **[!UICONTROL Days Since Last Use]** eller **[!UICONTROL Point of Interest]**) och konfigurera filtret efter behov. Följande anpassade segment riktar sig till exempel till användare som har en mobiltelefon som kör iOS och som befinner sig i Kalifornien (USA).
   >[!IMPORTANT]
   >
   >Om du klickar på **[!UICONTROL And]** i **[!UICONTROL Create Audience]**-avsnittet visas en dialogruta som påminner dig om att alla program som visas **måste** har ett giltigt certifikat. Om du klickade på **[!UICONTROL Or]** visas standarddialogrutan. Mer information om giltiga certifikat och rapportsviter finns i [Virtuella rapportsviter](/help/using/manage-apps/c-mob-vrs.md).
