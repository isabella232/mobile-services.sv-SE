---
description: Den här informationen hjälper dig att hämta lokalt lagrade Experience Cloud SDK-identiteter från din iOS-app och med förfrågningar om dataåtkomst i GDPR.
title: Hämtar lagrade identifierare
uuid: 4fb2c166-6700-4f8b-b60b-137b199e0509
exl-id: ec8592af-fb08-4ab3-99a1-51ac5697a3d8
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 2%

---

# Hämtar lagrade identifierare{#retrieving-stored-identifiers}

Den här informationen hjälper dig att hämta lokalt lagrade Experience Cloud SDK-identiteter från din iOS-app och med förfrågningar om dataåtkomst i GDPR.

Mer information om GDPR finns i [GDPR och Ditt företag](https://www.adobe.com/se/privacy/general-data-protection-regulation.html).

>[!IMPORTANT]
>
>Metoden `getAllIdentifiersAsync` hämtar identiteter som lagras i SDK:erna för Experience Cloud. Du måste anropa den här metoden **innan** användaren väljer bort.

Experience Cloud SDK-identiteter (om tillämpligt) lagras lokalt och returneras i en JSON-sträng som kan innehålla:

* Företagskontext - IMS-organisations-ID
* Användar-ID
* Experience Cloud iD (MID), tidigare Marketing Cloud ID
* Integrationskoder (ADID, Push ID)
* ID för datakälla (DPID, DPUUID)
* Analys-ID:n (AVID, AID, VID och associerade RSID)
* Tidigare måls-ID (TNTID, TNT3rdpartyID)
* Audience Manager ID (UUID)

Här är ett exempel på metoden `ADBMobile getAllIdentifiersAsync` i iOS:

```objective-c
[ADBMobile getAllIdentifiersAsync:^(NSString * _Nullable content){
      NSLog(content) 
}]
```
