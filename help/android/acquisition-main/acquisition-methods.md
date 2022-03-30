---
description: 'Följande förvärvsmetoder tillhandahålls av Android-biblioteket '
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Förvärvsmetoder
topic-fix: Developer and implementation
uuid: 22ec432f-e7ae-4e89-be07-26206bbeacf8
exl-id: 0ce1b8fb-fd45-45de-8f97-e297e4c6529f
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 20%

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
