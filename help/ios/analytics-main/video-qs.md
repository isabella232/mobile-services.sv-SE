---
description: Här är lite information om hur du mäter video på iOS med hjälp av videomätning i milstolpe.
solution: Experience Cloud,Analytics
title: Videoanalys
topic-fix: Developer and implementation
uuid: d75fa415-78f6-4f50-a563-76949f040138
exl-id: d4d11ca0-1280-49db-8983-5b6d83856482
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 13%

---

# Videoanalys {#video-analytics}

Här är lite information om hur du mäter video på iOS med hjälp av videomätning i milstolpe.

>[!TIP]
>
>Under videouppspelning skickas vanliga&quot;hjärtslag&quot;-anrop till den här tjänsten för att mäta den tid som spelas upp. Dessa hjärtslagsanrop skickas var 10:e sekund, vilket resulterar i detaljerade videointeraktionsvärden och exaktare videoutfallsrapporter. Mer information finns i [Mäta direktuppspelningsmedia i Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html).

Den allmänna processen att mäta video är mycket lik på alla plattformar. Innehållet ger en grundläggande översikt över utvecklaråtgärderna med kodexempel.

## Mappa spelarhändelser till analysvariabler {#section_E84987F878AB4A3A83AE700FEC4C9D4D}

I följande tabell visas de mediedata som skickas till Analytics. Använd bearbetningsregler för att mappa kontextdata till en Analytics-variabel.

* **a.media.name**

   (Obligatoriskt) Samlar in namnet på videon, enligt specifikationen i implementeringen, när en besökare tittar på videon på något sätt. Du kan lägga till klassificeringar för den här variabeln.

   (Valfritt) Custom Insight-variabeln innehåller information om videopappning.

   * Variabeltyp: eVar
   * Standardförfallodatum: Besök
   * Custom Insight (s.prop, används för videopappning)

* **a.media.name**

   (Valfritt) Innehåller information om videoavlyssning. Det måste vara kundtjänst som aktiverat för den här variabeln.

   * Variabeltyp: Custom Insight (s.prop)
   * Händelsetyp: Custom Insight (s.prop)

* **a.media.segment**

   (Obligatoriskt) Samlar in videosegmentdata, inklusive segmentnamnet och den ordning i vilken segmentet finns i videon. Den här variabeln fylls i genom att variabeln `segmentByMilestones` aktiveras när spelarhändelser spåras automatiskt, eller genom att ett anpassat segmentnamn anges när spelarhändelser spåras manuellt. När en besökare till exempel tittar på det första segmentet i en video kan SiteCatalyst samla in följande i eVar `1:M:0-25` Segment.

   Standardmetoden för insamling av videodata samlar in data vid följande punkter:

   * videostart (spela upp)
   * segment
   * videoslut (stopp)

   Analyser är den första segmentvyn i början av segmentet när besökaren börjar titta. Efterföljande segmentvyer när segmentet börjar.

   * Variabeltyp: eVar
   * Standardförfallodatum: Sidvy


* **a.contentType**

   Samlar in data om den typ av innehåll som visas av en besökare. Träffar som skickas via videomätning tilldelas innehållstypen `video`. Den här variabeln behöver inte reserveras exklusivt för videospårning. Genom att använda samma variabel när du har en annan innehållstyp för innehållsrapporter kan du analysera hur besökarna distribueras över olika typer av innehåll. Du kan till exempel tagga andra innehållstyper med värden som &quot;artikel&quot; eller &quot;produktsida&quot; med den här variabeln. Från ett videomätningsperspektiv kan du med Content Type identifiera videobesökare och beräkna videokonverteringsgrader.

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

* **a.media.complete**

   Anger att en användare har visat en komplett video. Som standard mäts complete-händelsen en sekund före videons slut. Under implementeringen kan du ange hur många sekunder från slutet av videon som du vill att en vy ska vara slutförd. För livevideo och andra strömmar som inte har någon definierad ände kan du ange en anpassad punkt för att mäta slutförandet, till exempel efter en viss tidpunkt.

   * Variabeltyp: Händelse
   * Typ: Räknare

