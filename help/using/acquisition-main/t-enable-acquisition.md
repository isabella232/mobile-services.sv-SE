---
description: Anskaffningsspårning måste vara aktiverat i SDK-konfigurationen innan du kan spåra och rapportera om marknadsföringslänkar.
keywords: mobil
solution: Experience Cloud,Analytics
title: Konfigurera värvning
topic-fix: Metrics
uuid: e996e43e-8a77-47a3-a6fb-53f676f92bef
exl-id: 3a12dfab-70d0-41e6-8d4e-5aba21bb8606
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Konfigurera värvning {#configure-acquisition}

Anskaffningsspårning måste vara aktiverat i SDK-konfigurationen innan du kan spåra och rapportera om marknadsföringslänkar.

1. Bläddra till avsnittet **[!UICONTROL SDK Acquisition Options]** på sidan Hantera appinställningar för programmet.
1. Utför följande uppgifter:

   * Markera kryssrutan **[!UICONTROL Enable]** om du vill aktivera förvärvet.

      När du markerar den här kryssrutan blir fältet **[!UICONTROL Referrer Timeout]** aktivt och värdet ändras från 0 till 5.

   * Ange ett värde i fältet **[!UICONTROL Referrer Timeout (seconds)]**

      (**Valfritt**) Om du har aktiverat kryssrutan **[!UICONTROL Enable]** är det här fältet valfritt. Du kan ändra timeout-värdet, som anges i sekunder. Den här inställningen anger väntetiden för förvärvsinformation innan den första starten skickas.
   >[!IMPORTANT]
   >Du måste ange ett värde som inte är noll. Om du aktiverar Anskaffning men låter värdet vara noll fungerar inte förvärvningslänkarna. Vi rekommenderar att du använder standardvärdet på 5 sekunder.

1. Hämta och använd den nya SDK-konfigurationsfilen i din app.

   Du har konfigurerat förvärvet på **iOS**.
Om du vill aktivera förvärv på **Android**, slutför du stegen i [Spåra mobilförvärv](/help/android/acquisition-main/acquisition.md).
