---
description: Information som kan hjälpa dig med videoanalys.
seo-description: Information som kan hjälpa dig med videoanalys.
seo-title: Videoanalys
solution: Experience Cloud,Analytics
title: Videoanalys
topic: Developer and implementation
uuid: f45dac3b-cd2e-4fba-a3b2-c243640ecfa4
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 15%

---


# Videoanalys {#video-analytics}

Information som kan hjälpa dig med videoanalys.

Videomätning beskrivs i detalj i guiden [Mäta video och ljud i Adobe Analytics](https://docs.adobe.com/content/help/sv-SE/media-analytics/using/media-overview.html) . Den allmänna processen att mäta video är mycket lik på alla AppMeasurement-plattformar. Det här snabbstartsavsnittet innehåller en grundläggande översikt över utvecklaråtgärderna tillsammans med kodexempel.

I följande tabell visas de mediedata som skickas till Analytics. Använd bearbetningsregler för att mappa kontextdata till en Analytics-variabel.

* **a.media.name**

   (**Obligatoriskt**) Samlar in namnet på videon, enligt specifikationen i implementeringen, när en besökare visar videon på något sätt.Du kan lägga till klassificeringar för den här variabeln.

   (**Valfritt**) Custom Insight-variabeln innehåller information om videopappning.

   * Variabeltyp: eVar
   * Standardförfallodatum: Besök
   * Custom Insight (s.prop, används för videopappning)

* **a.media.name**

   (**Valfritt**) Innehåller information om videovägning. ClientCare måste aktivera målning för den här variabeln.

   * Händelsetyp: Custom Insight (s.prop).
   * Variabeltyp: Custom Insight (s.prop)

* **a.media.segment**

   (**Obligatoriskt**) Samlar in videosegmentdata, inklusive segmentnamnet och den ordning i vilken segmentet finns i videon.

   Den här variabeln fylls i genom att den aktiveras när spelarhändelser spåras automatiskt, eller genom att ett anpassat segmentnamn anges när spelarhändelser spåras manuellt. `segmentByMilestones` När en besökare till exempel tittar på det första segmentet i en video kan SiteCatalyst samla in följande i eVar `1:M:0-25` Segment.

   Standardmetoden för insamling av videodata samlar in data vid följande punkter: videostart (uppspelning), segmentstart och videoslut (stopp). Analyser är den första segmentvyn i början av segmentet när besökaren börjar titta. Efterföljande segmentvyer när segmentet börjar.

   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy

* **a.contentType**

   Samlar in data om den typ av innehåll som visas av en besökare. Träffar som skickas via videomätning tilldelas innehållstypen &quot;video&quot;. Den här variabeln behöver inte reserveras exklusivt för videospårning. Om du har en annan innehållstyp för innehållsrapporter som använder samma variabel kan du analysera hur besökarna distribueras över olika typer av innehåll. Du kan till exempel tagga andra innehållstyper med värden som &quot;artikel&quot; eller &quot;produktsida&quot; med den här variabeln.

   Från ett videomätningsperspektiv kan du med Content Type identifiera videobesökare och därmed beräkna videokonverteringsgraden.

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

## Konfigurera mediainställningar {#section_929945D4183C428AAF3B983EFD3E2500}

Konfigurera ett `MediaSettings` objekt med de inställningar som du vill använda för att spåra video:

```js
var mySettings = ADB.Media.settingsWith("name", 10, "playerName", "playerId");
```

## Spåra spelarhändelser {#section_C7F43AECBC0D425390F7FCDF3035B65D}

För att mäta videouppspelning måste metoderna `Play`, `Stop`och `Close` anropas vid rätt tidpunkt. När spelaren exempelvis pausas `Stop`. `Play` anropas när uppspelningen startar eller återupptas.

## Klasser {#section_16838332727348F990305C0C6B0D795C}

### Klass: MediaSettings

```
property Platform::String ^name; 
property Platform::String ^playerName; 
property Platform::String ^playerID; 
property double length; 
property Platform::String ^channel; 
property Platform::String ^milestones; 
property Platform::String ^offsetMilestones; 
property bool segmentByMilestones; 
property bool segmentByOffsetMilestones; 
property int trackSeconds; 
property int completeCloseOffsetThreshold; 
 
// MediaAnalytics Ad settings 
property Platform::String ^parentName; 
property Platform::String ^parentPod; 
property Platform::String ^CPM; 
property double parentPodPosition; 
property bool isMediaAd;
```

### Mediemätningsklass och metodreferens {#section_50DF9359A7B14DF092634C8E913C77FE}

* **SettingsWith (winJS: settingsWith)**

   Returnerar ett `MediaSettings` objekt med angivna parametrar.

   * Här är syntaxen för den här metoden:

      ```csharp
      static MediaSettings ^SettingsWith(Platform::String ^name,  double length, Platform::String ^playerName, Platform::String  ^playerID); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var  mySettings  =  ADB.Media.settingsWith("name", 10,  "playerName", "playerId"); 
      ```

* **AdSettingsWith (winJS: adSettingsWith)**

   Returnerar ett `MediaSettings` objekt som ska användas för att spåra en annonsvideo.

   * Här är syntaxen för den här metoden:

      ```csharp
      static MediaSettings ^AdSettingsWith(Platform::String ^name,  double length, Platform::String ^playerName, Platform::String  ^parentName, Platform::String ^parentPod, double parentPosition,  Platform::String ^CPM);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var  myAdSettings = ADB.Media.adSettingsWith("name", 10,  "playerName", "parentName", "parentPod", 5, "myCPM");
      ```

* **Open (winJS: öppna)**

   Spårar media som är öppna med inställningarna som anges i `settings`.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Open(MediaSettings ^settings);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.open(mySettings);
      ```

* **Close (winJS: stäng)**

   Spårar en mediestängning för mediaobjektet med namnet *`name`*.

   * Här är syntaxen för den här metoden:

      ```csharp
      static  void  Close(Platform::String  ^name);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.close("mediaName"); 
      ```

* **Play (winJS: play)**

   Spårar en mediespelning för mediaobjektet med namnet *`name`* vid den angivna *förskjutningen* (i sekunder).

   * Här är syntaxen för den här metoden:

      ```csharp
      static  void  Play(Platform::String ^name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.play("mediaName",  0);
      ```

* **Complete (winJS: complete)**

   Markera medieobjektet som slutfört manuellt vid den *angivna förskjutningen* (i sekunder).

   * Här är syntaxen för den här metoden:

      ```csharp
      static  void  Complete(Platform::String ^name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.complete("mediaName", 8);
      ```

* **Stop (winJS: stop)**

   Meddelar mediemodulen att videon har stoppats eller pausats vid den angivna *förskjutningen*.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Stop(Platform::String ^name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.stop("mediaName",  4);
      ```

* **Klicka (winJS: klicka)**

   Meddelar mediemodulen att någon har klickat på medieobjektet.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Click(Platform::String ^name, double  offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.click("mediaName",  3); 
      ```

* **Track (winJS: spår)**

   Skickar ett spåråtgärdsanrop (ingen sidvy) för det aktuella medieläget.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Track(Platform::String ^name, Windows::Foundation::Collections::IMap<Platform::String^,  Platform::Object> ^contextData); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.track("mediaName",  null);
      ```
