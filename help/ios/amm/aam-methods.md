---
description: Här är en lista över Audience Manager-metoder som finns i iOS-biblioteket.
seo-description: Här är en lista över Audience Manager-metoder som finns i iOS-biblioteket.
seo-title: Audience Manager-metoder
solution: Marketing Cloud,Analytics
title: Audience Manager-metoder
topic: Developer and implementation
uuid: 97658bd6-4c4f-4875-abe9-36dad4ec8bae
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Audience Manager-metoder {#audience-manager-methods}

Här är en lista över Audience Manager-metoder som finns i iOS-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna prefixas enligt lösningen och Audience Manager-metoderna prefixas med &quot; `audience`&quot;.

Om Audience Manager är konfigurerat i JSON-filen skickas en signal som innehåller livscykelvärden med `application:didFinishLaunchingWithOptions:`.

* **publikVisitorProfil**

   Returnerar den besökarprofil som senast hämtades och, om ingen signal har skickats, returneras `null`. Besökarprofilen sparas i `NSUserDefaults` så att du enkelt kan komma åt den när du startar appen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (NSDictionary *) audienceVisitorProfile;
      ```

   * Här är kodexemplet för den här menyn:

      ```objective-c
      NSDictionary *profile = [ADBMobile audienceVisitorProfile]; 
      ```

* **audiensDpid**

   Returnerar aktuellt DPID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(NSString *) audience Dpid;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *currentDpid = [ADBMobileaudience Dpid]; 
      ```

* **audiensDpuuid**

   Returnerar aktuellt DPUID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(NSString *) audienceDpuuid;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *currentDpuuid = [ADBMobileaudience Dpuuid]; 
      ```

* **auditionSetDpid: &#x200B; dpuuid:**

   Anger DPID och DPUID. När det är inställt läggs båda till för varje signal.

   * Data Provider-ID ( **Data Provider ID)** är det data partner-ID som tilldelas av Audience Manager.
   * Dataleverantörens unika användar-ID (DPUUID) **är** dataleverantörens unika ID för användaren.

      >[!IMPORTANT]
      >
      >Före version 4.13.x kodades DPUID inte automatiskt. Från och med version 4.13.x avkodar SDK först det värde som skickades och kodar sedan om det här värdet. Denna process säkerställer att SDK inte bryter bakåtkompatibiliteten.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) audienceSetDpid: (NSString*)   
                      dpiddpuuid:(NSString*)dpuuid;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-
      [ADBMobile audienceSetDpid:@"290"
                        dpuuid:@"99301393920493"];
      ```

* **audiensReset**

   Återställer Audience Manager UUID och tömmer den aktuella besökarprofilen.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(void) audienceReset;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile audienceReset]; 
      ```

* **auditionSignalWithData: &#x200B; callback:**

   Skickar målgruppshantering en signal med egenskaper och hämtar matchande segment som returneras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) audienceSignalWithData:(NSDictionary*)data
                            callback:(void(^)(NSDictionary
      *response))callback; 
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile audienceSignalWithData:traits
                               callback:^(NSDictionary*response){
                                 //do something with returned segments
                               }];
      ```

## Exempel

```objective-c
// setup your traits dictionary 
NSDictionary *traits = @{@"trait":@"b"}; 
// submit your signal and take action on results 
[ADBMobile audienceSignalWithData:traits  
                         callback:^(NSDictionary *response) { 
                             // do something with visitor segments here 
                             if ([response[@"gender"] isEqualToString:@"male"]) { 
                             // do something with gender  
                             } 
                         }];
```
