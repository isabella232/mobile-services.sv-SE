---
description: 'Slutför följande nödvändiga uppgifter innan du konfigurerar en rapportsserie och samlar in Android-appdata: '
solution: Experience Cloud Services,Analytics
title: Innan du börjar
topic-fix: Developer and implementation
uuid: 0ca9e937-8d40-4570-9dbf-9aecc6ecedf6
exl-id: e9c0fd94-b61d-4f56-97b8-f71aac096c93
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
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

1. Slutför ett av avsnitten i [Logga in på användargränssnittet för Mobile Services i Adobe](../getting-started/requirements.md#section_690A2EC4572E47869F183974E932A6A8).
1. Skapa ett Analytics-konto för varje apputvecklare.

Programutvecklare har nu tillgång till de rapportsviter du har skapat.

>[!IMPORTANT]
>
>Om du vill skapa en ny rapportsserie och hämta SDK:er måste du vara Analytics Administrator.

### Apputvecklare

1. Kontrollera att Analytics-administratören har slutfört stegen i *Analysadministratörer* in [Rollspecifika uppgifter](../getting-started/requirements.md#section_8B9EA1FA189F4C6DB7D829F0B5844FBC).
1. Verifiera att Analytics-administratören har slutfört ett av avsnitten i [Logga in på användargränssnittet för Mobile Services i Adobe](../getting-started/requirements.md#section_690A2EC4572E47869F183974E932A6A8).
1. När rapportsviten har konfigurerats utför du stegen i [Ladda ned SDK](../getting-started/requirements.md#section_044C17DF82BC4FD8A3E409C456CE9A46).

Mer information om roller och behörigheter finns i [Roller och behörigheter](/help/using/gs/c-mob-roles-and-permissions.md).

## Logga in på användargränssnittet för Mobile Services i Adobe {#section_690A2EC4572E47869F183974E932A6A8}

Adobe Mobile-tjänster är det primära rapporteringsgränssnittet för mobilappsanalys och målinriktning. När du har utfört de här stegen kan du hämta en konfigurationsfil som är förkonfigurerad med din datainsamlingsserver, rapportserie och många andra inställningar.

Du kan logga in på användargränssnittet för Mobile-tjänster i Adobe på något av följande sätt:

### Experience Cloud

Logga in på [Experience Cloud](https://experiencecloud.adobe.com) med din Adobe ID. Den här metoden förutsätter att ditt företag har etablerats i Experience Cloud och att du har länkat ditt Analytics-konto. Mer information finns i [Hantera användare och produkter i Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/administration/admin-getting-started.html) i guiden Komponenter i Experience Cloud Central Interface.

>[!TIP]
>
>Om du är osäker på om ditt företag har etablerats i Experience Cloud använder du ditt befintliga Adobe Analytics-konto.

### Adobe Analytics

Klicka **[!UICONTROL Sign in with Analytics]** och ange företagsnamn, användarnamn och lösenord för Analytics.

## Skapa en rapportsvit {#section_7BC602ED1ABA42C6AB722F506B5219F3}

Så här skapar du en rapportserie för att samla in appdata och definiera en app:

1. Logga in på [Adobe Mobile Services](https://mobilemarketing.adobe.com).
1. Klicka på **[!UICONTROL Create an App]**.

   Om knappen inte visas klickar du på **[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**.

1. I **[!UICONTROL Report Suite]** nedrullningsbar meny, välja **[!UICONTROL New Report Suite]**.

1. Ange namnet på appen och välj en rapporttyp.

   Ett exempel på ett rapportsvits-ID är `mycomobileappdev`. Du måste skapa separata rapportsviter och appar för utvecklings- och produktionsversionerna, så att du kan upprepa de här stegen när du är redo att konfigurera produktionsversionen.
1. I **[!UICONTROL Report Suite ID]** kontrollerar du att rapportsvitens namn visas.
1. I **[!UICONTROL Copy Settings From]**, verifiera att **[!UICONTROL Mobile App Template]** är markerat.

   Med den här mallen kan tidsstämplar samla in offlinedata och aktivera mobillösningens variabler för att hämta livscykelvärden.

1. Välj tidszon, valuta och klicka på **[!UICONTROL Save]**.

## Ladda ned SDK {#section_044C17DF82BC4FD8A3E409C456CE9A46}

Så här hämtar du mobil-SDK:

1. logga in på användargränssnittet för Mobile Services genom att skriva [https://mobilemarketing.adobe.com/](https://mobilemarketing.adobe.com/) i en webbläsare.
1. Klicka på **[!UICONTROL All Apps]** och välj program.
Du kan också välja din app i den högra rutan.

   >[!IMPORTANT]
   >
   >Om du vill visa din app i den högra rutan måste du först skapa en app. Mer information om hur du skapar ett program finns i [Lägg till en ny app](/help/using/manage-apps/t-new-app.md).

1. Klicka i appen i den vänstra rutan på **[!UICONTROL Manage App Settings]**.

   >[!IMPORTANT]
   >
   >Om du inte ser **[!UICONTROL Manage App Settings]** kontrollerar du att du är inloggad på Adobe Mobile Services. Verifiera genom att klicka på ![lösningsväljare](assets/solution-switcher.png) ikonen längst upp till höger på sidan och kontrollera att **[!UICONTROL Adobe Mobile Services]** visas längst upp till vänster.

1. Längst ned på sidan Hantera appinställningar, i **[!UICONTROL App SDK Downloads]** hämtar du SDK och exempelappen för din plattform.

>[!TIP]
>
>En konfigurationsfil för din app inkluderas automatiskt i SDK-nedladdningen, så du behöver inte hämta filen separat. Om du redan har laddat ned SDK och vill få uppdaterade inställningar hämtar du konfigurationsfilen igen.

Om du använder Android Studio kan du även lägga till följande i appens `build.gradle` fil:

```java
compile 'com.adobe.mobile:adobeMobileLibrary:4.13.7'
```

Kom ihåg följande information:

* Ersätt versionsnumret i kodexemplet med rätt version av Android SDK:n.
* Hämta konfigurationsfilen och inkludera den i projektet.
