---
description: Adobe Target förhämtningsfunktion använder iOS Mobile SDK:er för att hämta innehåll så få gånger som möjligt genom att cachelagra serversvaren.
title: Förhämta innehåll i iOS
uuid: fef58042-65e2-4579-b8f1-d21554d2af57
exl-id: 64d43be7-6bd1-4657-8154-5b2c1cbbf42b
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 5%

---

# Förhämta innehåll i iOS {#prefetch-offer-content-in-ios}

Adobe Target förhämtningsfunktion använder iOS Mobile SDK:er för att hämta innehåll så få gånger som möjligt genom att cachelagra serversvaren.

>[!IMPORTANT]
>
>Förhämtningsfunktionen i Mobile SDK för iOS stöds inte för aktivitetstyperna Automatiskt mål, Automatisk allokering och Automated Personalization i Adobe Target.

Den här processen minskar inläsningstiden, förhindrar flera nätverksanrop och gör att Adobe Target kan meddelas vilken mbox som mobilappsanvändaren har besökt. Allt innehåll hämtas och cachelagras under förhämtningsanropet, och det här innehållet hämtas från cachen för alla framtida anrop som innehåller cachelagrat innehåll för det angivna mbox-namnet.

Förhämtningsinnehåll bevaras inte vid start. Förhämtningsinnehållet cachelagras så länge som programmet finns eller tills metoden `clearPrefetchCache()` anropas.

