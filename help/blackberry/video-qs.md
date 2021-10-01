---
description: Den allmänna processen att mäta video är mycket lik på alla AppMeasurement-plattformar. I det här avsnittet finns en grundläggande översikt över utvecklaråtgärderna tillsammans med kodexempel.
title: Videoanalys
uuid: 0d2731f3-77a9-4db1-9a8c-1e56c212ecb4
exl-id: 90da1a9e-2faa-429c-969e-869ebedf08cc
source-git-commit: d1ebb2bbc4742f5288f90a90e977d252f3f30aa3
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 14%

---

# Videoanalys {#video-analytics}

Den allmänna processen att mäta video är mycket lik på alla AppMeasurement-plattformar. I det här avsnittet finns en grundläggande översikt över utvecklaråtgärderna tillsammans med kodexempel.

Mer information om videomätning finns i guiden [Mäta direktuppspelningsmedia i Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html).  I följande tabell visas de mediedata som skickas till Analytics. Använd bearbetningsregler för att mappa kontextdata i kolumnen Kontextdatavariabel till en Analytics-variabel enligt beskrivningen i kolumnen Variabeltyp.

## Mappa spelarhändelser till analysvariabler

* **a.media.name**

   (Obligatoriskt) Samlar in namnet på videon, enligt specifikationen i implementeringen, när en besökare visar videon på något sätt.Du kan lägga till klassificeringar för den här variabeln.

   **(Valfritt)** Variabeln Custom Insight innehåller information om videoavslut.

   * Variabelnamn: eVar
      * Standardförfallodatum: Besök
      * Custom Insight (s.prop, används för videopappning)

* **a.media.name**

   (**Valfritt**) Tillhandahåller information om videopassning. Det måste vara kundtjänst som aktiverat för den här variabeln.

   * Händelsetyp: Custom Insight (s.prop)
   * Custom Insight (s.prop)

* **a.media.segment**

   (**Obligatoriskt**) Samlar in videosegmentdata, inklusive segmentnamnet och den ordning i vilken segmentet finns i videon. Den här variabeln fylls i genom att variabeln `segmentByMilestones` aktiveras när spelarhändelser spåras automatiskt, eller genom att ett anpassat segmentnamn anges när spelarhändelser spåras manuellt.

   När en besökare till exempel tittar på det första segmentet i en video kan SiteCatalyst samla `1:M:0-25` i eVar Segment. Standardmetoden för insamling av videodata samlar in data vid start- (uppspelning), start- och slutpunkterna för video (stopp).

   Analyser är den första segmentvyn i början av segmentet när besökaren börjar titta. Efterföljande segmentvyer när segmentet börjar.

   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy

* **a.contentType**

   Samlar in data om den typ av innehåll som visas av en besökare. Träffar som skickas via videomätning tilldelas innehållstypen &quot;video&quot;. Den här variabeln behöver inte reserveras exklusivt för videospårning. Om du har en annan innehållstyp för innehållsrapporter som använder samma variabel kan du analysera hur besökarna distribueras över olika typer av innehåll. Du kan till exempel tagga andra innehållstyper med värden som &quot;artikel&quot; eller &quot;produktsida&quot; med den här variabeln. Från ett videomätningsperspektiv kan du med Content Type identifiera videobesökare och därmed beräkna videokonverteringsgraden.

   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy

* **a.media.timePlay**

   Räknar den tid (i sekunder) som har ägnats åt att titta på en video sedan den senaste datainsamlingsprocessen (bildbegäran).

   * Variabeltyp: Händelse
   * Typ: Räknare

* **a.media.view**

   Anger att en besökare har visat en del av en video. Den ger dock ingen information om hur mycket, eller vilken del, av en video som besökaren visade.

   * Variabeltyp: Händelse
   * Typ: Räknare

* **a.media.segmentView**

   Anger att en besökare har visat en del av ett videosegment. Den ger dock ingen information om hur mycket, eller vilken del, av en video som besökaren visade.

   * Variabeltyp: Händelse
   * Typ: Räknare

* **a .media.complete**

   Anger att en användare har visat en komplett video. Som standard mäts complete-händelsen en sekund före videons slut. Under implementeringen kan du ange hur många sekunder från slutet av videon som du vill att en vy ska vara slutförd. För livevideo och andra strömmar som inte har någon definierad ände kan du ange en anpassad punkt för att mäta slutförda data. Till exempel efter en viss tidpunkt.

   * Variabeltyp: Händelse
   * Typ: Räknare

## Spåra spelarhändelser {#section_C7F43AECBC0D425390F7FCDF3035B65D}

För att mäta videouppspelning måste metoderna `mediaPlay`, `mediaStop` och `mediaClose` anropas vid rätt tidpunkt. Om spelaren exempelvis är pausad är `mediaStop`. `mediaPlay` anropas när uppspelningen startar eller återupptas.

## Mediemätningsklass och metodreferens {#section_50DF9359A7B14DF092634C8E913C77FE}

* **open**

   Öppnar en video för spårning.

   * Här är syntaxen för den här metoden:

      ```cpp
      void open(QString name, double length, QString playerName, QString playerID = QString()); 
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
        ADBMediaAnalytics::sharedInstance()->open("name", 10.0, "playerName", "playerID"); 
      ```

* **openAd**

   Öppnar ett `MediaSettings`-objekt för spårning.

   * Här är syntaxen för den här metoden:

      ```cpp
      void openAd(QString name, double length, QString playerName, QString parentName, QString parentPod, double parentPodPosition, QString CPM); 
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMediaAnalytics::sharedInstance()->openAd("name", 10, "playerName", "parentName", "podName", 0, "CPM"); 
      ```

* **stäng**

   Stänger medieobjektet *`name`*.

   * Här är syntaxen för den här metoden:

      ```cpp
      void close(QString name);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMediaAnalytics::sharedInstance()->close("name");
      ```

* **play**

   Spelar upp medieobjektet *`name`* vid angiven *`offset`* (i sekunder).

   * Här är syntaxen för den här metoden:

      ```cpp
      void play(QString name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMediaAnalytics::sharedInstance()->play("name", 0); 
      ```

* **complete**

   Markera medieobjektet som slutfört manuellt på *`offset`* (i sekunder).

   * Här är syntaxen för den här metoden:

      ```cpp
      void complete(QString name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMediaAnalytics::sharedInstance()->complete("name", 0);
      ```

* **stop**

   Meddelar mediemodulen att videon har stoppats eller pausats vid angiven *offset*.

   * Här är syntaxen för den här metoden:

      ```cpp
      stop(QString name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMediaAnalytics::sharedInstance()->stop("name", 0);
      ```

* **klicka**

   Meddelar mediemodulen att någon har klickat på medieobjektet.

   * Här är syntaxen för den här metoden:

      ```cpp
      void click(QString name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMediaAnalytics::sharedInstance()->close("name", 0);
      ```

* **spår**

   Skickar ett spåråtgärdsanrop (ingen sidvy) för det aktuella medieläget.

   * Här är syntaxen för den här metoden:

      ```cpp
      track(QString name, QHash<QString, QString> additionalData = QHash<QString, QString>()); 
      ```

   * Här är kodexemplet för den här metoden:

      ```cpp
      ADBMediaAnalytics::sharedInstance()->track("name", null);
      ```
