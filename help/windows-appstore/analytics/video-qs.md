---
description: Information som kan hjälpa dig med videoanalys.
seo-description: Information som kan hjälpa dig med videoanalys.
seo-title: Videoanalys
solution: Experience Cloud,Analytics
title: Videoanalys
topic-fix: Developer and implementation
uuid: 7d4e6668-a1d9-41da-96c8-8baac860c5b0
exl-id: 86d70a6f-db12-4f94-a37f-4b1d4b99e0f1
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 15%

---

# Videoanalys {#video-analytics}

Information som kan hjälpa dig med videoanalys.

Videomätning beskrivs i detalj i [Mäta ljud och video i Adobe Analytics](https://docs.adobe.com/content/help/sv-SE/media-analytics/using/media-overview.html/)-guiden. Den allmänna processen att mäta video är mycket lik på alla AppMeasurement-plattformar. Det här snabbstartsavsnittet innehåller en grundläggande översikt över utvecklaråtgärderna tillsammans med kodexempel.

I följande tabell visas de mediedata som skickas till Analytics. Använd bearbetningsregler för att mappa kontextdata till en Analytics-variabel.

* **a.media.name**

   (Obligatoriskt) Samlar in namnet på videon, enligt specifikationen i implementeringen, när en besökare visar videon på något sätt.Du kan lägga till klassificeringar för den här variabeln.

   (**Valfritt**) Custom Insight-variabeln innehåller information om videopassning.

   * Variabeltyp: eVar
   * Standardförfallodatum: Besök
   * Custom Insight (s.prop, används för videopappning)

* **a.media.name**

   (Valfritt) Innehåller information om videoavlyssning. ClientCare måste aktivera målning för den här variabeln.

   Händelsetyp: Custom Insight (s.prop)

   * Variabeltyp: Custom Insight (s.prop)

* **a.media.segment**

   (Obligatoriskt) Samlar in videosegmentdata, inklusive segmentnamnet och den ordning i vilken segmentet finns i videon. Den här variabeln fylls i genom att variabeln `segmentByMilestones` aktiveras när spelarhändelser spåras automatiskt, eller genom att ett anpassat segmentnamn anges när spelarhändelser spåras manuellt. När en besökare till exempel tittar på det första segmentet i en video kan SiteCatalyst samla in följande i eVar `1:M:0-25` segment.

   Standardmetoden för insamling av videodata samlar in data vid följande punkter:

   * videostart (spela upp)
   * segment
   * videoslut (stopp)

   Analyser är den första segmentvyn i början av segmentet när besökaren börjar titta. Efterföljande segmentvyer när segmentet börjar.

   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy


* **a.contentType**

   Samlar in data om den typ av innehåll som visas av en besökare. Träffar som skickas via videomätning tilldelas innehållstypen &quot;video&quot;. Den här variabeln behöver inte reserveras exklusivt för videospårning. Om du har en annan innehållstyp för innehållsrapporter som använder samma variabel kan du analysera hur besökarna distribueras över olika typer av innehåll. Du kan till exempel tagga andra innehållstyper med värden som &quot;artikel&quot; eller &quot;produktsida&quot; med den här variabeln. Från ett videomätningsperspektiv kan du med innehållstypen identifiera videobesökare och beräkna videokonverteringsgraden.

   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy

* **a.media.timePlay**

   Räknar den tid (i sekunder) som har ägnats åt att titta på en video sedan den senaste datainsamlingsprocessen (bildbegäran).

   * Variabeltyp: Händelse
   * Typ: Räknare

* **a.media.view**

   Anger att en besökare har visat en del av en video. Den ger dock ingen information om hur mycket, eller vilken del, av en video som besökaren visade.

   * Variabel: Händelse
   * Typ: Räknare

* **a.media.segmentView**

   Anger att en besökare har visat en del av ett videosegment. Den ger dock ingen information om hur mycket, eller vilken del, av en video som besökaren visade.

   * Variabeltyp: Händelse
   * Typ: Räknare

* **a .media.complete**

   Anger att en användare har visat en komplett video. Som standard mäts complete-händelsen en sekund före videons slut. Under implementeringen kan du ange hur många sekunder från slutet av videon som du vill att en vy ska vara slutförd. För livevideo och andra strömmar som inte har någon definierad ände kan du ange en anpassad punkt för att mäta slutförda data. Till exempel efter en viss tidpunkt.

   * Variabeltyp: Händelse
   * Typ: Räknare


## Konfigurera medieinställningar {#section_929945D4183C428AAF3B983EFD3E2500}

Konfigurera ett `MediaSettings`-objekt med de inställningar du vill använda för att spåra video:

```js
var mySettings = ADB.Media.settingsWith("name", 10, "playerName", "playerId");
```

## Spåra spelarhändelser {#section_C7F43AECBC0D425390F7FCDF3035B65D}

För att mäta videouppspelning måste metoderna `Play`, `Stop` och `Close` anropas vid rätt tidpunkt. Om spelaren exempelvis är pausad är `Stop`. `Play` anropas när uppspelningen startar eller återupptas.

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

## Mediemätningsklass och metodreferens {#section_50DF9359A7B14DF092634C8E913C77FE}

* **SettingsWith (winJS: settingsWith)**

   Returnerar ett `MediaSetting`-objekt med angivna parametrar.

   * Här är syntaxen för den här metoden:

      ```csharp
      static MediaSettings ^SettingsWith(Platform::String ^name, double length, Platform::String ^playerName, Platform::String ^playerID); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var mySettings = ADB.Media.settingsWith("name", 10, "playerName", "playerId"); 
      ```

* **AdSettingsWith (winJS: adSettingsWith**

   Returnerar ett `MediaSettings`-objekt som ska användas för att spåra en annonsvideo.

   * Här är syntaxen för den här metoden:

      ```csharp
      static MediaSettings ^AdSettingsWith(Platform::String ^name, double length, Platform::String ^playerName, Platform::String ^parentName, Platform::String ^parentPod, double parentPosition, Platform::String ^CPM); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var myAdSettings = ADB.Media.adSettingsWith("name", 10, "playerName", "parentName", "parentPod", 5, "myCPM"); 
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

   Spårar en mediestängning för medieobjektet *namn*.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Close(Platform::String ^name);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.close("mediaName");
      ```

* **Play (winJS: play)**

   Spårar en mediespelning för medieobjektet *`name`* vid angiven *offset* (i sekunder).

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Play(Platform::String ^name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.play("mediaName", 0);
      ```

* **Complete (winJS: complete)**

   Markera medieobjektet som slutfört manuellt vid *förskjutningen* som anges (i sekunder).

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Complete(Platform::String ^name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.complete("mediaName", 8); 
      ```

* **Stop (winJS: stop)**

   Meddelar mediemodulen att videon har stoppats eller pausats vid angiven *offset*.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Stop(Platform::String ^name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.stop("mediaName", 4);
      ```

* **Klicka (winJS: klicka)**

   Meddelar mediemodulen att någon har klickat på medieobjektet.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Click(Platform::String ^name, double offset);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.click("mediaName", 3);
      ```

* **Track (winJS: spår)**

   Skickar ett spåråtgärdsanrop (ingen sidvy) för det aktuella medieläget.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void Track(Platform::String ^name, Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^contextData);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADB.Media.track("mediaName", null);
      ```