>[!IMPORTANT]
>
>Förhämtnings-API:er för mål har varit tillgängliga sedan SDK-version 4.14.0. Mer information om parameterbegränsningar finns i [Batch Input Parameters](https://developers.adobetarget.com/api/#batch-input-parameters).

Om det anges i SDK version 4.14 eller senare hämtas `environmentId` från `ADBMobileConfig.json`-filen när ett TnT-anrop för v2-batchmbox initieras. Om ingen `environmentId` har angetts i den här filen skickas ingen miljöparameter i TNT-batchanropet och erbjudandet levereras för standardmiljön.

Exempel:

```
if (MobileConfig.getInstance().mobileUsingTarget()){ 
            long environmentID = MobileConfig.getInstance().getEnvironmentID(); 
            if(environmentID != 0L){ 
                parametersJson.put(TargetJson.ENVIRONMENT_ID, environmentID); 
            } 
        }
```

## Förhämtningsmetoder {#section_05967F1F3A554B0FBC2C08A954554BDE}

Här är metoder som du kan använda för förhämtning i iOS:

* **targetPrefetchContent**

   Skickar en förhämtningsbegäran med en array med platser till den konfigurerade målservern och returnerar begärandestatusen i det tillhandahållna återanropet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      (void) targetPrefetchContent:(nonnull NSArray*)targetPrefetchObjectArray 
                     withProfileParameters:(nullable NSDictionary*)profileParameters 
                            callback:(nullable void(^)(BOOL success))callback;
      ```

   * Här är parametrarna för den här metoden:

      * **`targetPrefetchArray`**

         Arrayen `TargetPrefetchObjects` som innehåller namnet och mboxParameters för varje målplats som ska förhämtas.

      * **`profileParameters`**

         Innehåller nycklar och värden för profilparametrar som ska användas för varje platsförhämtning i den här begäran.

      * **`callback`**

         Anropas när förhämtningen är klar. Returnerar `true` om förhämtningen lyckades och `false` om förhämtningen misslyckades.

* **targetLoadRequests**

   Kör en gruppbegäran för flera mbox-platser som anges i request-arrayen. Varje objekt i arrayen innehåller en callback-funktion som anropas när innehållet är tillgängligt för den angivna mbox-platsen.

   >[!IMPORTANT]
   >
   >Om innehållet för de begärda platserna redan har cache-lagrats, returneras det omedelbart i det angivna återanropet. Annars skickar SDK en nätverksbegäran till målservrarna för att hämta innehållet.

   * Här är syntaxen för den här metoden:

      ```objective-c
      (void)targetLoadRequests:(nonnullNSArray*)requests 
               withProfileParameters:(nullableNSDictionary*)profileParameters;
      ```

   * Här är parametrarna för den här metoden:

      * **`requests`**

         Matris `TargetRequestObjects` som innehåller namn, standardinnehåll, parametrar och återanropsfunktion per plats att hämta.

      * **`profileParameters`**

         Innehåller nycklar och värden för profilparametrar som ska användas för varje platsförhämtning i den här begäran.

* **targetPrefetchClearCache**

   Rensar data som cachelagrats av Target Prefetch.

   * Här är syntaxen för den här metoden:

      ```objective-c
      (void) targetPrefetchClearCache; 
      ```

   * Det finns inga parametrar för den här metoden.

* **targetRequestObjectWithName**

   Skapar och returnerar en instans av `TargetRequestObject` med angivna data.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(nullableADBTargetRequestObject*)targetRequestObjectWithName:(nonnullNSString*)name
      defaultContent:(nonnullNSString*)defaultContent
      mboxParameters:(nullableNSDictionary*)mboxParameters
      callback:(nullablevoid(^)(NSString*__nullablecontent))callback;
      ```

   * Det finns inga parametrar för den här metoden.

* **createTargetPrefetchObject**

   Skapar och returnerar en instans av `TargetPrefetchObject` med angivna data.

   * Här är syntaxen för den här metoden:

      ```objective-c
      +(nullable ADBTargetPrefetchObject *) targetPrefetchObjectWithName:(nonnullNSString *)name
      mboxParameters:(nullableNSDictionary *)mboxParameters;
      ```

## Offentliga klasser {#section_A273E53F069E4327BBC8CE4910B37888}

Här är de publika klasserna som har stöd för förhämtning i iOS:

### Klassreferens: TargetPreFetchObject

Kapslar in mbox-namnet och parametrarna som används för mbox-förhämtning.

* **`name`**

   Namn på den plats/mbox som du vill hämta.

   * **Typ**: NSString*

* **`mboxParameters`**

   En valfri ordlista som innehåller nyckelvärdepar för mbox-parametrar.

   * **Typ**: NSDictionary*

* **`orderParameters`**

   Lexikon som innehåller nyckelvärdepar för orderparametrar.

   * **Typ**: NSDictionary*

* **`productParameters`**

   Ordlista som innehåller nyckelvärdepar för produktparametrar.

   * **Typ**: NSDictionary*

### Klassreferens: TargetRequestObject

Den här klassen kapslar in mbox-namnet, standardinnehållet, mbox-parametrar och det returåteranrop som används för begäranden om målplats.

* **`name`**

   Namn på begärd plats.

   * **Typ**: NSString*

* **`mboxParameters`**

   NSString-värdet som representerar namnet på platsen/mbox som du vill hämta.

   * **Typ**: NSString*

* **`defaultContent`**

   Standardinnehållet som returneras om målservrarna inte kan nås.

   * **Typ**: NSString*

* **`callback`**

   När gruppen begär målplatser anropas återanropet när innehåll är tillgängligt för den här platsen.

   * **Typ**: Funktion

## Kodexempel {#section_BF7F49763D254371B4656E17953D520C}

Här följer ett exempel på hur du förhämtar innehåll med iOS SDK:er:

```objective-c
/** 
 * Prefetch Content 
 */ 
  
    NSDictionary *mboxParameters1 = @{@"status":@"platinum"}; 
    NSDictionary *productParameters1 = @{@"id":@"24D3412", 
                                        @"categoryId":@"Books"}; 
    NSDictionary *orderParameters1 = @{@"id":@"ADCKKIM", 
                                      @"total":@"344.30", 
                                      @"purchasedProductIds":@"34, 125, 99"};

    NSDictionary *mboxParameters2 = @{@"userType":@"Paid"}; 
    NSDictionary *productParameters2 = @{@"id":@"764334", 
                                         @"categoryId":@"Online"}; 
  
    NSArray *purchaseIDs = @[@"id1",@"id2"]; 
    NSDictionary *orderParameters2 = @{@"id":@"4t4uxksa", 
                                       @"total":@"54.90", 
                                       @"purchasedProductIds":purchaseIDs};

    // Creating Prefetch Objects 
    ADBTargetPrefetchObject *prefetch1 = [ADBMobile targetPrefetchObjectWithName:@"logo" mboxParameters:mboxParameters1]; 
    prefetch1.productParameters = productParameters1; 
    prefetch1.orderParameters = orderParameters1; 
  
    ADBTargetPrefetchObject *prefetch2 = [ADBMobile targetPrefetchObjectWithName:@"buttonColor" mboxParameters:mboxParameters2]; 
    prefetch2.productParameters = productParameters2; 
    prefetch2.orderParameters = orderParameters2; 

    // Creating prefetch Array 
    NSArray *prefetchArray = @[prefetch1,prefetch2]; 
  
    // Creating Profile parameters 
    NSDictionary *profileParmeters = @{@"age":@"20-32"};

    // Target API Call 
    [ADBMobile targetPrefetchContent:prefetchArray withProfileParameters:profileParmeters callback:^(BOOL isSuccess){ 
       // do something with the Boolean result 
    }];
```

Här är ett exempel på gruppen `loadRequest` med iOS SDK:er:

```objective-c
/** 
 * Batch loadRequest  
 */ 
  
   NSDictionary *mboxParameters1 = @{@"status":@"platinum"}; 
   NSDictionary *productParameters1 = @{@"id":@"24D3412", 
                                        @"categoryId":@"Books"}; 
   NSDictionary *orderParameters1 = @{@"id":@"ADCKKIM", 
                                      @"total":@"344.30", 
                                      @"purchasedProductIds":@"34, 125, 99"};

    NSDictionary *mboxParameters2 = @{@"userType":@"Paid"}; 
    NSDictionary *productParameters2 = @{@"id":@"764334", 
                                         @"categoryId":@"Online"}; 
    NSArray *purchaseIDs = @[@"id1",@"id2"]; 
    NSDictionary *orderParameters2 = @{@"id":@"4t4uxksa", 
                                       @"total":@"54.90", 
                                       @"purchasedProductIds":purchaseIDs};

    ADBTargetRequestObject *request1 = [ADBMobile targetRequestObjectWithName:@"logo" defaultContent:@"BlueWhale" mboxParameters:mboxParameters1 callback:^(NSString *content){ 
        // do something with the received content 
    }]; 
  
    request1.productParameters = productParameters1; 
    request1.orderParameters = orderParameters1;

    ADBTargetRequestObject *request2 = [ADBMobile targetRequestObjectWithName:@"buttonColor" defaultContent:@"red" mboxParameters:mboxParameters2 callback:^(NSString *content){ 
        // do something with the received content 
    }]; 
    request2.productParameters = productParameters1; 
    request2.orderParameters = orderParameters1;

    // create request object array 
    NSArray *requestArray = @[request1,request2]; 
  
    // Call the API 
    [ADBMobile targetLoadRequests:requestArray withProfileParameters:profileParmeters];
```

## Ytterligare information {#section_A454BAD1CD49423E86C71BAEE06125FD}

Här finns ytterligare information om dessa exempel:

* `ProductParameters` tillåter bara följande tangenter:

   * `id`
   * `categoryId`

* `OrderParameters` tillåter bara följande tangenter:

   * `id`
   * `total`
   * `purchasedProductIds`

* `purchasedProducts` använder en array med strängar.
