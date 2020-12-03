---
description: Adobe Target förhämtningsfunktion använder Android Mobile SDK:er för att hämta innehåll så få gånger som möjligt genom att cachelagra serversvaren.
seo-description: Adobe Target förhämtningsfunktion använder Android Mobile SDK:er för att hämta innehåll så få gånger som möjligt genom att cachelagra serversvaren.
seo-title: Förhämta erbjudandeinnehåll i Android
title: Förhämta erbjudandeinnehåll i Android
uuid: 063451b8-e191-4d58-8ed8-1723e310ad1a
translation-type: tm+mt
source-git-commit: fa7375ac8a1345d81748bcf635791c46d3943fed
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 4%

---


# Förhämta erbjudandeinnehåll i Android {#prefetch-offer-content-in-android}

Adobe Target förhämtningsfunktion använder Android Mobile SDK:er för att hämta innehåll så få gånger som möjligt genom att cachelagra serversvaren.

>[!IMPORTANT]
>
>Förhämtningsfunktionen i Mobile SDK för Android stöds inte för aktivitetstyperna Automatiskt mål, Automatisk allokering och Automated Personalization i Adobe Target.

Den här processen minskar inläsningstiden, förhindrar flera nätverksanrop och gör att Adobe Target kan meddelas vilken mbox som mobilappsanvändaren har besökt. Allt innehåll hämtas och cachelagras under förhämtningsanropet, och det här innehållet hämtas från cachen för alla framtida anrop som innehåller cachelagrat innehåll för det angivna mbox-namnet.

Förhämtningsinnehåll bevaras inte vid start. Innehållet i förhämtningen cachas så länge som programmet finns eller tills metoden anropas `clearPrefetchCache()` .

>[!IMPORTANT]
>
>Förhämtnings-API:er för mål har varit tillgängliga sedan SDK-version 4.14.0. Mer information om parameterbegränsningar finns i [Batch-input-parameters](https://developers.adobetarget.com/api/#batch-input-parameters).

I SDK version 4.14 eller senare, om den anges, `environmentId` hämtas filen från `ADBMobileConfig.json` när ett TnT-anrop för en v2-batchruta initieras. Om ingen `environmentId` anges i den här filen skickas ingen miljöparameter i TNT-batchanrop och erbjudandet levereras för standardmiljön.

Exempel:

```java
if (MobileConfig.getInstance().mobileUsingTarget()){ 
            long environmentID = MobileConfig.getInstance().getEnvironmentID(); 
            if(environmentID != 0L){ 
                parametersJson.put(TargetJson.ENVIRONMENT_ID, environmentID); 
            } 
        }
```

## Förhämtningsmetoder {#section_05967F1F3A554B0FBC2C08A954554BDE}

Här är metoder som du kan använda för förhämtning i Android:

* **prefetchContent**

   Skickar en förhämtningsbegäran med en array med platser till den konfigurerade målservern och returnerar begärandestatusen i det tillhandahållna återanropet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void prefetchContent(
      final List<TargetPrefetchObject> targetPrefetchArray,
      final Map<String, Object> profileParameters,
      final TargetCallback<Boolean> callback)
      ```

   * Här är parametrarna för den här metoden:

      * **targetPrefetchArray**

         Array med `TargetPrefetchObjects` namnet och mboxParameters för varje målplats som ska förhämtas.

      * **profileParameters**

         Innehåller nycklar och värden för profilparametrar som ska användas för varje platsförhämtning i den här begäran.

      * **callback**

         Anropas när förhämtningen är klar. Returnerar `true` om förhämtningen lyckades och `false` om förhämtningen misslyckades.

* **loadRequests**

   Kör en gruppbegäran för flera mbox-platser som anges i request-arrayen.  Varje objekt i arrayen innehåller en callback-funktion som anropas när innehållet är tillgängligt för den angivna mbox-platsen.

   >[!IMPORTANT]
   >
   >Om innehållet för de begärda platserna redan har cache-lagrats, returneras det omedelbart i det angivna återanropet. Annars skickar SDK en nätverksbegäran till målservrarna för att hämta innehållet.

   * Här är syntaxen för den här metoden:

      ```java
      public static void loadRequests( final List<TargetRequestObject> requestArray,  final Map<String, Object> profileParameters)
      ```

   * Här är parametrarna för den här metoden:

      * **requestArray**

         En array med `TargetRequestObjects` som innehåller namn, standardinnehåll, parametrar och återanropsfunktion per plats att hämta.

      * **profileParameters**

         Innehåller nycklar och värden för profilparametrar som ska användas för varje platsförhämtning i den här begäran.

* **clearPrefetchCache**

   Raderar data som cachelagrats av Target Prefetch.

   * Här är syntaxen för den här metoden:

      ```java
      public static void clearPrefetchCache();
      ```

   * Det finns inga parametrar för den här metoden.

* **createTargetRequestObject**

   Skapar och returnerar en instans av `TargetRequestObject` med angivna data.

   * Här är syntaxen för den här metoden:

      ```java
      public static TargetPrefetchObject createTargetRequestObject( 
      final String mboxName,
      final String defaultContent, 
      final Map<String, Object> mboxParams, 
      final Map<String, Object> orderParams, 
      final Map<String, Object> productParams, 
      final Target.TargetCallback<String> callback)
      ```

* **createTargetPrefetchObject**

   Skapar och returnerar en instans av TargetPrefetchObject med angivna data.

   * Här är syntaxen för den här metoden:

      ```java
      public static TargetPrefetchObject createTargetPrefetchObject( 
      final String mboxName, 
      final Map<String, Object> mboxParams) 
      final Map<String, Object> orderParams, 
      final Map<String, Object> productParams)
      ```

## Offentliga klasser {#section_A273E53F069E4327BBC8CE4910B37888}

Här är de publika klasserna som stöder förhämtning i Android:

### Klassreferens: TargetPrefetchObject

Kapslar in mbox-namnet och parametrarna som används för mbox-förhämtning.

* **`name`**

   Namnet på den plats som ska förhämtas.
   * **Typ**: Sträng

* `mboxParameters`

   Samling nyckelvärdepar som ska bifogas som `mboxParameters` för `TargetPrefetchObject`begäran.
   * **Typ**: Karta`<String, Object>`

* **`orderParameters`**

   Samling av nyckelvärdepar som ska kopplas till aktuell mbox under ordernoden.
   * **Typ**: Karta `<String, Object>`

* **`productParameters`**

   Samling nyckelvärdepar som ska bifogas till aktuell mbox under produktnoden.

   * **Typ**: Karta `<String, Object>`


### Klassreferens: TargetRequestObject

Den här klassen kapslar in mbox-namnet, standardinnehållet, mbox-parametrar och det returåteranrop som används för begäranden om målplats.

* **`mboxName`**

   Namn på begärd plats.

   * **Typ**: Sträng

* **`mboxParameters`**

   Samling nyckelvärdepar som ska bifogas som `mboxParameters` för detta `TargetRequestObject`.

   * **Typ: Karta`<String, Object>`**

* **`orderParameters`**

   Samling av nyckelvärdepar som ska kopplas till aktuell mbox under ordernoden.

   * **Typ**: Karta `<String, Object>`

* **`productParameters`**

   Samling nyckelvärdepar som ska bifogas till aktuell mbox under produktnoden.

   * **Typ**: Karta `<String, Object>`

* **`defaultContent`**

   Strängvärde som returneras i återanropet om SDK inte kan hämta innehåll från målservrar.

   * **Typ**: Sträng

* **`callback`**

   Funktionspekare som anropas när innehållet för den angivna `TargetRequestObject` är tillgängligt.

   * **Typ**: Target.TargetCallback`<String>`


## Code sample {#section_BF7F49763D254371B4656E17953D520C}

Här är ett exempel på hur du förhämtar innehåll med Android SDK:n:

```java
// When your app launches, prefetch the content for a list of locations. 
// Define the list of mboxes that you want to prefetch. 
List<TargetPrefetchObject> prefetchMboxesList = new ArrayList<>(); 
  
