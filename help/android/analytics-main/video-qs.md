---
description: Här är lite information om hur du mäter video på Android med videomätningslösningen.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Videoanalys
topic-fix: Developer and implementation
uuid: a137cc27-dc28-48c0-b08e-2ca17d2c7e1d
exl-id: 1b7f5523-767a-45e8-b2e7-ecf9984849e4
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 12%

---

# Videoanalys {#video-analytics}

Här är lite information om hur du mäter video på Android med videomätningslösningen.

>[!TIP]
>
>Under videouppspelning skickas vanliga&quot;hjärtslag&quot;-anrop till den här tjänsten för att mäta den tid som spelas upp. Dessa hjärtslagsanrop skickas var 10:e sekund, vilket resulterar i detaljerade videointeraktionsvärden och exaktare videoutfallsrapporter. Mer information om Adobe videomätningslösning finns i [Mäta direktuppspelningsmedia i Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html).

Den allmänna processen att mäta video är densamma på alla plattformar. Innehållet ger en översikt över utvecklaråtgärderna med kodexempel. I följande tabell visas de mediedata som skickas till Analytics. Bearbetningsregler används för att mappa kontextdata till en Analytics-variabel.

## Mappa spelarhändelser till analysvariabler {#section_E84987F878AB4A3A83AE700FEC4C9D4D}

* **a.media.name**
   * Variabeltyp: eVar
      * Standardförfallodatum: Besök
      * Custom Insight (s.prop, används för videopappning)
   * (**Obligatoriskt**) När en besökare tittar på videon på något sätt samlar den här kontextdatavariabeln in namnet på videon, enligt specifikationen i implementeringen. Du kan lägga till klassificeringar för den här variabeln.
   * (**Valfritt**) Custom Insight-variabeln innehåller information om videopappning.

* **a.media.name**
   * Variabeltyp: Custom Insight (s.prop)
   * (**Valfritt**) Innehåller information om videopappning.

      >[!IMPORTANT]
      >
      >Matchen måste aktiveras för den här variabeln av ExpCare.
   * Händelsetyp: Custom Insight (s.prop)

* **a.media.segment**
   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy
   * (**Obligatoriskt**) Samlar in videosegmentdata, inklusive segmentnamnet och den ordning i vilken segmentet finns i videon.

      Den här variabeln fylls i genom att aktivera `segmentByMilestones` variabel när spelarhändelser spåras automatiskt eller när du anger ett eget segmentnamn när du spårar spelarhändelser manuellt. När en besökare till exempel tittar på det första segmentet i en video kan SiteCatalyst samla in följande i eVar Segment: `1:M:0-25`.

      Standardmetoden för insamling av videodata samlar in data vid följande punkter:

      * videostart (spela upp)
      * segment
      * videoslut (stopp)

      Analyser är den första segmentvyn i början av segmentet när besökaren börjar titta. Efterföljande segmentvyer när segmentet börjar.


* **a.contentType**
   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy
   * Samlar in data om den typ av innehåll som visas av en besökare.

      Träffar som skickas via videomätning tilldelas innehållstypen `video`. Från videomätningsperspektiv **Innehållstyp** gör att du kan identifiera videobesökare och beräkna videokonverteringsgrader.

* **a.media.timePlay**
   * Variabeltyp: Händelse
   * Typ: Räknare
   * Räknar den tid (i sekunder) som har ägnats åt att titta på en video sedan den senaste datainsamlingsprocessen (bildbegäran).

* **a.media.view**
   * Variabeltyp: Händelse
   * Typ: Räknare
   * Anger att en besökare har visat en del av en video.

      Den ger dock ingen information om hur mycket, eller vilken del, av en video som besökaren visade.

* **a.media.segmentView**
   * Variabeltyp: Händelse
   * Typ: Räknare
   * Anger att en besökare har visat en del av ett videosegment.

      Den ger dock ingen information om hur mycket, eller vilken del, av en video som besökaren visade.

* **a .media.complete**
   * Variabeltyp: Händelse
   * Typ: Räknare
   * Anger att en användare har visat en komplett video.

      Som standard mäts complete-händelsen en sekund före videons slut. Under implementeringen kan du ange hur många sekunder från slutet av videon som du vill att en vy ska vara fullständig. För livevideo och andra strömmar som inte har någon definierad ände kan du ange en anpassad punkt för att mäta slutförda (till exempel efter en viss tidpunkt).


