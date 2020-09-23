---
description: Anskaffningsspårning måste vara aktiverat i SDK-konfigurationen innan du kan spåra och rapportera om marknadsföringslänkar.
keywords: mobile
seo-description: Anskaffningsspårning måste vara aktiverat i SDK-konfigurationen innan du kan spåra och rapportera om marknadsföringslänkar.
seo-title: Konfigurera värvning
solution: Experience Cloud,Analytics
title: Konfigurera värvning
topic: Metrics
uuid: e996e43e-8a77-47a3-a6fb-53f676f92bef
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Konfigurera värvning {#configure-acquisition}

Anskaffningsspårning måste vara aktiverat i SDK-konfigurationen innan du kan spåra och rapportera om marknadsföringslänkar.

1. Bläddra till **[!UICONTROL SDK Acquisition Options]** avsnittet på sidan Hantera appinställningar för programmet.
1. Utför följande uppgifter:

   * Markera kryssrutan om du vill aktivera förvärvet **[!UICONTROL Enable]** .

      När du markerar den här kryssrutan blir **[!UICONTROL Referrer Timeout]** fältet aktivt och värdet ändras från 0 till 5.

   * Ange ett värde i **[!UICONTROL Referrer Timeout (seconds)]** fältet

      (**Valfritt**) Om du har aktiverat **[!UICONTROL Enable]** kryssrutan är det här fältet valfritt. Du kan ändra timeout-värdet, som anges i sekunder. Den här inställningen anger väntetiden för förvärvsinformation innan den första starten skickas.
   >[!IMPORTANT]
   >Du måste ange ett värde som inte är noll. Om du aktiverar Anskaffning men låter värdet vara noll fungerar inte förvärvningslänkarna. Vi rekommenderar att du använder standardvärdet på 5 sekunder.

1. Hämta och använd den nya SDK-konfigurationsfilen i din app.

   Du har konfigurerat värvning på **iOS**.
Om du vill aktivera förvärv på **Android** ska du slutföra stegen i [Spåra mobilförvärv](/help/android/acquisition-main/acquisition.md).