Map<String, Object> mboxParameters1 = new HashMap<>(); 
mboxParameters1.put("status", "platinum"); 
prefetchMboxesList.add(Target.createTargetPrefetchObject("mboxName1", mboxParameters1));

Map<String, Object> mboxParameters2 = new HashMap<>(); 
mboxParameters2.put("userType", "paid"); 
 
List<String> purchasedIds = new ArrayList<String>(); 
purchasedIds.add("34"); 
purchasedIds.add("125");  
Map<String, Object> orderParameters2 = new HashMap<>(); 
orderParameters2.put("id", "ADCKKIM"); 
orderParameters2.put("total", "344.30"); 
orderParameters2.put("purchasedProductIds",  purchasedIds); 
  
Map<String, Object> productParameters2 = new HashMap<>(); 
productParameters2.put("id", "24D3412"); 
productParameters2.put("categoryId","Books"); 
  
prefetchMboxesList.add(Target.createTargetPrefetchObject("mboxName2", mboxParameters2, orderParameters2, productParameters2));

// Define the profile parameters map. 
Map<String, Object> profileParameters = new HashMap<>(); 
profileParameters.put("ageGroup", "20-32");

// Define the target callback for the prefetch call status. 
Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() { 
    @Override 
    public void call(final Boolean status) { 
        // check the returned status for the prefetch call 
    }};

// Call the prefetchContent API. 
Target.prefetchContent(prefetchMboxesList, profileParameters, prefetchStatusCallback);

// When the content is required, you can initiate the locations request. 
// Define the list of target request objects. 
List<TargetRequestObject> locationRequests = new ArrayList<>(); 
  
Target.TargetCallback<String> callback1 = new Target.TargetCallback<String>() { 
    @Override 
    public void call(final String content) { 
        // check the returned content for mboxName1. 
    }}; 
  
locationRequests.add(Target.createTargetRequestObject("mboxName1", "defaultContent1", mboxParameters1, callback1));

Target.TargetCallback<String> callback2 = new Target.TargetCallback<String>() { 
    @Override 
    public void call(final String content) { 
        // check the returned content for mboxName2. 
    }}; 
  
locationRequests.add(Target.createTargetRequestObject("mboxName2", "defaultContent2", mboxParameters2, orderParameters2, productParameters2, callback2)); 
  
// Call the loadRequests API. 
Target.loadRequests(locationRequests, profileParameters); 
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

* `purchasedProducts` använder en ArrayList med strängar.