## Konfigurera mediainställningar {#section_929945D4183C428AAF3B983EFD3E2500}

Konfigurera en `MediaSettings` objekt med de inställningar som du vill använda för att spåra video:

```java
MediaSettings mySettings = Media.settingsWith("name", 10, "playerName", "playerId");
```

## Spåra spelarhändelser {#section_C7F43AECBC0D425390F7FCDF3035B65D}

Om du vill mäta videouppspelning väljer du `mediaPlay`, `mediaStop`och `mediaClose` metoderna måste anropas vid rätt tidpunkt. När spelaren pausas, till exempel, anropa `mediaStop`. `mediaPlay` anropas när uppspelningen startar eller återupptas.

## Klasser {#section_16838332727348F990305C0C6B0D795C}

**Klass: MediaSettings**

```java
public String name; 
public String playerName; 
public String playerID; 
public double length; 
public String channel; 
public String milestones; 
public String offsetMilestones; 
public boolean segmentByMilestones; 
public boolean segmentByOffsetMilestones; 
public int trackSeconds = 0; 
public int completeCloseOffsetThreshold = 1; 
 
// MediaAnalytics Ad settings 
public String parentName; 
public String parentPod; 
public String CPM; 
public double parentPodPosition; 
public boolean isMediaAd;
```

**Klass: MediaState**

```java
public Date openTime = new Date(); 
public String name; 
public String segment; 
public String playerName; 
public String mediaEvent; 
public int offsetMilestone; 
public int segmentNum; 
public int milestone; 
public double length; 
public double offset; 
public double percent; 
public double timePlayed; 
public double segmentLength; 
public boolean complete = false; 
public boolean clicked = false; 
public boolean ad; 
public boolean eventFirstTime;
```

## Klassen Media Measurement och metodreferens {#section_50DF9359A7B14DF092634C8E913C77FE}

Här är metoderna i klassen Media Measurement:

* **settingsWith**

   Returnerar ett `MediaSettings` objekt med angivna parametrar.

   * Här är syntaxen för den här metoden:

      ```java
      public static MediaSettings adSettingsWith(String name, double length, String playerName, String parentName, String parentPod, double parentPodPosition, String CPM);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      MediaSettingsmySettings = Media.settingsWith("name", 10, "playerName", "playerId");
      ```

* **adSettingsWith**

   Returnerar ett `MediaSettings` -objekt som används för att spåra en annonsvideo.
   * Här är syntaxen för den här metoden:

      ```java
      public static MediaSettings adSettingsWith(String name, double length, String playerName, String parentName, String parentPod, double parentPodPosition, String CPM);
      ```

* **open**

   Öppnar en `MediaSettings` objekt för spårning.

   * Här är syntaxen för den här metoden:

      ```java
      public static void open(MediaSettings settings, MediaCallback callback); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.open(mySettings, new Media.MediaCallback() { 
        @Override 
        public void call(Object item)
        {//  monitor  callback  if  you  want  to  be  notified  every  second  the  media  is  playing  }
        }); 
      ```

   * **stäng**

      Stänger mediaobjektet med namnet *name*.

      * Här är syntaxen för den här metoden:

      ```java
      public static void close(String name);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.close("name"); 
      ```


* **play**
   * Spelar upp medieobjektet med namnet *name* vid angiven *offset* på några sekunder.
   * Här är syntaxen för den här metoden:

      ```java
      publicstatic void play(String name, double offset); 
      ```

* **complete**

   Markera medieobjektet som slutfört manuellt på *offset* anges i sekunder.

   * Här är syntaxen för den här metoden:

      ```java
      public static void complete(String name, double offset); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.complete("name", 0); 
      ```

* **stop**

   Meddelar mediamodulen att videon har stoppats eller pausats vid den angivna *offset*.

   * Här är syntaxen för den här metoden:

      ```java
      public static void stop(String name, double offset); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.stop("name", 0);
      ```

* **klicka**

   Meddelar mediemodulen att någon har klickat på medieobjektet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void click(String name double offset); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.click("name", 0);
      ```

* **spår**

   Skickar ett spåråtgärdsanrop (ingen sidvy) för det aktuella medieläget.

   * Här är syntaxen för den här metoden:

      ```java
      publicstatic void track(String name, Map<String, Object> data); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Media.track("name", null); 
      ```
