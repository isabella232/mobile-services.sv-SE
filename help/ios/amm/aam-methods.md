---
description: Här är en lista över de Audience Manager-metoder som finns i iOS bibliotek.
solution: Experience Cloud Services,Analytics
title: Audience Manager-metoder
topic-fix: Developer and implementation
uuid: 97658bd6-4c4f-4875-abe9-36dad4ec8bae
exl-id: b843a52f-2b83-4e19-9f43-895bd582d4ef
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 24%

---

# Audience Manager-metoder {#audience-manager-methods}

Här är en lista över de Audience Manager-metoder som finns i iOS bibliotek.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna prefixeras enligt lösningen och Audience Manager-metoderna prefixas med &quot; `audience`.&quot;

Om Audience Manager är konfigurerat i JSON-filen skickas en signal som innehåller livscykelvärden med `application:didFinishLaunchingWithOptions:`.

* **publikVisitorProfil**

   Returnerar den besökarprofil som senast hämtades och, om ingen signal har skickats, returneras `null`. Besökarprofilen sparas i `NSUserDefaults` för enkel åtkomst när du startar programmet flera gånger.

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

   * The **Data Provider ID (DPID)** är det datapartners ID som tilldelas av Audience Manager.
   * The **Dataproviderns unika användar-ID (DPUID)** är dataleverantörens unika ID för användaren.

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

   Återställer Audience Manager UID och tömmer den aktuella besökarprofilen.

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
