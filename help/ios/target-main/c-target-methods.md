---
description: Här är en lista över Adobe Target-metoder som finns i iOS-biblioteket.
seo-description: Här är en lista över Adobe Target-metoder som finns i iOS-biblioteket.
seo-title: iOS-målmetoder för Adobe Mobile Services
solution: Experience Cloud,Analytics
title: Målmetoder för iOS
topic-fix: Developer and implementation
uuid: 692bcda1-02ba-4902-bd65-15888adf1952
exl-id: ba03f865-970c-4b48-af35-749f05b273d8
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 22%

---

# Målmetoder för iOS {#target-methods}

Här är en lista över Adobe Target-metoder som finns i iOS-biblioteket.

SDK har för närvarande stöd för flera Adobe Experience Cloud-lösningar, inklusive Analytics, Target, Audience Manager och Adobe Experience Platform Identity Service. Metoderna är prefasta enligt lösningen. Målmetoderna har till exempel prefixet `target`.

>[!TIP]
>
>Livscykelmätvärden skickas som parametrar till varje mbox-belastning. Mer information finns i [Livscykelvärden](/help/ios/metrics.md). Om du skickar Target-begäranden inuti delegatmetoden `didFinishLaunching` lägger du till ett `[ADBMobile trackAction:data:]`- eller `[ADBMobile trackState:data:]`-anrop före Target-implementeringskoden. På så sätt innehåller Target-begäranden alla livscykeldata.

## Klassreferens: ADBTargetLocationRequest

### Egenskaper

```objective-c
NSString *name; 
NSString *defaultContent; 
NSMutableDictionary *parameters;
```

### Strängkonstanter

>[!TIP]
>
>Följande konstanter är enkla att använda när du anger nycklar för anpassade parametrar.

```iOS
NSString *const ADBTargetParameterOrderId; 
NSString *const ADBTargetParameterOrderTotal; 
NSString *const ADBTargetParameterProductPurchasedId; 
NSString *const ADBTargetParameterCategoryId; 
NSString *const ADBTargetParameterMbox3rdPartyId; 
NSString *const ADBTargetParameterMboxPageValue; 
NSString *const ADBTargetParameterMboxPc; 
NSString *const ADBTargetParameterMboxSessionId; 
NSString *const ADBTargetParameterMboxHost;
```

>[!IMPORTANT]
>
>* Om du använder SDK:er **före** version 4.14.0, se [Indataparametrar](https://developers.adobetarget.com/api/#input-parameters) för parameterbegränsningar.
   >
   >
* Om du använder SDK:er version 4.14.0 **eller efter** finns det parameterbegränsningar i [batchindataparametrar](https://developers.adobetarget.com/api/#batch-input-parameters).


### Metoder

* **targetLoadRequest: &#x200B; återanrop**

   Skickar begäran till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett `callback`-block.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) targetLoadRequest:(ADBTargetLocationRequest *)request
                        callback:(void (^)(NSString *content))callback;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile targetLoadRequest:myRequest
                          callback:^(NSString *content) {
                            // do something with content
                          }];
      ```

* **targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:requestLocationParameters:callback:**

   Skickar en begäran till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) targetLoadRequestWithName:(nullable NSString *)name
                          defaultContent:(nullable NSString *)defaultContent
                      profileParameters:(nullable NSDictionary *)profileParameters
                        orderParameters:(nullable NSDictionary *)orderParameters
                         mboxParameters:(nullable NSDictionary *)mboxParameters
                requestLocationParameters:(nullable NSDictionary *)requestLocationParameters
                                 callback:(nullable void (^)(NSString
                                 * __nullable content))callback;
      ```

   * Returnerar: Ej tillämpligt

   * Här är parametrarna för den här metoden:

      * **`name`**

         Namnet på målrutan/målplatsen som du vill hämta.

         * **Typ**: NSString*
      * **`defaultContent`**

         Värdet returneras i återanropet om målservern inte kan nås eller om användaren inte är berättigad till kampanjen.

         * **Typ**: NSString*
      * **`profileParameters`**

         Värden i den här ordlistan placeras i objektet &quot;profileParameters&quot; i begäran till Target.

         * **Typ**: NSDictionary*
      * **`orderParameters`**

         Värden i den här ordlistan placeras i objektet &quot;order&quot; i begäran till Target.

         * **Typ**: NSDictionary
      * **`mboxParameters`**

         Värden i den här ordlistan placeras i objektet &quot;mboxParameters&quot; i begäran till Target.

         * **Typ**: NSDictionary*
      * **`requestLocationParameters`**

         Värden i den här ordlistan placeras i objektet &quot;requestLocation&quot; i begäran till Target.

         **Typ**: NSDictionary*

      * **`callback`**

         Den här metoden anropas med innehållet i erbjudandet från målservern. Om målservern inte kan nås, eller om användaren inte är berättigad till kampanjen, returneras defaultContent.
      **Typ**: Funktion

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile targetLoadRequestWithName:@"myHeroBanner"
                            defaultContent:@"defaultHeroBanner.png"
                        profileParameters:@{@"age":@"20-29"}
                          orderParameters:nil
                           mboxParameters:@{@"customParam":@"customValue"}
                requestLocationParameters:@{@"host":@"my.hostname.com"}
                                 callback:^(NSString *content){
                                   // do something with content
                                   myImageView.image = [UIImage imageNamed:content];
                                 }];
      ```

      Mer information om det underliggande mål-API:t finns i [Adobe Target-utvecklare](https://docs.adobe.com/dev/products/target/reference/delivery.html).







* **targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:callback**

   Skickar begäran till den konfigurerade målservern och returnerar strängvärdet för erbjudandet som genereras i ett blockåteranrop.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) targetLoadRequestWithName:(nullable NSString *)name
                          defaultContent:(nullable NSString *)defaultContent
                      profileParameters:(nullable NSDictionary *)profileParameters
                        orderParameters:(nullable NSDictionary *)orderParameters
                         mboxParameters:(nullable NSDictionary *)mboxParameters
                               callback:(nullable void (^)(NSString * __nullable content))callback;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile targetLoadRequestWithName:@"mboxName"
                            defaultContent:@"defaultContent"
                         profileParameters:{@"profile-parameter-key": @"profile-parameter-value"}
                           orderParameters:@{@"order-parameter-key": @"order-parameter-value"}
                            mboxParameters:@{@"mbox-parameter-key": @"mbox-parameter-value"}
                                   callback:^(NSString * content) {
                                           //do something with content 
                                 }
                               }];
      ```

