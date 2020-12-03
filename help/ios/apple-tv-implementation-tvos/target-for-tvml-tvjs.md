---
description: Du kan utnyttja Adobe Target i dina TVML-/TVJS-appar genom att göra direkta ersättningar av dina XML-filer. Ange områden på sidan som ska ersättas av Target-innehåll med hjälp av det anpassade XML-elementet ADBTarget.
seo-description: Du kan utnyttja Adobe Target i dina TVML-/TVJS-appar genom att göra direkta ersättningar av dina XML-filer. Ange områden på sidan som ska ersättas av Target-innehåll med hjälp av det anpassade XML-elementet ADBTarget.
seo-title: Adobe Target for TVML/TVJS
title: Adobe Target for TVML/TVJS
uuid: afd5a583-5266-43f2-8cb0-0ace89c53a57
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Adobe Target for TVML/TVJS{#adobe-target-for-tvml-tvjs}

Du kan utnyttja Adobe Target i dina TVML-/TVJS-appar genom att göra direkta ersättningar av dina XML-filer. Ange områden på sidan som ska ersättas av Target-innehåll med hjälp av det anpassade XML-elementet ADBTarget.

>[!IMPORTANT]
>
>Innan du använder elementet `ADBTarget` i dina TVML-sidor måste du konfigurera din TVML/TVJS-app så att den använder tvOS SDK. Mer information finns i [Apple TV-implementering med tvOS](/help/ios/apple-tv-implementation-tvos/apple-tv-implementation-tvos.md).

## Komma igång {#section_88445645FD67416EAF6FDC3E3D3F5C33}

1. Identifiera den `.xml` fil där du vill använda målplatsen.
1. Lägg till ett `ADBTarget` element i filen som ett underordnat element till `<document>` elementet.
1. Om Target inte kan hitta din Mbox-plats, eller om det gör en timeout, används värdet mellan dina `<ADBTarget>` - och `</ADBTarget>` -taggar som standardinnehåll.

## Konfigurera din mbox i Target {#section_F2DA140C34B0421D976046F825B23123}

Det returnerade innehållet från Target ersätter allt innehåll mellan `<ADBTarget>` och `</ADBTarget>`inklusive båda `ADBTarget` -taggarna.

>[!TIP]
>
>Du bör planera vad du vill ersätta utifrån detta.

Användningssättet kan vara så enkelt som att ersätta ett strängvärde i en etikett eller så komplext som att ersätta en hel sida.

## Konfigurera ADBTarget-elementet {#section_44A7AEC6FC0648ADAD0BACB57D493AFA}

I elementet `ADBTarget` måste du ange namnet på Mbox i `mbox` egenskapen. Du kan också lägga till anpassade egenskaper i din begäran i `customParameterName="customParameterValue"` formatet.

* **`mbox`**

   Namn på din Mbox-plats.

   * Egenskapstyp: Sträng
   * Den här egenskapen är obligatorisk.

* **`id`**

   Beställnings-ID.

   * Egenskapstyp: Sträng
   * Den här egenskapen är **inte** obligatorisk.

* **`total`**

   Ordersumman.

   * Egenskapstyp: Sträng
   * Den här egenskapen är **inte** obligatorisk.

* **`purchasedProductIds`**

   En kommaavgränsad lista över inköpta produkt-ID:n för den här ordern.

   * Här är kodexemplet för den här egenskapen:


      ```objective-c
      purchasedProductIds="product1,product2,product3" 
      ```

   * Egenskapstyp: Sträng
   * Den här egenskapen är **inte** obligatorisk.

* **`mboxParameters`**

   En lista med nyckelvärdepar för `mboxParameters`. Varje post i den här strängen avgränsas med ett semikolon, och nyckelvärden avgränsas med ett kolon.

   * Här är kodexemplet för den här egenskapen:

      ```objective-c
      mboxParameters="mboxparameterKey:mboxParameterValue;mboxParameterKey1:mboxParameterValue1;mboxParameterKey2:mboxParameterValue2"
      ```

   * Egenskapstyp: Sträng
   * Den här egenskapen är **inte** obligatorisk.

* **`customParameterName`**

   Värdet för den här egenskapen är `customParameterValue`.

   * Egenskapstyp: Sträng
   * Den här egenskapen är **inte** obligatorisk.


## Exempel {#section_6D6D6E8C7FE147168FC30D83CBC06985}

### Exempel 1

I följande exempel används ett `ADBTarget` element på `LandingPage.xml.js` sidan för att ersätta innehållet i en varning:

#### Konfigurera mål

Anta att du har en Mbox-plats med namnet `landingPage` och att erbjudandeinnehållet är inställt på följande:

```objective-c
<title>My cool landing page</title> 
<description>Thanks for coming to my page</description> 
```

#### Konfigurera landingPage.xml.js

* Här är konfigurationen för landingPage.xml.js:

   ```js
   <alertTemplate> 
       <ADBTarget mbox="landingPage">  
           <title>TargetTestPage</title> 
           <description>Load fail or timeout (defaultContent)</description> 
       </ADBTarget>  
   </alertTemplate> 
   ```

* Om begäran till Target lyckas och ditt erbjudandeinnehåll returneras, kommer din sida att resultera i följande:

   ```objective-c
   <alertTemplate> 
       <title>My cool landing page</title> 
       <description>Thanks for coming to my page</description> 
   </alertTemplate>
   ```

* Om målservern inte kan nås eller begäran inte kan nås, kommer sidan att resultera i:

   ```objective-c
   <alertTemplate> 
       <title>TargetTestPage</title> 
       <description>Load fail or timeout (defaultContent)</description> 
   </alertTemplate>
   ```

### Exempel 2

I följande exempel visas hur du lägger till anpassade data i ditt `ADBTarget` element. Med den här metoden kan du skapa villkorsstyrda upplevelser och erbjuda innehåll för den här Mbox-platsen i Target:

```objective-c
<alertTemplate> 
    <ADBTarget mbox="landingPage" customData="custom data" moreCustomData="more custom data"> 
        <title>TargetTestPage</title> 
        <description>Load fail or timeout (defaultContent)</description> 
    </ADBTarget>  
</alertTemplate>
```
