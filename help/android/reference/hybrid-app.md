---
description: Om appen öppnar mobilt webbinnehåll måste besökarna inte identifieras separat när de förflyttar sig mellan den inbyggda och mobila webben.
seo-description: Om appen öppnar mobilt webbinnehåll måste besökarna inte identifieras separat när de förflyttar sig mellan den inbyggda och mobila webben.
seo-title: Spårning av besökare mellan en app och en mobil webbsajt
solution: Experience Cloud,Analytics
title: Spårning av besökare mellan en app och en mobil webbsajt
topic-fix: Developer and implementation
uuid: 073572e4-4c55-4b27-b4a7-e4349ccde7bf
exl-id: 7ca98572-138d-48f8-aa2a-d376eebb0b2c
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Spårning av besökare mellan en app och den mobila webben {#visitor-tracking-between-an-app-and-mobile-web}

Om appen öppnar mobilt webbinnehåll måste besökarna inte identifieras separat när de förflyttar sig mellan den inbyggda och mobila webben.

## Besökar-ID:n i appar

Android SDK genererar ett unikt besökar-ID när ett program installeras. Detta ID lagras i beständigt minne på den mobila enheten, skickas med varje träff och tas endast bort när användaren avinstallerar programmet.

>[!TIP]
>
>Besökar-ID:n för appar bevaras genom uppgraderingar.

## Besökar-ID:n på den mobila webben

Vanliga mobilwebbimplementeringar använder samma standardanalys `s_code.js` eller `AppMeasurement.js` som används på skrivbordsplatser. JavaScript-biblioteken har egna metoder för att generera unika besökar-ID:n, vilket gör att ett annat besökar-ID genereras när du öppnar mobilt webbinnehåll från din app.

## Implementera besöksspårning mellan en app och den mobila webben {#section_1755BCCFD42D456EB2319141030FDDFF}

Så här använder du samma besökar-ID i appen och på mobilwebben:

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i IntelliJ IDEA- eller Eclipse-projektet* i [Core-implementering och livscykel](/help/android/getting-started/dev-qs.md).

1. Om du vill lägga till besökarinformation till den URL som används för att öppna webbvyn ringer du `visitorAppendToURL`:

   ```java
   String urlString = "https://www.mydomain.com/index.php"; 
   String urlStringWithVisitorData = Visitor.appendToURL(urlString); 
   Intent browserIntent = new Intent(Intent.ACTION_VIEW, Uri.parse(urlStringWithVisitorData)); 
   startActivity(browserIntent);
   ```

   Alternativt kan du från och med SDK version 4.16.0 anropa `Visitor.getUrlVariablesAsync` och generera en egen URL:

   ```java
   final String urlString = "https://www.mydomain.com/index.php"; 
   Visitor.getUrlVariablesAsync(new Visitor.VisitorCallback(){ 
       @Override 
       public void call(String urlVariables) { 
           final String urlStringWithVisitorData = String.format("%s?%s", urlString, urlVariables); 
           final Intent browserIntent = new Intent(Intent.ACTION_VIEW, Uri.parse(urlStringWithVisitorData)); 
           startActivity(browserIntent); 
       } 
   });
   ```

ID-tjänstkoden på måldomänen extraherar MID från URL:en i stället för att skicka en begäran till Adobe om ett nytt ID. Koden använder det MID som skickas för att spåra besökaren.

Kontrollera att parametern `mid` finns för varje träff på träffar från det mobila webbinnehållet och att det här värdet matchar parametern `mid` som skickas av programkoden.

## Felsöka besöksspårning {#section_9B641F8569E34A089C52AA28EA4C891D}

### Jag ser inte `Visitor.appendToURL`.

Kontrollera att Adobe SDK som paketeras i det överordnade programmet är version 4.12.0 eller senare.

**Jag ser inte Adobe ID:n i min URL.**

* Kontrollera följande:
   * URL-strängen som används för att öppna webbvyn genererades av `Visitor.appendToURL(urlString)`.
   * Adobe-ID:n är kodade.
Kontrollera att de ID:n som läggs till i den URL som öppnas genom att kontrollera att frågeparametern `adobe_mc` visas i URL:en.

### Min `mid` är inte identisk i min app med min webbvy.

* Kontrollera följande:

   * URL-strängen som används för att öppna webbvyn genererades av `Visitor.appendToURL(urlString)`.
   * URL-strängen innehåller Adobe-parametrar.

      Strängen ska innehålla `adobe_mc="SAMPLE_ID_DATA"` där `"SAMPLE_ID_DATA"` innehåller ID:n som genereras i Adobe Mobile SDK.
   * `VisitorAPI.js` är version 1.7.0 eller senare.

Om dessa felsökningssteg inte löser dina problem kan du kontakta Adobe Experience Care.

>[!IMPORTANT]
>
>Om du vill att Adobe ska kunna validera implementeringen måste du dela ett exempelprogram och den associerade platsen.
