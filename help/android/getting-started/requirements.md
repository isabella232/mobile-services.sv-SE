---
description: 'Slutför följande nödvändiga uppgifter innan du konfigurerar en rapportsserie och samlar in Android-appdata: '
solution: Experience Cloud,Analytics
title: Innan du börjar
topic-fix: Developer and implementation
uuid: 0ca9e937-8d40-4570-9dbf-9aecc6ecedf6
exl-id: e9c0fd94-b61d-4f56-97b8-f71aac096c93
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# Innan du börjar {#before-you-start}

Innan du konfigurerar en rapportserie och samlar in Android-appdata måste du utföra följande nödvändiga uppgifter:

## Rollspecifika uppgifter {#section_8B9EA1FA189F4C6DB7D829F0B5844FBC}

Analysadministratörer och apputvecklare måste utföra följande uppgifter:

### Analysadministratörer

Så här konfigurerar du en rapportserie och samlar in data om mobilappar:

1. Fyll i ett av avsnitten i [Logga in på användargränssnittet för Adobe Mobile Services](../getting-started/requirements.md#section_690A2EC4572E47869F183974E932A6A8).
1. Skapa ett Analytics-konto för varje apputvecklare.

Programutvecklare har nu tillgång till de rapportsviter du har skapat.

>[!IMPORTANT]
>
>Om du vill skapa en ny rapportsserie och hämta SDK:er måste du vara Analytics Administrator.

### Apputvecklare

1. Kontrollera att din Analytics-administratör har slutfört stegen i *Analysadministratörer* i [Rollspecifika uppgifter](../getting-started/requirements.md#section_8B9EA1FA189F4C6DB7D829F0B5844FBC).
1. Kontrollera att Analytics-administratören har slutfört ett av avsnitten i [Logga in på användargränssnittet för Adobe Mobile Services](../getting-started/requirements.md#section_690A2EC4572E47869F183974E932A6A8).
1. När rapportsviten har konfigurerats slutför du stegen i [Hämta SDK](../getting-started/requirements.md#section_044C17DF82BC4FD8A3E409C456CE9A46).

Mer information om roller och behörigheter finns i [Roller och behörigheter](/help/using/gs/c-mob-roles-and-permissions.md).

## Logga in på användargränssnittet för Adobe Mobile Services {#section_690A2EC4572E47869F183974E932A6A8}

Adobe mobiltjänster är det primära rapporteringsgränssnittet för mobilappsanalys och målinriktning. När du har utfört de här stegen kan du hämta en konfigurationsfil som är förkonfigurerad med din datainsamlingsserver, rapportserie och många andra inställningar.

Du kan logga in på användargränssnittet för Adobe Mobile Services på något av följande sätt:

### Experience Cloud

Logga in på [Experience Cloud](https://experiencecloud.adobe.com) med din Adobe ID. Den här metoden förutsätter att ditt företag har etablerats i Experience Cloud och att du har länkat ditt Analytics-konto. Mer information finns i [Hantera Experience Cloud-användare och -produkter](https://experienceleague.adobe.com/docs/core-services/interface/administration/admin-getting-started.html) i guiden Komponenter i Experience Cloud Central Interface.

>[!TIP]
>
>Om du är osäker på om ditt företag har etablerats i Experience Cloud använder du ditt befintliga Adobe Analytics-konto.

### Adobe Analytics

Klicka på **[!UICONTROL Sign in with Analytics]** och ange företagsnamnet för Analytics, ditt användarnamn och ditt lösenord.

## Skapa en rapportsvit {#section_7BC602ED1ABA42C6AB722F506B5219F3}

Så här skapar du en rapportserie för att samla in appdata och definiera en app:

1. Logga in på [Adobe Mobile Services](https://mobilemarketing.adobe.com).
1. Klicka på **[!UICONTROL Create an App]**.

   Om du inte ser den här knappen klickar du på **[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**.

1. Välj **[!UICONTROL New Report Suite]** i listrutan **[!UICONTROL Report Suite]**.

1. Ange namnet på appen och välj en rapporttyp.

   Ett exempel på ett rapportsvit-ID är `mycomobileappdev`. Du måste skapa separata rapportsviter och appar för utvecklings- och produktionsversionerna, så att du kan upprepa de här stegen när du är redo att konfigurera produktionsversionen.
1. Kontrollera att rapportsvitens namn visas i **[!UICONTROL Report Suite ID]**.
1. Kontrollera att **[!UICONTROL Mobile App Template]** är markerat i **[!UICONTROL Copy Settings From]**.

   Med den här mallen kan tidsstämplar samla in offlinedata och aktivera mobillösningens variabler för att hämta livscykelvärden.

1. Välj tidszon, valuta och klicka på **[!UICONTROL Save]**.

## Ladda ned SDK {#section_044C17DF82BC4FD8A3E409C456CE9A46}

Så här hämtar du mobil-SDK:

1. logga in på gränssnittet för mobila tjänster genom att skriva [https://mobilemarketing.adobe.com/](https://mobilemarketing.adobe.com/) i en webbläsare.
1. Klicka på listrutan **[!UICONTROL All Apps]** i den vänstra rutan och välj din app.
Du kan också välja din app i den högra rutan.

   >[!IMPORTANT]
   >
   >Om du vill visa din app i den högra rutan måste du först skapa en app. Mer information om hur du skapar ett program finns i [Lägg till ett nytt program](/help/using/manage-apps/t-new-app.md).

1. Klicka på **[!UICONTROL Manage App Settings]** i den vänstra rutan i appen.

   >[!IMPORTANT]
   >
   >Om du inte ser alternativet **[!UICONTROL Manage App Settings]** kontrollerar du att du är inloggad på Adobe Mobile Services. Verifiera genom att klicka på ikonen ![lösningsväljaren](assets/solution-switcher.png) längst upp till höger på sidan och se till att **[!UICONTROL Adobe Mobile Services]** visas längst upp till vänster.

1. Längst ned på sidan Hantera programinställningar hämtar du SDK och exempelappen för din plattform i **[!UICONTROL App SDK Downloads]**-avsnittet.

>[!TIP]
>
>En konfigurationsfil för din app inkluderas automatiskt i SDK-nedladdningen, så du behöver inte hämta filen separat. Om du redan har laddat ned SDK och vill få uppdaterade inställningar hämtar du konfigurationsfilen igen.

Om du använder Android Studio kan du även lägga till följande i programmets `build.gradle`-fil:

```java
compile 'com.adobe.mobile:adobeMobileLibrary:4.13.7'
```

Kom ihåg följande information:

* Ersätt versionsnumret i kodexemplet med rätt version av Android SDK:n.
* Hämta konfigurationsfilen och inkludera den i projektet.
