---
description: Du måste slutföra de här åtgärderna innan du konfigurerar Push Messaging i program.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Krav för att aktivera push-meddelanden
topic-fix: Metrics
uuid: 194e6e07-b794-4152-a838-a4125c3292d4
exl-id: 543155a4-f687-48a6-8690-5c8da8490c62
source-git-commit: dbe3af75010fbf5195a3f93fc43cb696aaa32b65
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Krav för att aktivera push-meddelanden {#prerequisites-to-enable-push-messaging}

Du måste slutföra de här åtgärderna innan du konfigurerar push-meddelanden i dina program.

## Aktivera Experience Cloud för ditt företag

Ditt Adobe Analytics-företag måste vara Experience Cloud aktiverat. Du kan verifiera statusen för din kontoansvarige på Adobe.

## Installera och konfigurera Mobile SDK

* **Installera Mobile SDK**

   Om du vill konfigurera push-meddelanden måste du hämta och installera minst version 4.6 eller senare av Mobile SDK. Mer information finns i [Ladda ned SDK:er](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-analytics/download-sdk.md).

* **Konfigurera push-tjänster**

   Du måste konfigurera push-tjänster i Mobile SDK.

## Logga in på tjänsten Mobile Core med din Adobe ID

>[!IMPORTANT]
>
>För att kunna använda Push Services-funktionen måste användarna logga in på Mobile Core-tjänsten med hjälp av sina Adobe ID och deras Analytics-konto måste vara länkat till deras Adobe ID:n. Push Services-funktionen är inte tillgänglig om användare loggar in med sina befintliga Adobe Analytics-konton.

Om användarna inte har Adobe-ID:n utför du följande steg:

1. (**Experience Cloud Administrator**) Bjud in användare till Experience Cloud.

1. (**Användare**) Skapa en personlig Adobe ID med hjälp av instruktionerna från Experience Cloud-administratören.

   Ett e-postmeddelande skickas automatiskt till varje användare när administratören har slutfört det föregående steget.

1. (**Användare**) Logga in på Mobile med Adobe ID.

## Länka användarkonton i Experience Cloud

Varje användare måste länka Analytics-lösningskontot från Experience Cloud-organisationen.

1. Logga in på [Adobe Experience Cloud](https://experience.adobe.com) med en Adobe ID.

1. Välj företagsnamnet för Analytics i det övre högra hörnet.

1. Klicka **[!UICONTROL Add Organization]** och markera **[!UICONTROL Adobe SiteCatalyst/Adobe Social]** i listrutan.

1. Ange företagsnamnet, dina tidigare autentiseringsuppgifter för det angivna företaget och klicka på **[!UICONTROL Link Account]**.

   Adobe ID är nu länkat till ditt Analytics-konto, ditt företag och dina inloggningsuppgifter.

Mer information finns i [Organisationer i Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=sv) i guiden Komponenter i Experience Cloud Central Interface.

## Konfigurera push-tjänster och SDK ID-tjänsten i mobilanvändargränssnittet

Innan du aktiverar ID-tjänsten för din app kan du **[!UICONTROL Push Services]** -avsnittet är inaktiverat. Men när du har aktiverat ID-tjänsten aktiveras push-tjänsten. Mer information om hur du aktiverar push-tjänster finns i [Konfigurera alternativ för tjänsten SDK ID](/help/using/c-manage-app-settings/c-mob-confg-app/t-config-visitor.md).

>[!IMPORTANT]
>
>Du måste klicka **[!UICONTROL Save]** för att spara ändringarna och uppdatera push-tjänsterna.
>
>Du kan konfigurera en app för appbutiken för Apple och en för Google i varje rapportserie. Om du behöver ytterligare program, till exempel ett för en produktionsmiljö och ett för en utvecklingsmiljö, skapar du en ny app för appbutiken och en ny rapportsserie för varje miljö.

* För **Apple**, dra och släpp din privata nyckel och/eller ditt certifikat. Om din privata nyckel är lösenordskrypterad skriver du lösenordet.

   * För **Privat nyckel** drar och släpper du filen med den privata nyckeln i rutan.

      Du kan också klicka **[!UICONTROL Browse]** för att markera filen. Den här filen innehåller den privata nyckeln. Certifikatet kan också inkluderas i den här filen (`.p12`, `pkcs12`, `.pfx`, `.key`, `.pem`).

   * För **Lösenord för privat nyckel** Om filen med den privata nyckeln är krypterad anger du lösenordet.

      (Villkorligt) För **Certifikat** drar och släpper du certifikatfilen i rutan. Du kan också klicka **[!UICONTROL Browse]** för att markera filen. Det här fältet är inte obligatoriskt om filen för den privata nyckeln även innehåller certifikatet ( `.cert`, `.cer`, `.crt`, `.pem`).

* För **Google** anger du programmets API-nyckel.

   Klicka **[!UICONTROL Test]** för att verifiera att appen och mobiltjänsterna är korrekt konfigurerade. Det här alternativet är användbart för felsökning och felsökning.

   Skriv enhetens push-token som du vill skicka meddelandet. Du kan skicka meddelandet till flera enheter genom att ange variabler i en kommaseparerad lista.

   ![push test message](assets/push_test_list.png)
