---
description: Lista över Target-metoder som tillhandahålls av Universal Windows Platform-biblioteket.
seo-description: Lista över Target-metoder som tillhandahålls av Universal Windows Platform-biblioteket.
seo-title: Målmetoder
solution: Marketing Cloud,Analytics
title: Målmetoder
topic: Developer and implementation
uuid: 2ad5953b-7850-446a-8053-b3715b86329b
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Målmetoder {#target-methods}

Lista över Target-metoder som tillhandahålls av Universal Windows Platform-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target och Audience Manager.

[Livscykelmätvärden](/help/universal-windows/metrics.md) skickas som parametrar till varje mbox-inläsning.

>[!TIP]
>
>När du använder `winmd` metoder från winJS (JavaScript) får alla metoder automatiskt sin första bokstav nedsänkt.

## Klassreferens: TargetLocationRequest

## Egenskaper

```
property Platform::String ^name; 
property Platform::String ^defaultContent; 
property Windows::Foundation::Collections::IMap<Platform::String^, Platform::Object^> ^parameters;
```

## Strängkonstanter

Den här informationen hjälper dig att ange nycklar för anpassade parametrar.

```
static property Platform::String ^TARGET_PARAMETER_ORDER_ID { 
  Platform::String ^get() { return L"orderId"; } 
} 
static property Platform::String ^TARGET_PARAMETER_ORDER_TOTAL { 
  Platform::String ^get() { return L"orderTotal"; } 
} 
static property Platform::String ^TARGET_PARAMETER_PRODUCT_PURCHASE_ID { 
  Platform::String ^get() { return L"productPurchasedId"; } 
} 
static property Platform::String ^TARGET_PARAMETER_CATEGORY_ID { 
  Platform::String ^get() { return L"categoryId"; } 
} 
static property Platform::String ^TARGET_PARAMETER_MBOX_3RDPARTY_ID { 
  Platform::String ^get() { return L"mbox3rdPartyId"; } 
} 
static property Platform::String ^TARGET_PARAMETER_MBOX_PAGE_VALUE { 
  Platform::String ^get() { return L"mboxPageValue"; } 
} 
static property Platform::String ^TARGET_PARAMETER_MBOX_PC { 
  Platform::String ^get() { return L"mboxPC"; } 
} 
static property Platform::String ^TARGET_PARAMETER_MBOX_SESSION_ID { 
  Platform::String ^get() { return L"mboxSession"; } 
} 
static property Platform::String ^TARGET_PARAMETER_MBOX_HOST { 
  Platform::String ^get() { return L"mboxHost"; } 
}
```

* **LoadRequest (winJS: loadRequest)**

   Skickar `request` till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett block `callback`.

   * Här är syntaxen för den här metoden:

      ```csharp
      static Windows::Foundation::IAsyncOperation<Platform::String ^> ^LoadRequest(TargetLocationRequest ^request);
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var fADB = ADBMobile; 
       ADB.Target.loadRequest(heroBannerRequest).then(function(content){ 
          //do something with content returned from target server 
       });
      ```

* **CreateRequest (winJS: createRequest)**

   Skapar ett `TargetLocationRequest` objekt med de angivna parametrarna.

   * Här är syntaxen för den här metoden:

      ```csharp
      static TargetLocationRequest ^CreateRequest(Platform::String ^name, Platform::String ^defaultContent,Windows::Foundation::Collections::IMap<Platform::String^,Platform::Object^> ^parameters); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      var ADB = ADBMobile;
      var heroBannerRequest = ADB.Target.createRequest("heroBanner","default.png", null); 
      ```

* **CreateOrder &#x200B; ConfirmRequest (winJS: createOrder &#x200B; ConfirmRequest)**

   Skapar ett `TargetLocationRequest` objekt med de angivna parametrarna.

   * Här är syntaxen för den här metoden:

      ```csharp
      static TargetLocationRequest ^CreateOrderConfirmRequest(Platform::String ^name, Platform::String ^orderId,Platform::String ^orderTotal,Platform::String ^productPurchasedId,Windows::Foundation::Collections::IMap<Platform::String^,Platform::Object^> ^parameters); 
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      varADB = ADBMobile;
      var orderConfirm = ADB.Target.createOrderConfirmRequest("orderConfirm","order","47.88","3722",null);
      ```

* **ClearCookies (winJS: clearCookies)**

   Rensar målcookies för programmet på den aktuella enheten.

   * Här är syntaxen för den här metoden:

      ```csharp
      static void ClearCookies();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      ADBMobile.Target.clearCookies();
      ```

* **GetPcId (winJS: getPcId)**

   Returnerar PC ID-cookie för den aktuella enheten.

   * Här är syntaxen för den här metoden:

      ```csharp
      staticPlatform::String ^GetPcId();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
      autopcId = ADBMobile.Target.getPcId();
      ```

* **GetSessionId (winJS: getSessionId)**

   Returnerar cookie-filen för sessions-ID för den aktuella enheten.

   * Här är syntaxen för den här metoden:

      ```csharp
      staticPlatform::String ^GetSessionId();
      ```

   * Här är kodexemplet för den här metoden:

      ```js
       autosessionId=ADBMobile.Target.getSessionId(); 
      ```
