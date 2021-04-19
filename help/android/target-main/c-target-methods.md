---
description: Här är en lista över Adobe Target-metoder som finns i Android-biblioteket.
keywords: android;bibliotek;mobil;sdk
seo-description: Här är en lista över Adobe Target-metoder som finns i Android-biblioteket.
seo-title: Målmetoder för Android
solution: Experience Cloud,Analytics
title: Målmetoder för Android
topic-fix: Developer and implementation
uuid: 8e9808b2-ba80-4646-ba05-8e62d4fde065
exl-id: 0c7a6718-d078-4a2b-a2c9-d5cd50263939
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 23%

---

# Målmetoder för Android{#target-methods}

Här är en lista över Adobe Target-metoder som finns i Android-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna är prefasta enligt lösningen. Experience Cloud ID-metoder har till exempel prefixet `target`.

>[!TIP]
>
>[Livscykelmetrisk ](/help/android/metrics.md) skickas som parametrar till varje mbox-inläsning.

## Klassreferens: TargetLocationRequest {#section_A8CC898922164E819EC730DC92A6742B}

**Egenskaper:**

```java
public String name; 
public String defaultContent; 
public HashMap<String, Object> parameters;
```

**Strängkonstanter**

>[!TIP]
>
>Följande konstanter är enkla att använda när du anger nycklar för anpassade parametrar.

```java
public static final String TARGET_PARAMETER_ORDER_ID   = "orderId"; 
public static final String TARGET_PARAMETER_ORDER_TOTAL         = "orderTotal"; 
public static final String TARGET_PARAMETER_PRODUCT_PURCHASE_ID = "productPurchasedId"; 
public static final String TARGET_PARAMETER_CATEGORY_ID         = "categoryId"; 
public static final String TARGET_PARAMETER_MBOX_3RDPARTY_ID    = "mbox3rdPartyId"; 
public static final String TARGET_PARAMETER_MBOX_PAGE_VALUE     = "mboxPageValue"; 
public static final String TARGET_PARAMETER_MBOX_PC             = "mboxPC"; // pcId in cookie 
public static final String TARGET_PARAMETER_MBOX_SESSION_ID     = "mboxSession"; // sessionId in cookie 
public static final String TARGET_PARAMETER_MBOX_HOST           = "mboxHost";
```

