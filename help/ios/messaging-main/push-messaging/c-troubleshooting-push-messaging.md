---
description: Den här informationen hjälper dig att felsöka push-meddelanden.
keywords: mobil
solution: Experience Cloud,Analytics
title: Felsökning av push-meddelanden
topic-fix: Metrics
uuid: 87d7dcb6-82a8-46e3-a6ed-7f895a22f2af
exl-id: dda84d30-2a7b-496c-b8f3-3bd6b97076aa
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Felsöka push-meddelanden {#troubleshooting-push-messaging}

Den här informationen hjälper dig att felsöka push-meddelanden.

## Varför dröjer det ibland med att skicka push-meddelanden?

Följande typer av fördröjningar kan associeras med push-meddelanden för mobiltjänster:

* **Väntar på Analytics-träffar**

   Varje rapportsvit har en inställning som avgör när inkommande Analytics-träffar ska behandlas. Standardvärdet är 1 timme på timmen. Den faktiska bearbetningen av Analytics-träffar kan ta upp till 30 minuter, men är vanligtvis 15-20 minuter.

   En rapportserie träffar till exempel varje timme. Om du beräknar bearbetningstiden med högst 30 minuter kan det ta upp till 90 minuter innan en inkommande träff blir tillgänglig för ett push-meddelande. Om en användare startade appen kl. 9.01 visas träffen i gränssnittet för mobila tjänster som en ny unik användare mellan kl. 10.15 och kl. 10.30.

* **Väntar på push-tjänst**

   Det är inte säkert att push-tjänsten (APNS eller GCM) skickar ut meddelandet omedelbart. Även om det är ovanligt har vi sett en fördröjning på 5-10 minuter. På sidan Meddelanden kan du verifiera att push-meddelandet har skickats till push-tjänsten genom att klicka på länken Visa för meddelandet. I rapporten visas antalet lyckade skicka till push-tjänsten i kolumnen Publicerad.

   >[!TIP]
   >
   >Push-tjänsterna garanterar inte att ett meddelande skickas. Mer information om tjänsternas tillförlitlighet finns i lämplig dokumentation:
   >
   >* **APNS**:  [Tjänstekvalitet](https://developer.apple.com/documentation/usernotifications)
   >
   >* **GCM**:  [Meddelandets livstid](https://developers.google.com/cloud-messaging/concept-options)


## Hur förnyar jag mitt Apple Push Service-certifikat?

För att skicka push-meddelanden krävs ett giltigt push-tjänstcertifikat. Mobiltjänster meddelar dig när ditt certifikat snart upphör att gälla eller har gått ut. Om du får det här meddelandet följer du de här stegen för att förnya certifikatet:

1. Klicka på **[!UICONTROL Manage App Settings]**.
2. Om du vill ta bort det aktuella certifikatet bläddrar du till **[!UICONTROL Push Services]** och klickar på **[!UICONTROL Delete]**.
3. Konfigurera och testa ett nytt certifikat.

   Mer information finns i [Krav för att aktivera push-meddelanden](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/prerequisites-push-messaging.md)

4. Klicka på **[!UICONTROL Save]**.

## Varför kan jag inte se mina push-meddelanden i en iOS-simulator?

iOS-simulatorer stöder inte push-meddelanden.
