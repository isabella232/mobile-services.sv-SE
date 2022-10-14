---
description: Anskaffningsspårning måste vara aktiverat i SDK-konfigurationen innan du kan spåra och rapportera om marknadsföringslänkar.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Konfigurera värvning
topic-fix: Metrics
uuid: e996e43e-8a77-47a3-a6fb-53f676f92bef
exl-id: 3a12dfab-70d0-41e6-8d4e-5aba21bb8606
source-git-commit: dbe3af75010fbf5195a3f93fc43cb696aaa32b65
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Konfigurera värvning {#configure-acquisition}

Anskaffningsspårning måste vara aktiverat i SDK-konfigurationen innan du kan spåra och rapportera om marknadsföringslänkar.

1. Bläddra till sidan Hantera appinställningar för appen till **[!UICONTROL SDK Acquisition Options]** -avsnitt.
1. Utför följande uppgifter:

   * Om du vill aktivera förvärvet väljer du **[!UICONTROL Enable]** kryssruta.

      När du markerar den här kryssrutan visas **[!UICONTROL Referrer Timeout]** blir aktivt och värdet ändras från 0 till 5.

   * Ange ett värde i dialogrutan **[!UICONTROL Referrer Timeout (seconds)]** fält

      (**Valfritt**) Om du aktiverade **[!UICONTROL Enable]** är det här fältet valfritt. Du kan ändra timeout-värdet, som anges i sekunder. Den här inställningen anger väntetiden för förvärvsinformation innan den första starten skickas.
   >[!IMPORTANT]
   >Du måste ange ett värde som inte är noll. Om du aktiverar Anskaffning men låter värdet vara noll fungerar inte förvärvningslänkarna. Vi rekommenderar att du använder standardvärdet på 5 sekunder.

1. Hämta och använd den nya SDK-konfigurationsfilen i din app.

   Du har konfigurerat förvärvet på **iOS**.