>[!IMPORTANT]
>
>* Om du använder SDK:er **före** version 4.14.0, se [https://developers.adobetarget.com/api/#input-parameters](https://developers.adobetarget.com/api/#input-parameters) för parameterbegränsningar.
   >
   >
* Om du använder SDK:er version 4.14.0 **eller senare** läser du [https://developers.adobetarget.com/api/#batch-input-parameters](https://developers.adobetarget.com/api/#batch-input-parameters) för parameterbegränsningar.


* **loadRequest**

   Skickar begäran till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```java
      public static void loadRequest(TargetLocationRequest request, TargetCallback<String> callback);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Target.loadRequest(heroBannerRequest, new Target.TargetCallback<String>() {  @Override  public void call(String item) {   // do something with item  } });
      ```

* **loadRequest**

   Skickar begäran till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```java
      public static void loadRequest(final String name final String defaultContent, final Map `<String, Object>` profileParameters, 
                                     final Map `<String, Object>` orderParameters,final Map `<String Object>` mboxParameters, final TargetCallback<String> callback)
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Map `<String, Object>` profileParameters = new HashMap `<String, Object>`(); profileParameters.put(“profile-parameter-key”, “profile-parameter-value”); 
      Map `<String, Object>` orderParameters = new HashMap `<String, Object>`(); orderParameters.put(“order-parameter-key”, “order-parameter-value”);
      Map `<String, Object>` mboxParameters = new HashMap `<String, Object>`(); 
      mboxParameters.put(“mbox-parameter-key”, “mbox-parameter-value”); 
      Target.loadRequest(“mboxName”, “defaultContent”, profileParameters, orderParameters, mboxParameters
      new TargetCallback<String>() {
          @Override
          public void call (String item) {
             Log.d(“Target Content”, item); 
          }
      });
      ```

* **loadRequest**

   Skickar en begäran till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett TargetCallback.

   * Här är syntaxen för den här metoden:

      ```java
      public static void loadRequest(final String name, final String defaultContent, final Map<String, Object> profileParameters, final Map<String, Object> orderParameters, final Map<String, Object> mboxParameters, final Map<String, Object> requestLocationParameters, final TargetCallback<String> callback);
      ```

   * **Returnerar:** Ej tillämpligt

   * **Parametrar:**

      Här är parametrarna för den här metoden:

      * **name**

         Namnet på målrutan/målplatsen som du vill hämta.

         * **text:** String
      * **defaultContent**

         Värdet returneras i återanropet om målservern inte kan nås eller om användaren inte är berättigad till kampanjen.

         * **text:** String
      * **profileParameters**

         Värden i den här ordlistan placeras i objektet &quot;profileParameters&quot; i begäran till Target.

         * **text:** Karta  `<String, Object>`
      * **orderParameters**

         Värden i den här ordlistan placeras i objektet &quot;order&quot; i begäran till Target.

         * **text:** Karta  `<String, Object>`
      * **mboxParameters**

         Värden i den här ordlistan skickas i begäran till Target.

         * **text:** Karta  `<String, Object>`
      * **requestLocationParameters**

         Värden i den här ordlistan placeras i objektet &quot;requestLocation&quot; i begäran till Target.

         * **text:** Karta  `<String, Object>`
      * **callback**

         Den här metoden anropas med innehållet i erbjudandet från målservern. Om målservern inte kan nås eller om användaren inte är berättigad till kampanjen returneras defaultContent.

         * **Typ:** TargetCallback  `<String>`
   * Här är exempelkoden för den här metoden:

      ```java
      Map `<String, Object>` profileParameters = new HashMap `<String, Object>`(); profileParameters.put(“profile-parameter-key”, “profile-parameter-value”); 
      Map `<String, Object>` orderParameters = new HashMap `<String, Object>`(); orderParameters.put(“order-parameter-key”, “order-parameter-value”); 
      Map `<String, Object>` mboxParameters = new HashMap `<String, Object>`(); mboxParameters.put(“mbox-parameter-key”, “mbox-parameter-value”); 
      Map `<String, Object>` requestLocationParameters = new HashMap `<String, Object>`(); requestLocationParameters.put(“request-location-parameter-key”, “request-location-parameter-value”); 
      
      Target.loadRequest(“mboxName”, “defaultContent”, profileParameters, orderParameters, mboxParameters, requestLocationParameters,new TargetCallback<String>() {
         @Override
         public void call (String item) { 
            Log.d(“Target Content”, item);
         } 
      });
      ```

      Mer information om det underliggande mål-API:t finns i [Delivery](https://docs.adobe.com/dev/products/target/reference/delivery.html) i hjälpen för målutvecklare.








* **createOrder &#x200B; ConfirmRequest**

   Skapar ett TargetLocationRequest-objekt med de angivna parametrarna.

   * Här är syntaxen för den här metoden:

      ```java
      public static TargetLocationRequest createOrderConfirmRequest(String name, String orderId, String orderTotal, String productPurchasedId, Map<String, Object> parameters);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      TargetLocationRequest orderConfirm = Target.createOrderConfirmRequest("orderConfirm", "order", "47.88", "3722", null);
      ```

* **createRequest**

   Skapar ett TargetLocationRequest-objekt med de angivna parametrarna.

   * Här är syntaxen för den här metoden:

      ```java
      public static TargetLocationRequest createRequest(String name, String defaultContent, Map<String, Object> parameters);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      TargetLocationRequest heroBannerRequest = Target.createRequest("heroBanner", "default.png", null);
      ```

* **clearCookies**

   Tar bort alla målcookies från din app.

   * Här är syntaxen för den här metoden:

      ```java
      public static void clearCookies();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Target.clearCookies();
      ```

* **getPcID**

   Returnerar pcID.

   * Här är syntaxen för den här metoden:

      ```java
      public static String getPcID();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Target.getPcID();
      ```

* **getSessionID**

   Returnerar sessions-ID.

   * Här är syntaxen för den här metoden:

      ```java
      public static String getSessionID();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Target.getSessionID();
      ```

* **setThirdPartyID**

   Anger ID för tredje part.

   * Här är syntaxen för den här metoden:

      ```java
      public static String setThirdPartyID(final String thirdPartyId);
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      Target.setThirdPartyID(“third-party-id”);
      ```

* **getThirdPartyID**

   Returnerar tredjeparts-ID.

   * Här är syntaxen för den här metoden:

      ```java
      public static String getThirdPartyID();
      ```

   * Här är kodexemplet för den här metoden:

      ```java
      String thirdPartyId = Target.getThirdPartyID();
      ```
