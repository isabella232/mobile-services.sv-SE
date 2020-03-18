---
description: Här är en lista över Audience Manager-metoder som finns i Android-biblioteket.
keywords: android;library;mobile;sdk
seo-description: Här är en lista över Audience Manager-metoder som finns i Android-biblioteket.
seo-title: Audience Manager-metoder
solution: Marketing Cloud,Analytics
title: Audience Manager-metoder
topic: Developer and implementation
uuid: 2f6e4664-1306-41d4-9fa7-e3a99f1df4ab
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Audience Manager-metoder{#audience-manager-methods}

Här är en lista över Audience Manager-metoder som finns i Android-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna är prefasta enligt lösningen. Experience Cloud ID-metoder har till exempel prefix `audience manager`.

Om Audience Manager är konfigurerat i JSON-filen skickas en signal som innehåller livscykelvärden med en träff i livscykeln.

* **getVisitorProfile**

   Returnerar den besökarprofil som senast hämtades och, om ingen signal har skickats, returneras `null`. Besökarprofilen sparas i `SharedPreferences` så att du enkelt kan komma åt den när du startar appen.

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

   Om det DPUID-värde som skickas till den här metoden innehåller tecken som inte är URL-säkra måste kunderna koda parametern innan de skickar den till SDK.

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
