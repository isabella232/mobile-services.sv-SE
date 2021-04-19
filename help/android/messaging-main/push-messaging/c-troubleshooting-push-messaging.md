---
description: Den här informationen hjälper dig att felsöka push-meddelanden.
keywords: mobil
seo-description: Den här informationen hjälper dig att felsöka push-meddelanden.
seo-title: Felsök push-meddelanden
solution: Experience Cloud,Analytics
title: Felsök push-meddelanden
topic-fix: Metrics
uuid: 9c4a9371-6691-4a2c-a6c1-b9f901a41599
exl-id: 82b89f56-f43e-4b0d-80c5-5bff4013e5f7
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Felsöka push-meddelanden {#troubleshooting-push-messaging}

Den här informationen hjälper dig att felsöka push-meddelanden.

## Varför dröjer det ibland med att skicka push-meddelanden?

Följande typer av fördröjningar kan associeras med push-meddelanden för mobiltjänster:

* Väntar på Analytics-träffar

   Varje rapportsvit har en inställning som avgör när inkommande Analytics-träffar ska behandlas. Standardvärdet är 1 timme på timmen. Den faktiska bearbetningen av Analytics-träffar kan ta upp till 30 minuter, men är vanligtvis 15-20 minuter. En rapportserie träffar till exempel varje timme. Om du beräknar bearbetningstiden med högst 30 minuter kan det ta upp till 90 minuter innan en inkommande träff blir tillgänglig för ett push-meddelande. Om en användare startade appen kl. 9.01 visas träffen i gränssnittet för mobila tjänster som en ny unik användare mellan kl. 10.15 och kl. 10.30.

* Väntar på push-tjänst

   Push-tjänsten (APNS eller FCM) kanske inte skickar ut meddelandet omedelbart. Även om det är ovanligt har vi sett en fördröjning på 5-10 minuter. På sidan Meddelanden kan du verifiera att push-meddelandet har skickats till push-tjänsten genom att klicka på länken **[!UICONTROL View]** för meddelandet. I rapporten visas antalet lyckade skicka till push-tjänsten i kolumnen **[!UICONTROL Published]**.

   >[!TIP]
   >
   >Push-tjänsterna garanterar inte att ett meddelande kommer att skickas.

   Mer information om tjänsternas tillförlitlighet finns i lämplig dokumentation:

   * **APNS**:  [Tjänstekvalitet](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW5)
   * **FCM**:  [Meddelandets livstid](https://firebase.google.com/docs/cloud-messaging/concept-options#lifetime)

## Varför stängs mina push-meddelanden av eller utökas inte?

För vissa Android-enheter kan du behöva använda `NotificationCompat.BigTextStyle` när du visar meddelanden.