* **targetCreateOrder &#x200B; ConfirmRequestWithName: &#x200B; orderId: &#x200B; orderTotal: &#x200B; productPurchasedId: &#x200B; parametrar**

   Skapar en `ADBTargetLocationRequest`.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (ADBTargetLocationRequest *)
      targetCreateOrderConfirmRequestWithName:(NSString *)name
                                      orderId:(NSString *)orderId
                                  orderTotal:(NSString *)orderTotal
                          productPurchasedId:(NSString *)productPurchasedId
                              parameters:(NSDictionary *)parameters;
      ```

* **targetCreateRequestWithName: &#x200B; &#x200B; defaultContent: &#x200B; parameters**

   Bekvämlighetskonstruktor för att skapa ett ADBTargetLocationRequest-objekt med de angivna parametrarna.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (ADBTargetLocationRequest *)
      targetCreateRequestWithName:(NSString *)name
                           defaultContent:(NSString *)defaultContent
                               parameters:(NSDictionary *)parameters;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      ADBTargetLocationRequest *myRequest =  
      [ADBMobile targetCreateRequestWithName:@"heroBanner"
                              defaultContent:@"default.png"
                                  parameters:nil];
      ```

* **targetThirdPartyID**

   Returnerar tredjeparts-ID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (nullable NSString *) targetThirdPartyID;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *thirdPartyId = [ADBMobile targetThirdPartyID];
      ```

* **targetSetThirdPartyID**

   Anger ID för tredje part.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) targetSetThirdPartyID:(nullable NSString *)thirdPartyID;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile targetSetThirdPartyID:@"thirdPartyID"];
      ```

* **targetClearCookies**

   Tar bort alla målcookies från din app.

   >[!TIP]
   >
   >Sedan version 4.10.0 av SDK använder Target inte längre cookies. Den här metoden återställer thirdPartyID och sessionID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (void) targetClearCookies;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      [ADBMobile targetClearCookies];
      ```

* **targetPcID**

   Returnerar PcID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (nullable NSString *) targetPcID;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *myTargetPcID = [ADBMobile targetPcID];
      ```

* **targetSessionID**

   Returnerar SessionID.

   * Här är syntaxen för den här metoden:

      ```objective-c
      + (nullable NSString *) targetPcID;
      ```

   * Här är kodexemplet för den här metoden:

      ```objective-c
      NSString *myTargetSessionID = [ADBMobile targetSessionID];
      ```

### Exempel

```objective-c
// make your request 
ADBTargetLocationRequest *myRequest =  
 [ADBMobile targetCreateRequestWithName:@"heroBanner"  
                         defaultContent:@"default.png"  
                          parameters:nil]; 
// load your request 
[ADBMobile targetLoadRequest:myRequest  
                    callback:^(NSString *content) { 
                        // do something with content 
                        heroImage.image = [UIImage imageNamed:content];
                    }];
```
