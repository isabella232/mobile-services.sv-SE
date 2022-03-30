---
description: Den här informationen kan hjälpa dig att felsöka push-meddelanden.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Felsökning av push-meddelanden
topic-fix: Metrics
uuid: c7be4ab7-0cfe-4296-84a8-01412f4fd93f
exl-id: 56feb8e1-e196-4b70-8240-6e41581ca602
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# Felsöka push-meddelanden{#troubleshooting-push-messaging}

Den här informationen kan hjälpa dig att felsöka push-meddelanden.

## Varför dröjer det ibland med att skicka push-meddelanden?

Följande typer av fördröjningar kan vara kopplade till push-meddelanden för Mobile Services:

* **Väntar på Analytics-träffar**

   Varje rapportsvit har en inställning som avgör när inkommande Analytics-träffar ska behandlas. Standardvärdet är var 1 timme.

   Den faktiska bearbetningen av Analytics-träffar kan ta upp till 30 minuter, men är vanligtvis 15-20 minuter. En rapportserie träffar till exempel varje timme. När du anger den nödvändiga bearbetningstiden på högst 30 minuter kan det ta upp till 90 minuter innan en inkommande träff blir tillgänglig för ett push-meddelande. Om en användare startade appen kl. 9.01 visas träffen i användargränssnittet för Mobile Services som en ny unik användare mellan kl. 10.15 och kl. 10.30.

* **Väntar på push-tjänsten**

   Push-tjänsten (APNS eller GCM) kanske inte skickar ut meddelandet omedelbart. Även om det är ovanligt har det förekommit väntetider på upp till 5-10 minuter. Du kan verifiera att push-meddelandet har skickats till push-tjänsten genom att titta i **[!UICONTROL Report]** vy för push-meddelandet, hitta meddelandet i **[!UICONTROL Message History]** och tittar på **[!UICONTROL Published]** antal.

   >[!TIP]
   >
   >Push-tjänsterna garanterar inte att ett meddelande kommer att skickas. Mer information om tjänsternas tillförlitlighet finns i lämplig dokumentation:
   >
   >* **APNS**: [Tjänstekvalitet](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW5)
   >* **FCM**: [Meddelandets livstid](https://firebase.google.com/docs/cloud-messaging/concept-options#lifetime)


## Varför är min Android GCM API-nyckel ogiltig?

* **Ogiltig API-nyckel**

   API-nyckeln kan vara ogiltig av följande orsaker:

   * Den angivna API-nyckeln är inte en servernyckel med rätt GCM API-nyckelvärde.
   * Servernyckeln tillåter IP-adresser och blockerar Adobe-servrar från att skicka ett push-meddelande.

* **Bestämma API-nyckelns giltighet**

   Kör följande kommando för att avgöra om API-nyckeln är giltig:

   ```java
   # api_key=YOUR_API_KEY
   #curl--header"Authorization:key=$api_key"\
       --headerContent-Type:"application/json"\ 
       https://gcm-http.googleapis.com/gcm/send\
       -d"{\"registration_ids\":[\"ABC\"]}"
   ```

   En returnerad 401 HTTP-statuskod betyder att API-nyckeln är ogiltig. Annars ser du något liknande:

   ```java
   {"multicast_id":6782339717028231855,"success":0,"failure":1,
   canonical_ids":0,"results":[{"error":"InvalidRegistration"}]}
   ```

   Du kan även kontrollera giltigheten för en registreringstoken genom att ersätta `"ABC"` med token.

## Varför fungerar inte mitt APNS-certifikat?

Ditt APNS-certifikat kan vara ogiltigt av följande orsaker:

* Du kanske använder ett sandlådecertifikat i stället för produktionscertifikatet.
* Du använder ett nytt produktions-/sandlådecertifikat som inte stöds.
* Du använder `.p8` i stället för en `.p12` -fil.

## Åtgärdar fel i push-meddelanden

Följande exempel visar hur du kan lösa ett push-fel när du använder ett VRS.

Följande kund har två iOS-appar:

* Programnamn: Photoshop_app_iOS
   * Överordnad RSID: AllaAdobe Photoshop_apps
   * VRSID: Photoshop_iOS_app_SF
   * VRSID-definitionssegment: `a.appid contains "PhotoShop_iOS_app_SF"`
* Programnamn: Photoshop_app_iOS
   * Överordnad RSID: AllaAdobe Photoshop_apps
   * RSID: Photoshop_iOS_app_LA
   * VRSID-definitionssegment: `a.os contains "iOS"`

Om en Photoshop-anställd i det här exemplet skickar en push-funktion till *Photoshop_iOS_app_SF* app, alla *Photoshop_iOS_app_SF-app* användarna får push-meddelandet som förväntat. Men om medarbetaren skickar ett meddelande till *Photoshop_iOS_app_LA* app, eftersom dess VRSID-definitionssegment är felaktigt (`iOS` i stället för `a.os contains "PhotoShop_iOS_app_LA"`) skickas meddelandet till **alla** iOS användare i *AllaAdobe Photoshop_apps*. Även om meddelandet fortfarande går till *Photoshop_iOS_app_LA* -användare blocklist meddelandet även push-ID:n för *Photoshop_iOS_app_SF* användare eftersom *Photoshop_iOS_app_SF* appen har ett annat certifikat. Om segmentet hade definierats som `a.os contains "PhotoShop_iOS_app_LA"`, skulle push-meddelandet bara ha skickats till *Photoshop_iOS_app_LA* -användare.

Om det skickas med *Photoshop_IOS_app_LA* push-certifikat, push-identifierare för *Photoshop_iOS_app_SF* kom tillbaka som `invalid`.

>[!CAUTION]
>
>När du har skapat ett push-meddelande för en app som använder ett VRS-system klickar du på **[!UICONTROL Save & Send]** visas en varning som påminner dig om att alla appar som visas **måste** har ett giltigt certifikat. Om varje app gör det **not** har ett giltigt certifikat, målgruppssegmenten kan vara oändligt blocklist och du kanske inte kan skicka fler push-meddelanden till berörda användare. Mer information om målgruppssegment finns i [Målgrupp: definiera och konfigurera målgruppsalternativ för push-meddelanden](/help/using/in-app-messaging/t-create-push-message/c-audience-push-message.md).