## Konfigurera mediainställningar {#section_929945D4183C428AAF3B983EFD3E2500}

Konfigurera ett `ADBMediaSettings`-objekt med de inställningar du vill använda för att spåra video:

```objective-c
ADBMediaSettings *mediaSettings = [ADBMobile mediaCreateSettingsWithName:MEDIA_NAME  
length:MEDIA_LENGTH playerName:PLAYER_NAME playerID:PLAYER_ID]; 
 
// milestone tracking. Use either standard milestones (percentage of total length) 
// or offset milestones (seconds elapsed from the beginning of the video) 
mediaSettings.milestones = @"25,50,75"; 
mediaSettings.segmentByMilestones = YES; 
 
mediaSettings.offsetMilestones = @"60,120"; 
mediaSettings.segmentByOffsetMilestones = YES; 
 
// seconds tracking - sends a hit every x seconds 
mediaSettings.trackSeconds = 30; // sends a hit every 30 seconds 
 
// open the video 
[ADBMobile mediaOpenWithSettings:mediaSettings callback:nil]; 
 
// You are now ready to play the video, for example, [movieViewController.moviePlayer play]; 
// Note the mediaPlay, mediaStop and mediaClose methods are called in the 
// event handlers described in the next section
```

## Spåra spelarhändelser {#section_C7F43AECBC0D425390F7FCDF3035B65D}

För att mäta videouppspelning måste metoderna `mediaPlay`, `mediaStop` och `mediaClose` anropas vid rätt tidpunkt. Om spelaren exempelvis är pausad är `mediaStop`. `mediaPlay` anropas när uppspelningen startar eller återupptas.

I följande exempel visas hur du konfigurerar meddelanden och anropar mediemetoder för att mäta video:

```objective-c
// configure notifications for when the video is finished, and when the 
media playback state changes 
 
- (void) configureNotifications:(MPMoviePlayerController *) movieController { 
 [[NSNotificationCenter defaultCenter] 
  addObserver: self 
  selector: @selector(mediaFinishedCallback:) 
  name: MPMoviePlayerPlaybackDidFinishNotification 
  object: movieController]; 
  
 [[NSNotificationCenter defaultCenter] 
  addObserver: self 
  selector: @selector(mediaPlaybackChangedCallback:) 
  name: MPMoviePlayerPlaybackStateDidChangeNotification 
  object: movieController]; 
} 
 
// define your notification callbacks. 
 
- (void) mediaFinishedCallback: (NSNotification*) notification { [ADBMobile mediaClose:MEDIA_NAME];} 
 
- (void) mediaPlaybackChangedCallback: (NSNotification*) notification { 
 MPMoviePlayerController *mediaController = notification.object; 
 if (mediaController.playbackState == MPMoviePlaybackStatePlaying) { 
  [ADBMobile mediaPlay:MEDIA_NAME offset: isnan(mediaController.currentPlaybackTime) ? 0.0 : mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateSeekingBackward) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateSeekingForward) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStatePaused) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateInterrupted) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateStopped) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
}
```

## Klasser {#section_16838332727348F990305C0C6B0D795C}

### Klass: ADBMediaSettings

```objective-c
bool segmentByMilestones; 
bool segmentByOffsetMilestones; 
double length; 
NSString *channel; 
NSString *name; 
NSString *playerName; 
NSString *playerID; 
NSString *milestones; 
NSString *offsetMilestones; 
NSUInteger trackSeconds; 
NSUInteger completeCloseOffsetThreshold; 
// settings used for ad tracking. For  
bool isMediaAd; 
double parentPodPosition; 
NSString *CPM; 
NSString *parentName; 
NSString *parentPod; 
```

### Klass: ADBMediaState

```objective-c
bool ad; 
bool clicked; 
bool complete; 
bool eventFirstTime; 
double length; 
double offset; 
double percent; 
double segmentLength; 
double timePlayed; 
double timePlayedSinceTrack; 
double timestamp; 
NSDate *openTime  
NSString *name 
NSString *playerName 
NSString *mediaEvent 
NSString *segment 
NSUInteger milestone 
NSUInteger offsetMilestone 
NSUInteger segmentNum 
NSUInteger eventType
```

