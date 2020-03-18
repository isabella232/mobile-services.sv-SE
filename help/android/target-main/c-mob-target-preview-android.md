---
description: Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.
seo-description: Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.
seo-title: Förhandsvisa mål på Android
title: Förhandsvisa mål på Android
uuid: f3c82d64-009c-4929-a5e6-3677b2977889
translation-type: tm+mt
source-git-commit: 83e6968efb0ed1b4ef504286c6cb2e8e4d2eaf94

---


# Förhandsvisa mål på Android {#target-preview-on-android}

Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.

Mer information om hur du konfigurerar och använder Target Preview finns i [Target Mobile Preview](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/target-mobile-preview.html).

>[!IMPORTANT]
>
>Om du vill använda Target Preview måste du ha SDK version 4.14.0 eller senare.

* **setPreviewRestartDeplink**

   Anger en appdeveplänk som utlöses när förhandsvisningsmarkeringar används i förhandsgranskningsläget.

   * Här är syntaxen för den här metoden:

      ```java
      public static void setPreviewRestartDeeplink(String deeplink);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Target.setPreviewRestartDeeplink(“myapp://myhost”); 
      ```

