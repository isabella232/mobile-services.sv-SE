---
description: Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.
title: Förhandsvisa mål på iOS
uuid: d92867a4-0569-4732-a928-28f9e2f8b21e
exl-id: d5695156-59cd-42c5-b9a3-d8e0ebbb89d0
source-git-commit: d1ebb2bbc4742f5288f90a90e977d252f3f30aa3
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 12%

---

# Förhandsvisa mål på iOS{#target-preview-on-ios}

Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.

Mer information om hur du konfigurerar och använder Target Preview finns i [Target mobile preview](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/target-mobile-preview.html) i Adobe Target-dokumentationen.

>[!IMPORTANT]
>
>Om du vill använda Target Preview måste du ha SDK version 4.14.0 eller senare.

## Metoden Förhandsvisa mål

* **setPreviewRestartDeplink**

   Anger en appdeveplänk som utlöses när förhandsvisningsmarkeringar används i förhandsgranskningsläget.

   * Här är syntaxen för den här metoden:

      ```objective-c
       + (void) targetPreviewRestartDeepLink:(nullable NSString *)callbackURL;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile targetPreviewRestartDeepLink:@"myapp://myhost"]; 
      ```
