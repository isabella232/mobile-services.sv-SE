---
description: Du kan konfigurera appen så att den använder Apple Push Notification Service (APNS) eller Firebase Cloud Messaging (FCM).
keywords: mobil
seo-description: Du kan konfigurera appen så att den använder Apple Push Notification Service (APNS) eller Firebase Cloud Messaging (FCM).
seo-title: Konfigurera appen att använda APNS eller FCM
solution: Experience Cloud,Analytics
title: Konfigurera appen att använda APNS eller FCM
topic-fix: Metrics
uuid: fa411f2a-ba47-4499-bbe5-1aedef6b49ad
exl-id: 9064e1f3-f176-4699-b1e6-90f29e1af0d3
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 12%

---

# Konfigurera appen att använda APNS eller FCM{#configure-app-to-use-apns-or-fcm}

Du kan konfigurera appen så att den använder Apple Push Notification Service (APNS) eller Firebase Cloud Messaging (FCM).

## Android-appar {#section_41D304102CDF4586911EC1413AD35A10}

### Om FCM inte är aktiverat i din app

Så här konfigurerar du Android-appen så att den använder FCM i det här scenariot:

1. Gå till [https://firebase.google.com/](https://firebase.google.com/) och logga in med dina inloggningsuppgifter för Google Dev.

1. Klicka på **[!UICONTROL Get Started]** och välj **[!UICONTROL Add Project]**.

1. Ange ett projektnamn och om du väljer Google Analytics för Firebase-data klickar du i kryssrutan för att godkänna villkoren för kontrollant.

1. Klicka på **[!UICONTROL Create project]** och vänta tills projektet har skapats.

1. Klicka på det skapade projektet och **[!UICONTROL Project Overview]**-sidan för det skapade projektet ska visas. Klicka på knappen med Android-ikonen för att lägga till en Android-app i projektet.

1. Ange programpaketets namn, programmets smeknamn och signeringscertifikatet om det behövs.

1. Följ de ytterligare steg som föreslås i installationsguiden. När du har verifierat Firebase-konfigurationen genom att testa kommunikationen med Firebase-servrarna går du tillbaka till sidan **[!UICONTROL Project Overview]**.

1. Klicka på kugghjulsikonen till höger om knappen **[!UICONTROL Project Overview]** och klicka på **[!UICONTROL Project Settings]**.

1. Klicka på fliken **[!UICONTROL Cloud Messaging]**.

1. Kopiera **[!UICONTROL Legacy server key]** och **[!UICONTROL Sender ID]** för senare bruk.

   Exempel:

   ```
   - Legacy server key = AIzaSyC6FNgsCOpBL5eXhDvwf8979mWba6x7Roo
   ```

   ```
   - Sender ID = 835015092250
   ```

### Om FCM är aktiverat i din app

Så här konfigurerar du Android-appen så att den använder FCM i det här scenariot:

1. Gå till [https://firebase.google.com/](https://firebase.google.com/) och logga in med dina inloggningsuppgifter för Google Dev.

1. Klicka på **[!UICONTROL Get Started]**. Detta öppnar projektindexsidan. Hitta det Firebase-aktiverade projektet som är länkat till Android-appen och klicka på projektkortet.

1. **[!UICONTROL Project Overview]** för projektet ska sedan läsas in. Klicka på kugghjulsikonen till höger om knappen **[!UICONTROL Project Overview]** och klicka på **[!UICONTROL Project Settings]**.

1. Klicka på fliken **[!UICONTROL Cloud Messaging]**.

1. Kopiera **[!UICONTROL Legacy server key]** och **[!UICONTROL Sender ID]** för senare bruk.

   Exempel:

   ```
   - Legacy server key = AIzaSyC6FNgsCOpBL5eXhDvwf8979mWba6x7Roo
   ```

   ```
   - Sender ID = 835015092250
   ```



## iOS-appar {#section_2031DAB485FC4D2B9027E42AD90B294D}

Så här konfigurerar du din iOS-app att använda APNS:

1. Gå till [https://developer.apple.com/account](https://developer.apple.com/account) och logga in på ditt [Apple Developer-konto](https://developer.apple.com/account).
1. Under **[!UICONTROL iOS Apps]** väljer du **[!UICONTROL Identifiers]**.
1. Om du har ett program-ID konfigurerat för push går du till steg 11.
1. Tryck på knappen **[!UICONTROL +]** för att skapa ett nytt program-ID.
1. Skriv en beskrivning av program-ID.
1. Ange ett program-ID-suffix.

   >[!IMPORTANT]
   >
   >Om du vill ha stöd för push måste du använda ett explicit program-ID som **inte** använder ett jokertecken (till exempel `- com.tester.pushSample`).

1. Under **[!UICONTROL App Services]** markerar du rutan **[!UICONTROL Push Notifications]**.
1. Klicka på **[!UICONTROL Continue]**.
1. Klicka på **[!UICONTROL Submit]**.
1. Klicka på **[!UICONTROL Done]**.
1. Välj det app-ID som är konfigurerat att använda push-meddelanden i listan och klicka på **[!UICONTROL Edit]**.
1. Om du redan har skapat ett push-certifikat går du vidare till steg 15.
1. Rulla ned till **[!UICONTROL Push Notifications]** och klicka på rätt **[!UICONTROL Create Certificate...]**-knapp.

   Den knapp du klickar på beror på om du skapar ett certifikat för utveckling eller produktion.
1. Följ stegen på hur du skapar din CSR på Apples webbplats, överför CSR och genererar ditt certifikat.
1. Rulla ned till avsnittet **[!UICONTROL Push Notifications]** och hämta det SSL-certifikat som du nyss skapade.
1. Dubbelklicka på det hämtade certifikatet för att lägga till det i nyckelkedjan.

### SSL-certifikat och privata nycklar

Så här hämtar du ditt SSL-certifikat och din privata nyckel (APNS):

1. Öppna **[!UICONTROL Keychain Access]**.
1. Klicka på **[!UICONTROL My Certificates]** för att hitta rätt **[!UICONTROL iOS Push Services Certificate]** för din app och din miljö.

   Du kan identifiera rätt certifikat genom att matcha paket-ID:t och om det är Development eller Production.

1. Expandera certifikatet och kontrollera att det innehåller en privat nyckel.
1. Högerklicka på den privata nyckeln och välj **[!UICONTROL  Export " *`<name of key>`*]**.
1. Ange nödvändig information i dialogrutan och spara den nya `.p12`-filen.

   Du behöver inte ange något lösenord.

1. I **[!UICONTROL Private Key]** skriver du `.p12`-filen.
