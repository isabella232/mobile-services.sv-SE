---
description: Följ de här stegen för att konfigurera en rapportserie för insamling av appdata från iOS.
solution: Experience Cloud Services,Analytics
title: Innan du börjar
topic-fix: Developer and implementation
uuid: 04133f68-3618-41fd-8a13-aec5b6f04df6
exl-id: 83da7cf5-3211-484d-bfe8-7b3b4999eea2
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# Innan du börjar {#before-you-start}

Följ de här stegen för att konfigurera en rapportserie för insamling av appdata från iOS.

## Rollspecifika uppgifter {#section_8B9EA1FA189F4C6DB7D829F0B5844FBC}

Analysadministratörer och apputvecklare måste utföra följande uppgifter:

### Analysadministratörer

Så här konfigurerar du en rapportserie och samlar in data om mobilappar:

1. Slutför ett av avsnitten i [Logga in på användargränssnittet för Mobile Services i Adobe](/help/ios/getting-started/getting-started.md).
1. Skapa ett Analytics-konto för varje apputvecklare.

Programutvecklare har nu tillgång till de rapportsviter du har skapat.

>[!IMPORTANT]
>
>Om du vill skapa en ny rapportsserie och hämta SDK:er måste du vara Analytics Administrator.

### Apputvecklare

1. Kontrollera att Analytics-administratören har slutfört stegen i *Analysadministratörer* ovan.

1. Verifiera att Analytics-administratören har slutfört ett av avsnitten i *Logga in på användargränssnittet för Mobile Services i Adobe* nedan.
1. När rapportsviten har konfigurerats utför du stegen i *Ladda ned SDK* nedan.

Mer information om roller och behörigheter finns i [Roller och behörigheter](/help/using/gs/c-mob-roles-and-permissions.md).

## Logga in på användargränssnittet för Mobile Services i Adobe {#section_690A2EC4572E47869F183974E932A6A8}

Adobe Mobile-tjänster är det primära rapporteringsgränssnittet för mobilappsanalys och målinriktning. När du har utfört de här stegen kan du hämta en konfigurationsfil som är förkonfigurerad med din datainsamlingsserver, rapportserie och många andra inställningar.

Du kan logga in på Adobe Mobile Services på något av följande sätt:

* **Experience Cloud**

   Logga in på [Experience Cloud](https://experience.adobe.com) med din Adobe ID.

   Den här metoden förutsätter att ditt företag har etablerats och att du har länkat ditt Analytics-konto. Mer information om etablering finns i [Hantera användare och produkter i Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/administration/admin-getting-started.html) i guiden Komponenter i Experience Cloud Central Interface. Mer information om hur du länkar ditt konto finns i [Organisationer i Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html).

   >[!TIP]
   >
   >Om du är osäker på om ditt företag har etablerats i Experience Cloud använder du ditt befintliga Adobe Analytics-konto.

* **Adobe Analytics**

   Klicka **[!UICONTROL Sign in with Analytics]** och ange företagsnamn, användarnamn och lösenord för Analytics.

## Skapa en rapportsvit {#section_7BC602ED1ABA42C6AB722F506B5219F3}

Så här skapar du en rapportserie för att samla in appdata och definiera en app:

1. Klicka på **[!UICONTROL Create New App]**.

   Om knappen inte visas klickar du på **[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**.

1. I **[!UICONTROL Report Suite]** nedrullningsbar meny, välja **[!UICONTROL New Report Suite]**.

1. Ange namnet på din app och välj ett unikt rapportsprogram-ID.

   Ett exempel på ett rapportsvits-ID är `mycomobileappdev`. Ni måste skapa separata rapportsviter och appar för utvecklings- och produktionsversionerna. När du är redo att konfigurera produktionsversionen upprepar du dessa steg.
1. Lämna **[!UICONTROL Mobile App Template]** markerat.

   Med den här mallen kan tidsstämplar samla in offlinedata och aktivera mobillösningens variabler för att hämta livscykelvärden.

1. Välj **[!UICONTROL Timezone]**, **[!UICONTROL Currency]** och klicka **[!UICONTROL Save]**.

## Ladda ned SDK {#section_044C17DF82BC4FD8A3E409C456CE9A46}

Så här hämtar du mobil-SDK:

1. Logga in på Mobile Services och öppna appen på något av följande sätt:

   * I **[!UICONTROL All Apps]** väljer du din app.
   * Leta reda på appen i den högra rutan och öppna den.

1. Klicka på **[!UICONTROL Manage App Settings]**.
1. I **[!UICONTROL App SDK Downloads]** avsnitt, bläddra till **[!UICONTROL App SDK Downloads]** -avsnitt.

1. Hämta SDK och exempelappen för din plattform.

>[!TIP]
>
>En konfigurationsfil för din app inkluderas automatiskt i SDK-nedladdningen, så du behöver inte hämta filen separat. Om du redan har laddat ned SDK och vill få uppdaterade inställningar hämtar du konfigurationsfilen igen.
