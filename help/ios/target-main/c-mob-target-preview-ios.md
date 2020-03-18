---
description: Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.
seo-description: Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.
seo-title: Förhandsvisa mål på iOS
title: Förhandsvisa mål på iOS
uuid: d92867a4-0569-4732-a928-28f9e2f8b21e
translation-type: tm+mt
source-git-commit: 06144a1695ac40ce984656491456968888f9e96e

---


# Förhandsvisa mål på iOS{#target-preview-on-ios}

Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.

Mer information om hur du konfigurerar och använder förhandsvisning av mål finns i [Målmobilförhandsvisning](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/target-mobile-preview.html).

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
      [ADBMobile targetPreviewRestartDeepLink:@" myapp://myhost"]; 
      ```
