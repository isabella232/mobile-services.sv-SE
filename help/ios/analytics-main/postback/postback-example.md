---
description: Exempel på definitioner och källkod för funktionen Postback.
seo-description: Exempel på definitioner och källkod för funktionen Postback.
seo-title: Exempel på återanslående
solution: Marketing Cloud,Analytics
title: Exempel på återanslående
topic: Developer and implementation
uuid: 809c5646-7a80-40df-984b-0af89d854259
translation-type: tm+mt
source-git-commit: e481b046769c3010c41e1e17c235af22fc762b7e

---


# Exempel på återanslående {#postback-example}

Exempel på definitioner och källkod för funktionen Postback.

>[!CAUTION]
>
>Det här exemplet finns endast i informationssyfte. Filen bör konfigureras i Adobe Mobile-gränssnittet och får inte ändras manuellt. `ADBMobileConfig.json` En manuellt redigerad konfigurationsfil kan vara farlig om konfigurationen av fjärrmeddelanden är aktiverad.

## ADBMobileConfig.json-definition {#section_0F6EC001AB6D488E815F50C7F5DA022E}

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

## Kodexempel {#section_8169B88A2C634CB788DA574EE8C4B1DC}

```objective-c
NSDictionary *contextData = @{@"user.name":@"bob", @"user.zip":@"90210"}; 
[ADBMobile trackState:@"MainMenu" data:contextData];
```

Eftersom det här spårningsanropet är `“MainMenu”`i läget utlöses det ovanstående återanslående meddelandet. URL:en ersätter alla mallvariabler med värden från träffen. Om man utgår ifrån att användarens föregående session var 132 sekunder lång och att användaren är i iOS SDK version 4.6.0, visas ett exempel på den resulterande URL:en:

`https://my.server.com/?user=bob&zip=90210&c16=4.6.0-iOS&c27=cln,132`
