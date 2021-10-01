---
description: Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.
title: Förhandsvisa mål på Android
uuid: f3c82d64-009c-4929-a5e6-3677b2977889
exl-id: 69103f3a-9521-4808-8ecd-7b960efca04d
source-git-commit: d1ebb2bbc4742f5288f90a90e977d252f3f30aa3
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 12%

---

# Förhandsvisa mål på Android {#target-preview-on-android}

Med Target Preview kan du enkelt utföra QA-åtgärder från början till slut för målaktiviteter och förhandsgranska dessa aktiviteter på enheten.

Mer information om hur du konfigurerar och använder förhandsvisning av mål finns i [Målmobilförhandsvisning](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/target-mobile-preview.html) i användarhandboken för Adobe Target.

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
      Target.setPreviewRestartDeeplink("myapp://myhost"); 
      ```
