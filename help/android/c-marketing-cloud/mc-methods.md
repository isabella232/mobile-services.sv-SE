---
description: Här är Experience Cloud ID-metoderna som tillhandahålls av Android-biblioteket.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Adobe Experience Platform Identity Service-metoder
topic-fix: Developer and implementation
uuid: c5107a7e-273b-4f71-8738-4c603479b24c
exl-id: 8eb98c3f-c6ef-4593-ad3a-f566f4d4b6a2
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 24%

---

# Adobe Experience Platform Identity Service-metoder{#experience-cloud-id-service-methods}

Här är Experience Cloud ID-metoderna som tillhandahålls av Android-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service.

Metoderna är prefasta enligt lösningen. Experience Cloud ID-metoder har till exempel prefix `visitor`. Mer information finns i [Experience Cloud ID-konfiguration](/help/android/c-marketing-cloud/mcvid.md).

* **public static String appendToURL(final String URL)**

   Lägger till besöksdata från Adobe i en URL-sträng som ska användas med JavaScript-biblioteket Adobe. Du måste ha Mobile SDK 4.12+ för att kunna använda den här metoden. Mer information finns i [appendVisitorIDsTo](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/appendvisitorid.html) i dokumentationen för Adobe Experience Cloud Identity Service.

   >[!IMPORTANT]
   >
   >Den här metoden kan orsaka ett blockerande nätverksanrop. Anropa inte detta på tidskänsliga trådar.

   * Här är syntaxen för den här metoden:

      ```java
      public static String appendToURL(final String URL) 
      ```

      En obligatorisk URL-sträng som besökarinformationen läggs till i.

   * Här är kodexemplet för den här metoden:

      ```java
      String urlSample = "https://example.com";`
              String urlWithAdobeVisitorInfo = Visitor.appendToURL(urlSample);
      
              Intent(Intent.ACTION_VIEW);
              i.setData(Uri.parse(urlWithAdobeVisitorInfo));
              startActivity(i);
      ```

* **getMarketingCloudId**

   Hämtar Experience Cloud-ID:t från besökar-ID-tjänsten.

   * Här är syntaxen för den här metoden:

      ```java
      public static String getMarketingCloudId(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      String = Visitor.getMarketingCloudId();
      ```

      >[!IMPORTANT]
      >
      >Den här metoden kan orsaka ett blockerande nätverksanrop och bör **not** anropas från en gränssnittstråd.

* **syncIdentifiers**

   Med Experience Cloud-ID:t kan du ange ytterligare kund-ID:n som kan kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare, med en kundtypsidentifierare som avgränsar omfånget för olika kund-ID:n. Den här metoden motsvarar `setCustomerIDs` i JavaScript-biblioteket.

   * Här är syntaxen för den här metoden:

      ```java
      public static void syncIdentifiers(Map<String, String> identifiers); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Map<String,String> identifiers = new HashMap<String, String>();
      identifiers.put("idType", "idValue");
      Visitor.syncIdentifiers(identifiers);
      ```

* **syncIdentifier**

   Synkroniserar angiven identifierartyp och angivet värde med tjänsten för besökar-ID.

   Skicka in `authenticationState` som ett av följande värden:

   * `VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_UNKNOWN`
   * `VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_AUTHENTICATED`
   * `VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_LOGGED_OUT`

   * Här är syntaxen för den här metoden:

      ```java
      public static void syncIdentifier(final String identifierType, final String identifier, final VisitorID.VisitorIDAuthenticationState authenticationState);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Visitor.syncIdentifier("myIdType", "valueForUser", VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_LOGGED_OUT);
      ```

* **syncIdentifiers**

   Synkroniserar angivna identifierare till ID-tjänsten.

   Skicka in `authenticationState` som ett av följande värden:
   * `VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_UNKNOWN`
   * `VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_AUTHENTICATED`
   * `VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_LOGGED_OUT`

   * Här är syntaxen för den här metoden:

      ```java
      public static void syncIdentifiers(final Map<String String> identifiers, final VisitorID.VisitorIDAuthenticationState authenticationState);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Map<String, String> identifiers = new HashMap<String, String>();
          identifiers.put("myIdType", "valueForUser"); Visitor.syncIdentifiers(identifiers,
      VisitorID.VisitorIDAuthenticationState.VISITOR_ID_AUTHENTICATION_STATE_AUTHENTICATED); 
      ```

* **getIdentifiers**

   Hämtar en lista med skrivskyddade `ADBVisitorID` objekt.

   * Här är syntaxen för den här metoden:

      ```java
      public static List<VisitorID> getIdentifiers(); 
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      List<VisitorID> myVisitorIDs = Visitor.getIdentifiers(); 
      ```

* **getUrlVariablesAsync**

   Den här metoden, som introducerades i version 4.16.0, returnerar en sträng med URL-variabler för Visitor ID-tjänsten. Mer information om hur den här metoden används finns i [Adobe Experience Platform Identity Service-metoder](/help/android/reference/hybrid-app.md).

   * Här är syntaxen för den här metoden:

      ```java
      public static void getUrlVariablesAsync(final VisitorCallback callback);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      final String urlString = https://www.mydomain.com/index.php; 
      Visitor.getUrlVariablesAsync(new Visitor.VisitorCallback(){ 
        @Override 
        public void call(String urlVariables) { 
            final String urlStringWithVisitorData = String.format("%s?%s", urlString, urlVariables); 
            ...
        } 
      });
      ```

## Offentliga metoder {#section_8AC744B431A3438C9B45629CA3EA0F51}

```java
public class VisitorID { 
    public final String idOrigin; 
    public final String idType; 
    public final String id; 
    public VisitorIDAuthenticationState authenticationState; 
 
    public enum VisitorIDAuthenticationState { 
         VISITOR_ID_AUTHENTICATION_STATE_UNKNOWN(0), 
         VISITOR_ID_AUTHENTICATION_STATE_AUTHENTICATED(1), 
         VISITOR_ID_AUTHENTICATION_STATE_LOGGED_OUT(2); 
    } 
}
```
