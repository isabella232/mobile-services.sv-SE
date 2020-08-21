---
description: Här är Experience Cloud ID-metoderna som tillhandahålls av Android-biblioteket.
keywords: android;library;mobile;sdk
seo-description: Här är Experience Cloud ID-metoderna som tillhandahålls av Android-biblioteket.
seo-title: Adobe Experience Platform Identity Service-metoder
solution: Marketing Cloud,Analytics
title: Adobe Experience Platform Identity Service-metoder
topic: Developer and implementation
uuid: c5107a7e-273b-4f71-8738-4c603479b24c
translation-type: tm+mt
source-git-commit: 7ae626be4d71641c6efb127cf5b1d3e18fccb907
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 23%

---


# Adobe Experience Platform Identity Service methods{#experience-cloud-id-service-methods}

Här är Experience Cloud ID-metoderna som tillhandahålls av Android-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service.

Metoderna är prefasta enligt lösningen. Experience Cloud ID-metoder har till exempel prefixet `visitor`. Mer information finns i [Experience Cloud ID-konfiguration](/help/android/c-marketing-cloud/mcvid.md).

* **public static String appendToURL(final String URL)**

   Lägger till besöksdata från Adobe i en URL-sträng som ska användas med JavaScript-biblioteket Adobe. Du måste ha Mobile SDK 4.12+ för att kunna använda den här metoden. Mer information finns i [Bifoga hjälpfunktion](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/appendvisitorid.html)för besökar-ID.

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
      >Den här metoden kan orsaka ett blockerande nätverksanrop och bör **inte** anropas från en gränssnittstråd.

* **syncIdentifiers**

   Med Experience Cloud-ID:t kan du ange ytterligare kund-ID:n som kan kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare, med en kundtypsidentifierare som avgränsar omfattningen för olika kund-ID:n. Den här metoden motsvarar den `setCustomerIDs` i JavaScript-biblioteket.

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

   Ange `authenticationState` ett av följande värden:

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

   Ange `authenticationState` ett av följande värden:
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