## Mediemätningsklass och metodreferens {#section_50DF9359A7B14DF092634C8E913C77FE}

* **mediaCreateSettings &#x200B; WithName: &#x200B; length: &#x200B; playerName: &#x200B; playerID:**

   Returnerar ett `ADBMediaSettings`-objekt med angivna parametrar.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(ADBMediaSettings *) mediaCreateSettingsWithName:(NSString *)name
                                                 length:(double)length
                                              playerName:(NSString *)playerName
                                               playerID:(NSString *)playerID;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBMediaSettings *myCatSettings =
            [ADBMobile mediaCreateSettingsWithName:@"catVideo"                                               length:85
                                        playerName:@"catVideoPlayer"
                                          playerID:@"catPlayerId"]; 
      ```

* **mediaAdCreateSettings &#x200B; WithName: &#x200B; length: &#x200B; playerName: &#x200B; parentName: &#x200B; parentPod: &#x200B; parentPodPosition: &#x200B; CPM:**

   Returnerar ett `ADBMediaSettings`-objekt som ska användas för att spåra en annonsvideo.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (ADBMediaSettings *) mediaAdCreateSettingsWithName:(NSString *)name
                                                    length:(double)length   
                                                playerName:(NSString *)playerName
                                                parentName:(NSString *)parentName
                                                 parentPod:(NSString *)parentPod
                                        parentPodPosition:(double)parentPodPosition
                                                      CPM:(NSString *)CPM; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
        ADBMediaSettings *mySettings = 
             [ADBMobile mediaAdCreateSettingsWithName:@"ad"                                       length:30
                                           playerName:@"adPlayer"
                                           parentName:@"catVideo"
                                           parentPod:@"catCollection"
                                           parentPodPosition:2
                                                        CPM:nil];
      ```

* **mediaOpenWithSettings: &#x200B; callback:**

   Öppnar ett `ADBMediaSettings`-objekt för spårning.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) mediaOpenWithSettings:(ADBMediaSettings *)settings
                            callback:(void (^)(ADBMediaState *mediaState))callback; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile mediaOpenWithSettings:mySettings callback:^(ADBMediaState *mediaState) {
           // do something with media state if you want}];
      ```

* **mediaClose:**

   Stänger medieobjektet *namn*.

   * Här är syntaxen för den här metoden:

      ```objective-c
       + (void) mediaClose:(NSString *)name; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile mediaClose:@"kittiesPlaying"];
      ```

* **mediaPlay: &#x200B; förskjutning:**

   Spelar upp medieobjektet *name* vid angiven *offset* (i sekunder).

   * Här är syntaxen för den här metoden:

      ```objective-c
       + (void) mediaPlay:(NSString *)name offset:(double)offset;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile mediaPlay:@"cats" offset:25];
      ```

* **mediaComplete: &#x200B; offset:**

   Markera medieobjektet som slutfört manuellt vid *förskjutningen* som anges (i sekunder).

   * Här är syntaxen för den här metoden:

      ```objective-c
       + (void) mediaComplete:(NSString *)name offset:(double)offset;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
       [ADBMobile mediaComplete:@"meowzah" offset:90]; 
      ```

* **mediaStop: &#x200B; offset:**

   Meddelar mediemodulen att videon har stoppats eller pausats vid angiven *offset*.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) mediaStop:(NSString *)name offset:(double)offset; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile mediaStop:@"toonses" offset:30]; 
      ```

* **mediaClick: &#x200B; förskjutning:**

   Meddelar mediemodulen att någon har klickat på medieobjektet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) mediaClick:(NSString *)name offset:(double)offset;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile mediaClick:@"soManyCats" offset:47];
      ```

* **mediaTrack: &#x200B; withData:**

   Skickar ett spåråtgärdsanrop (ingen sidvy) för det aktuella medieläget.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) mediaTrack:(NSString *)name withData:(NSDictionary *)data;
      ```
