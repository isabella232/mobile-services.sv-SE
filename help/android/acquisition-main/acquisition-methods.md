---
description: 'Följande förvärvsmetoder tillhandahålls av Android-biblioteket '
keywords: android;library;mobile;sdk
seo-description: 'Följande förvärvsmetoder tillhandahålls av Android-biblioteket '
seo-title: Förvärvsmetoder
solution: Marketing Cloud,Analytics
title: Förvärvsmetoder
topic: Developer and implementation
uuid: 22ec432f-e7ae-4e89-be07-26206bbeacf8
translation-type: tm+mt
source-git-commit: bf076aa8e59d5c3e634fc4ae21f0de0d4541a83f

---


# Anskaffningsmetoder{#acquisition-methods}

Följande förvärvsmetod tillhandahålls av Android-biblioteket:

* **campaignStartForApp**

   Tillåter utvecklare att starta en app-anskaffningskampanj som om användaren klickade på en länk. Detta är praktiskt när du vill skapa länkar för manuell hämtning och hantera omdirigering av appbutiken själv.

   * Här är syntaxen för den här metoden:

      ```java
      public static void campaignStartForApp(final String appId final Map<String Object> data); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Acquisition.campaignStartForApp("0652024f-adcd-49f9-9bd7-2552a4564d2f" new 
      HashMap<String Object (){{
           put("custom.key" "value");
      }}); 
      ```
