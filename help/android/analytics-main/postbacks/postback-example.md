---
description: Du kan använda den här informationen för att få en förståelse för återanslående och hur de fungerar.
keywords: android;library;mobile;sdk
seo-description: Du kan använda den här informationen för att få en förståelse för återanslående och hur de fungerar.
seo-title: Exempel på återgång
solution: Marketing Cloud,Analytics
title: Exempel på återgång
topic: Developer and implementation
uuid: 8010cd00-d42b-4e16-8403-692fab2550f1
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Exempel på återgång {#postbacks-example}

Du kan använda den här informationen för att få en förståelse för vilka återanslående som är och hur de fungerar.

>[!CAUTION]
>
>Det här exemplet finns endast i informationssyfte. Filen bör konfigureras i Adobe Mobile-gränssnittet och får inte ändras manuellt. `ADBMobileConfig.json` En manuellt redigerad konfigurationsfil kan vara farlig om konfigurationen av fjärrmeddelanden är aktiverad.

## `ADBMobileConfig.json` definition {#section_8751E8176F3546C09420341A39758AFF}

```js
"messages": [ 
    { 
        "messageId": "79ae37c9-89b9-465e-af7f-d3351771f1dc", 
        "template": "callback", 
        "payload": {  
            "templateurl": "https://my.server.com/?user={user.name}&zip={user.zip}&c16={%sdkver%}&c27=cln,{a.PrevSessionLength}", 
            "templatebody": "c2RrdmVyPXslc2RrdmVyJX0mY2I9eyVjYWNoZWJ1c3QlfSZjbGllbnRJZD17bi5jbGllbnQuaWR9JnRzPXsldGltZXN0YW1wVSV9JnRzej17JXRpbWVzdGFtcFolfQ==", 
            "contenttype": "application/x-www-form-urlencoded",  
            "timeout": 4 
        }, 
        "showOffline": true, 
        "showRule": "always", 
        "endDate": 2524730400, 
        "startDate": 0, 
        "audiences": [], 
        "triggers": [ 
            { 
                "key": "pageName", 
                "matches": "eq", 
                "values": [ 
                    "MainMenu" 
                ] 
            } 
        ] 
    } 
] 
```

## Kodexempel {#section_D063DE82976D4EDEA97E804BD1C4718F}

```js
HashMap<String, Object> contextData = new HashMap<String, Object>(); 
contextData.put("user.name", "bob"); 
contextData.put("user.zip", "90210"); 
Analytics.trackState("MainMenu", contextData);
```

Eftersom det här spårningsanropet är `“MainMenu”`i läget utlöses det ovanstående återanslående meddelandet. URL:en ersätter alla mallvariabler med värden från träffen. Om man utgår ifrån att användarens föregående session var 132 sekunder lång och att användaren använder Android SDK version 4.6.0 ser den resulterande URL-adressen ut så här:

`https://my.server.com/?user=bob&zip=90210&c16=4.6.0-AN&c27=cln,132`
