---
description: Den här informationen kan hjälpa dig att felsöka push-meddelanden.
keywords: mobile
seo-description: Den här informationen kan hjälpa dig att felsöka push-meddelanden.
seo-title: Felsökning av push-meddelanden
solution: Marketing Cloud,Analytics
title: Felsökning av push-meddelanden
topic: Metrics
uuid: c7be4ab7-0cfe-4296-84a8-01412f4fd93f
translation-type: tm+mt
source-git-commit: e9691f9cbeadd171948aa752b27a014c3ab254d6

---


# Felsöka push-meddelanden{#troubleshooting-push-messaging}

Den här informationen kan hjälpa dig att felsöka push-meddelanden.

## Varför dröjer det ibland med att skicka push-meddelanden?

Följande typer av fördröjningar kan associeras med push-meddelanden för mobiltjänster:

* **Väntar på Analytics-träffar**

   Varje rapportsvit har en inställning som avgör när inkommande Analytics-träffar ska behandlas. Standardvärdet är var 1 timme.

   Den faktiska bearbetningen av Analytics-träffar kan ta upp till 30 minuter, men är vanligtvis 15-20 minuter. En rapportserie träffar till exempel varje timme. När du anger den nödvändiga bearbetningstiden på högst 30 minuter kan det ta upp till 90 minuter innan en inkommande träff blir tillgänglig för ett push-meddelande. Om en användare startade appen kl. 9.01 visas träffen i gränssnittet för mobila tjänster som en ny unik användare mellan kl. 10.15 och kl. 10.30.

* **Väntar på push-tjänsten**

   Push-tjänsten (APNS eller GCM) kanske inte skickar ut meddelandet omedelbart. Även om det är ovanligt har det förekommit väntetider på upp till 5-10 minuter. Du kan verifiera att push-meddelandet har skickats till push-tjänsten genom att titta i **[!UICONTROL Report]** vyn över push-meddelandet, hitta meddelandet i **[!UICONTROL Message History]** tabellen och titta på **[!UICONTROL Published]** antalet.

   >[!TIP]
   >
   >Detta är antalet lyckade utskick till push-tjänsten. Push-tjänsterna garanterar inte att ett meddelande kommer att skickas.

   Mer information om tillförlitligheten i tjänsten finns i:

   * [Tjänstekvalitet](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW5l)
   * [Ett meddelandes](https://developers.google.com/cloud-messaging/concept-options#lifetime)livstid.

## Varför är min Android GCM API-nyckel ogiltig?

* **Ogiltig API-nyckel**

   API-nyckeln kan vara ogiltig av följande orsaker:

   * Den angivna API-nyckeln är inte en servernyckel med rätt GCM API-nyckelvärde.
   * Servernyckeln har vitlistat IP-adresserna och blockerar Adobes servrar från att skicka ett push-meddelande.

* **Bestämma API-nyckelns giltighet**

   Kör följande kommando för att avgöra om API-nyckeln är giltig:

   **Android**

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

   Du kan också kontrollera giltigheten för en registreringstoken genom att ersätta `"ABC"` den med token.

## Varför fungerar inte mitt APNS-certifikat?

Ditt APNS-certifikat kan vara ogiltigt av följande orsaker:

* Du kanske använder ett sandlådecertifikat i stället för produktionscertifikatet.
* Du använder ett nytt produktions-/sandlådecertifikat som inte stöds.
* Du använder `.p8` fil i stället för en `.p12` fil.

## Åtgärdar fel i push-meddelanden

**Ett exempel**

Följande exempel visar hur du kan lösa ett push-fel när du använder ett VRS.

Följande kund har två iOS-appar:

* Programnamn: PhotoShop_app_iOS
   * Överordnad RSID: AllaAdobe PhotoShop_apps
   * VRSID: PhotoShop_iOS_app_SF
   * VRSID-definitionssegment: `a.appid contains “PhotoShop_iOS_app_SF”`
* Programnamn: PhotoShop_app_iOS
   * Överordnad RSID: AllaAdobe PhotoShop_apps
   * RSID: PhotoShop_iOS_app_LA
   * VRSID-definitionssegment: `a.os contains “iOS”`

Om en Photoshop-anställd i det här exemplet skickar en push till appen *PhotoShop_iOS_app_SF* får alla *användare av appen* Photoshop_iOS_app_SF det push-meddelande som de förväntar sig. Men om medarbetaren skickar ett meddelande till appen *PhotoShop_iOS_app_LA* eftersom dess VRSID-definitionssegment är felaktigt (i stället`iOS` för `a.os contains "PhotoShop_iOS_app_LA"`) skickas meddelandet till **alla** iOS-användare i *Alla Adobe PhotoShop_apps*. Även om meddelandet fortfarande går till *PhotoShop_iOS_app_LA* -användare, visas även push-ID:n för *PhotoShop_iOS_app_SF* -användare i meddelandet, eftersom *PhotoShop_iOS_app_SF* -appen har ett annat certifikat. Om segmentet hade definierats som `a.os contains “PhotoShop_iOS_app_LA”`skulle push-meddelandet bara ha skickats till *PhotoShop_iOS_app_LA* -användare.

Om det skickas med push-certifikatet *PhotoShop_IOS_app_LA* återgår push-identifierarna för *PhotoShop_iOS_app_SF* som `invalid`.

>[!CAUTION]
>
>När du har skapat ett push-meddelande för en app som använder ett VRS-system och klickat **[!UICONTROL Save & Send]** visas en varning som påminner dig om att varje app som visas **måste** ha ett giltigt certifikat. Om varje app **inte** har ett giltigt certifikat kan målgruppssegmenten bli svartlistade i oändlighet, och du kanske inte kan skicka fler push-meddelanden till de berörda användarna. Mer information om målgruppssegment finns i [Målgrupp: definiera och konfigurera målgruppsalternativ för push-meddelanden](/help/using/in-app-messaging/t-create-push-message/c-audience-push-message.md).
