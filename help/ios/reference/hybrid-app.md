---
description: Om appen öppnar mobilt webbinnehåll måste du se till att besökarna inte identifieras separat när de förflyttar sig mellan den inbyggda och mobila webben.
solution: Experience Cloud,Analytics
title: Spårning av besökare mellan en app och en mobil webbplats
topic-fix: Developer and implementation
uuid: 2d951de6-3954-4379-a4ff-99b9695b9869
exl-id: d8459d59-0edd-42c4-81b5-529b250accb4
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Spårning av besökare mellan en app och en mobil webbsajt  {#visitor-tracking-between-an-app-and-mobile-web}

Om appen öppnar mobilt webbinnehåll måste du se till att besökarna inte identifieras separat när de förflyttar sig mellan den inbyggda och mobila webben.

## Besökar-ID:n i appar

iOS SDK genererar ett unikt besökar-ID när en app installeras. Detta ID lagras i beständigt minne på den mobila enheten och skickas med varje träff. Detta ID tas bara bort när användaren avinstallerar programmet.

>[!TIP]
>
>Besökar-ID:n för appar bevaras genom uppgraderingar.

## Besökar-ID:n på den mobila webben

Vanliga mobilwebbimplementeringar använder samma standardanalys `s_code.js` eller `AppMeasurement.js` som används på skrivbordsplatser. JavaScript-biblioteken har egna metoder för att generera unika besökar-ID:n, vilket gör att ett annat besökar-ID genereras när du öppnar mobilt webbinnehåll från din app.

Om du vill använda samma besökar-ID i appen och på mobilwebben och skicka appbesökar-ID:t till mobilwebben i URL:en:

## Implementera besökarspårning mellan en app och en mobil webbsajt {#section_EDC91D6C67AD43999227707C2769C65D}

1. Lägg till biblioteket i ditt projekt och implementera livscykeln.

   Mer information finns i *Lägg till SDK- och konfigurationsfilen i ditt projekt* i [Core Implementation och Lifecycle](/help/ios/getting-started/dev-qs.md).
1. Om du vill lägga till besökarinformation till den URL som används för att öppna webbvyn ringer du `visitorAppendToURL`:

   ```objective-c
   NSURL *url = [NSURL URLWithString:@"https://www.mydomain.com/index.php"]; 
   NSURL *urlWithVisitorData = [ADBMobile visitorAppendToURL:url]; 
   [[UIApplication sharedApplication] openURL:urlWithVisitorData];
   ```

   Alternativt kan du från och med SDK version 4.16.0 anropa `visitorGetUrlVariablesAsync:` och generera en egen URL:

   ```objective-c
   NSString *urlString = @"https://www.mydomain.com/index.php"; 
   [ADBMobile visitorGetUrlVariablesAsync:^(NSString * _Nullable urlVariables) { 
       NSString *urlStringWithVisitorData = [NSString stringWithFormat:@"%@?%@", urlString, urlVariables]; 
       NSURL *urlWithVisitorData = [NSURL URLWithString:urlStringWithVisitorData]; 
       [[UIApplication sharedApplication] openURL:urlWithVisitorData options:@{} completionHandler:^(BOOL success) { 
           // handle openURL success 
       }]; 
   }];
   ```

ID-tjänstkoden på måldomänen extraherar MID från URL:en i stället för att skicka en begäran till Adobe om ett nytt ID. ID-tjänstkoden på målsidan använder det MID som skickades för att spåra besökaren.

På träffar från mobilwebbinnehållet kontrollerar du att parametern `mid` finns i varje träff och att det här värdet matchar `mid` som skickas av appkoden.

## Felsöka besöksspårning {#section_C070AE85E3CE4E9893FD4F40E73F2C92}

### Jag ser inte `[ADBMobile visitorAppendToURL:]`.

Kontrollera att Adobe SDK som paketeras i det överordnade programmet är version 4.12.0 eller senare.

### Jag ser inte Adobe ID:n i min URL.

Kontrollera följande:

* URL-strängen som används för att öppna webbvyn genererades av `[ADBMobile visitorAppendToURL:]`

* Adobe-ID:n är kodade.

   Kontrollera att ID:n har lagts till i den URL som öppnas genom att leta efter frågeparametern `adobe_mc`.

### Mitt &quot;mitt&quot; är inte identiskt i min app med min webbvy.*

Kontrollera följande:

* URL-strängen som används för att öppna webbvyn genererades av `[ADBMobile visitorAppendToURL:]`

   URL-strängen innehåller Adobe-parametrar.

   Strängen ska innehålla `adobe_mc="SAMPLE_ID_DATA"` där `"SAMPLE_ID_DATA"` innehåller ID:n som genereras i Adobe Mobile SDK.

* `VisitorAPI.js` är version 1.7.0 eller senare.

Om dessa felsökningssteg inte löser dina problem kan du kontakta Adobe Client Care; vara redo att dela ett exempelprogram och den tillhörande webbplatsen så att Adobe kan validera implementeringen.
