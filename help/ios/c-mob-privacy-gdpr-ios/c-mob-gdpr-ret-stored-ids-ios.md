---
description: Den här informationen hjälper dig att hämta lokalt lagrade Experience Cloud SDK-identiteter från din iOS-app och med förfrågningar om GDPR-dataåtkomst.
seo-description: Den här informationen hjälper dig att hämta lokalt lagrade Experience Cloud SDK-identiteter från din iOS-app och med förfrågningar om GDPR-dataåtkomst.
seo-title: Hämtar lagrade identifierare
title: Hämtar lagrade identifierare
uuid: 4fb2c166-6700-4f8b-b60b-137b199e0509
translation-type: tm+mt
source-git-commit: 06144a1695ac40ce984656491456968888f9e96e

---


# Hämtar lagrade identifierare{#retrieving-stored-identifiers}

Den här informationen hjälper dig att hämta lokalt lagrade Experience Cloud SDK-identiteter från din iOS-app och med förfrågningar om GDPR-dataåtkomst.

Mer information om GDPR finns i [GDPR och Ditt företag](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!IMPORTANT]
>
>Metoden hämtar `getAllIdentifiersAsync` identiteter som lagras i Experience Cloud SDK:er. Du måste anropa den här metoden **innan** användaren avanmäler sig.

Experience Cloud SDK-identiteter (om tillämpligt) lagras lokalt och returneras i en JSON-sträng, som kan innehålla:

* Företagskontext - IMS-organisations-ID
* Användar-ID
* Experience Cloud iD (MID), tidigare Marketing Cloud ID
* Integrationskoder (ADID, Push ID)
* ID för datakälla (DPID, DPUUID)
* Analys-ID:n (AVID, AID, VID och associerade RSID)
* Tidigare måls-ID (TNTID, TNT3rdpartyID)
* Audience Manager ID (UUID)

Här är ett exempel på `ADBMobile getAllIdentifiersAsync` metoden i iOS:

```objective-c
[ADBMobile getAllIdentifiersAsync:^(NSString * _Nullable content){
      NSLog(content) 
}]
```

