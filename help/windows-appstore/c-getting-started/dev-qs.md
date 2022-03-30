---
description: Komma igång-artikel för utvecklare
solution: Experience Cloud Services,Analytics
title: Snabbstart för utvecklare
topic-fix: Developer and implementation
uuid: b368959b-d985-436e-8b3e-97e355a97951
exl-id: dd3262b1-e211-4758-9b4a-9dc7c4920c10
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# Snabbstart för utvecklare {#developer-quick-start}

Du behöver Visual Studio 2013 eller senare för att implementera SDK.

## Skaffa SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

När du har packat upp [SDK-nedladdning](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases)har du en separat mapp för varje arkitektur och plattformskombination som stöds. Du får också en `ADBMobileConfig.json` som förklaras senare i den här handboken.

## Välj rätt version {#section_E53C5AA7D5474824A89BB32C003865A1}

Annat `.dll`/ `.winmd` filer tillhandahålls för varje målplattform (Windows 8.1, Windows Phone 8.1) och den arkitektur som stöds (x86, x64, ARM). Filerna delas upp i en mappstruktur enligt följande:

![](assets/folder-structure.png)

>[!IMPORTANT]
>
>Versionen av `ADBMobile.winmd` återspeglar inte versionen av biblioteket. The `.winmd` filen endast innehåller metadata och därför har den ett versionsnummer av `255.255.255.255` vilket beteende som accepteras enligt Microsoft (se [Hur lägger jag till sammansättningsinformation för en DLL-fil för en WinRT C++-/CX-komponent?](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/6bcccaee-aa53-4770-bd5b-1205977f1ca7/how-do-i-add-assembly-information-for-a-winrt-c-cx-component-dll?forum=winappswithnativecode)). Om du vill kontrollera vilken version av biblioteket du använder kontrollerar du versionen av det underliggande `ADBMobile.dll` -fil.

## Syntaxskillnader {#section_A02DE120B6D240F5AFFE7509755C4F14}

App Store-biblioteket för Windows 8.1 Universal kan användas på flera programmeringsspråk. Exemplen i den här handboken är i WinJS (JavaScript) och kan behöva ändras om du använder ett annat språk. Observera, att när du använder winmd-metoder från winJS (JavaScript), kommer alla metoder automatiskt att få sin första bokstav nedsänkt.

Den största skillnaden mellan implementeringarna är den datastruktur som används för kontextdata.

När du använder SDK i ett WinJS-projekt ska du dessutom använda en tom sträng ( `""` eller `''`) istället för `null` för tomma strängvärden.

## Lägg till biblioteks- och konfigurationsfilen i projektet - C Sharp {#section_93C25D893B4A4CD3B996CF3C5590C8DC}

1. Starta Visual Studio och öppna din lösning.
1. I **Solution Explorer**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

1. Välj rätt version av biblioteket och bläddra till den associerade `ADBMobile.winmd` -fil.

   Mer information finns i *Välj rätt version* nedan.

1. Klicka på **[!UICONTROL Add]**.

1. Verifiera att `ADBMobile.winmd` är markerat i **[!UICONTROL Reference Manager]** fönster och klicka **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >När du lägger till en referens till en Windows Phone-app väljer du `ADBMobile.winmd`, ändra standardfilfiltret från **[!UICONTROL Component Files]** till **Alla filer**.

1. I **[!UICONTROL Solution Explorer]**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

   Hoppa över det här steget om du även har ett C++-projekt i lösningen.

1. I **Windows** till vänster väljer du **[!UICONTROL Extensions]**, markera och lägga till **[!UICONTROL Microsoft Visual C++ 2013 Runtime Package for Windows]**.

1. Lägg till följande rad i klassen:

   ```
   using ADBMobile;
   ```

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json` i lösningen och väljer **[!UICONTROL Properties]**.

1. Ändra **[!UICONTROL Build Action]** till **[!UICONTROL Content]**.

## Lägg till biblioteks- och konfigurationsfilen i projektet - C++ {#section_A95C1D18F6144F37ADC8F51590F3983E}

1. Starta Visual Studio och öppna din lösning.
1. I **[!UICONTROL Solution Explorer]**, högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL References]**.

1. Välj rätt version av biblioteket och lägg sedan till en referens till det associerade biblioteket `ADBMobile.winmd` -fil.

   Mer information finns i *Välj rätt version* nedan.

1. Klicka på **[!UICONTROL Add]**.

1. I **[!UICONTROL Reference Manager]** fönster, verifiera att `ADBMobile.winmd` är markerat och klickar **[!UICONTROL OK]**.

   >[!TIP]
   >
   >När du lägger till en referens till en Windows Phone-app väljer du `ADBMobile.winmd`, ändra standardfilfiltret från **[!UICONTROL Component Files]** till **Alla filer**.

1. Lägg till följande rad i klassen:

   ```
   using namespace ADMS::Measurement;
   ```

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json` i lösningen och väljer **[!UICONTROL Properties]**.

