---
description: Den här informationen hjälper dig att hämta lokalt lagrade SDK-identiteter från din Android-app och med förfrågningar om GDPR-dataåtkomst.
title: Hämtar lagrade identifierare
uuid: 6fd3d202-b0a1-4c80-96f4-369fc24ac0a3
exl-id: 86c990d8-334b-4003-b0ac-d5404cb598e4
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Hämtar lagrade identifierare{#retrieving-stored-identifiers}

Den här informationen hjälper dig att hämta lokalt lagrade SDK-identiteter från din Android-app och med förfrågningar om GDPR-dataåtkomst.

>[!IMPORTANT]
>
>Metoden `getAllIdentifiersAsync` hämtar identiteter som lagras i SDK:n. Du måste anropa den här metoden **innan** användaren väljer bort.

SDK-identiteter (om tillämpligt) lagras lokalt och returneras i en JSON-sträng som kan innehålla:

* Företagskontext - IMS-organisations-ID
* Användar-ID
* Experience Cloud iD (MID), tidigare Marketing Cloud ID
* Integrationskoder (ADID, Push ID)
* ID för datakälla (DPID, DPUUID)
* Analys-ID:n (AVID, AID, VID och associerade RSID)
* Tidigare måls-ID (TNTID, TNT3rdpartyID)
* Audience Manager ID (UUID)

Här är ett exempel på metoden `ADBMobile getAllIdentifiersAsync` i Android:

```java
Config.getAllIdentifiersAsync(new ConfigCallback<String>() { 
     @Override 
     public void call(String identitiesJson) {                 
         Log.d("ADBMobile Identities", identitiesJson); 
     } 
});
```
