---
description: Här är en lista över de Audience Manager-metoder som finns i Android-biblioteket.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud,Analytics
title: Audience Manager-metoder
topic-fix: Developer and implementation
uuid: 2f6e4664-1306-41d4-9fa7-e3a99f1df4ab
exl-id: 707b40b8-e56e-4c26-8b59-87c5d71cad0c
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 27%

---

# Audience Manager-metoder{#audience-manager-methods}

Här är en lista över de Audience Manager-metoder som finns i Android-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna är prefasta enligt lösningen. Experience Cloud ID-metoder har till exempel prefixet `audience manager`.

Om Audience Manager är konfigurerat i JSON-filen skickas en signal som innehåller livscykelvärden med en träff i livscykeln.

* **getVisitorProfile**

   Returnerar den besökarprofil som senast hämtades och, om ingen signal har skickats, returnerar `null`. Besökarprofilen sparas i `SharedPreferences` så att du enkelt kommer åt den när du startar appen flera gånger.

   * Här är syntaxen för den här metoden:

      ```java
      public static HashMap<String, Object> getVisitorProfile(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      HashMap<String, Object> visitorProfile = AudienceManager.getVisitorProfile(); 
      ```

* **getDpid**

   Returnerar aktuellt DPID.

   * Här är syntaxen för den här metoden:

      ```java
      public static void getDpid(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      String dpid = AudienceManager.getDpid(); 
      ```

* **getDpuuid**

   Returnerar aktuellt DPUID.

   * Här är syntaxen för den här metoden:

      ```java
      public static void getDpuuid(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      String dpuuid = AudienceManager.getDpuuid(); 
      ```

* **setDpidAndDpuuid**

   Anger DPID och DPUID, och dessa värden skickas med varje signal.

   Om det DPUID-värde som skickas till den här metoden innehåller tecken som inte är URL-säkra, måste kunderna koda parametern innan de skickar den till SDK.

   * Här är syntaxen för den här metoden:

      ```java
      public static void setDpidAndDpuuid(String dpid, String dpuuid); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      AudienceManager.setDpidAndDpuuid("myDpid", "myDpuuid"); 
      ```

* **signalWithData**

   Skickar målgruppshantering en signal med egenskaper och hämtar matchande segment som returneras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```java
      public static void signalWithData(Map<String, Object> data, AudienceManagerCallback<Map<String, Object>> callback);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      HashMap Traits = new HashMap<String, Object>();
      aamTraits.put("trait", "b");
      AudienceManager.signalWithData(aamTraits, new AudienceManager.AudienceManagerCallback<Map<String, Object>> () {
        @Override
         public void call(Map<String, Object> item) { 
              // segments come back here normally found in the segs object of your json 
         }
      });
      ```