1. På **[!UICONTROL General]** flik, ändra **[!UICONTROL Content]** till **[!UICONTROL Yes]** och klicka **[!UICONTROL OK]**.

## Lägg till biblioteks- och konfigurationsfilen i projektet - WinJS {#section_FF83113EBF4742AFA929F4AC28F92DB5}

1. Starta Visual Studio och öppna din lösning.
1. I **Solution Explorer**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

   Mer information finns i *Välj rätt version* nedan.

1. Välj rätt version av biblioteket och bläddra sedan till den associerade `ADBMobile.winmd` -fil.

1. Klicka på **[!UICONTROL Add]**.

1. Verifiera att `ADBMobile.winmd` är markerad i **[!UICONTROL Reference Manager]** fönster och klicka **[!UICONTROL OK]**.

   >[!TIP]
   >
   >När du lägger till en referens till en Windows Phone-app väljer du `ADBMobile.winmd`, ändra standardfilfiltret från **[!UICONTROL Component Files]** till **Alla filer**.

1. I **[!UICONTROL Solution Explorer]**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

   Hoppa över det här steget om du även har ett C++-projekt i lösningen.

1. I **[!UICONTROL Windows]** till vänster väljer du **[!UICONTROL Extensions]** och markera och lägga till **[!UICONTROL Microsoft Visual C++ 2013 Runtime Package for Windows]**.

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json]` i lösningen och väljer **[!UICONTROL Properties]**.

1. Med **[!UICONTROL File Properties]** vald, kontrollera **[!UICONTROL Package Action]** är inställd på **[!UICONTROL Content]**.

   För JavaScript-projekt är filen inställd på **[!UICONTROL Content]** som standard.

## Uppdatera konfigurationsfilen ADBMobleConfig.json {#section_0BC8CC0E4AAD4AC385FA0AEDC3C56AFE}

The `ADBMobileConfig.json` filen innehåller globala SDK-inställningar och finns i projektets rot när du har slutfört stegen i *Lägg till biblioteks- och konfigurationsfilen i projektet* -avsnitt. Om `ADBMobileConfig.json` filen inte har förkonfigurerats av Adobe Mobile Services. Du måste uppdatera några värden för att komma igång.

Följande är ett exempel på en `ADBMobileConfig.json` fil:

```js
{ 
    "version" : "1.0", 
    "analytics" : { 
        "rsids" : "coolApp", 
        "server" : "my.CoolApp.com", 
        "charset" : "UTF-8", 
        "ssl" : true, 
        "offlineEnabled" : true, 
        "lifecycleTimeout" : 300, 
        "privacyDefault" : "optedin", 
        "poi" : [ 
                    ["san francisco",37.757144,-122.44812,7000], 
                    ["santa cruz",36.972935,-122.01725,600] 
                ] 
    }, 
 "target" : { 
  "clientCode" : "myTargetClientCode", 
  "timeout" : 1 
 }, 
 "audienceManager" : { 
  "server" : "myServer.demdex.com" 
 } 
}
```

Uppdatera minst följande värden för de lösningar du använder:

* **Analyser**: `rsids` och `server`
* **Målgrupp**: `clientCode`
* **Målgruppshantering**: `server`

Mer information finns i [ADBMobileConfig.json-konfiguration](/help/windows-appstore/c-configuration/methods.md).

## Felsökning {#section_3A10376A60394A15BEE483323E0CD4AA}

När du vill aktivera felsökning för SDK måste du ringa `ADBMobile.Config.setDebugLogging(true);`.

För C Sharp- och JS-program måste du aktivera intern kodfelsökning genom att utföra följande steg (intern kodfelsökning är standardinställningen för C++-program):

### C Sharp

Högerklicka på projektet och välj **[!UICONTROL Properties]** > **[!UICONTROL Debug tab]**. I listrutan för felsökning väljer du **[!UICONTROL Native Only]**.

### JS

Högerklicka på projektet och välj  **[!UICONTROL Properties]** > **[!UICONTROL Configuration Properties]** > **[!UICONTROL Debug tab]**. Ändra listrutan för felsökningstyp till **Endast inbyggd**.

Så ja! Nu kan du implementera Analytics, Target och Audience Management i din universella App Store-app för Windows 8.1.
