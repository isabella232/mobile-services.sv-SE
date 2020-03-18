---
description: 'null'
seo-description: 'null'
seo-title: Snabbstart för utvecklare
solution: Marketing Cloud,Analytics
title: Snabbstart för utvecklare
topic: Developer and implementation
uuid: b368959b-d985-436e-8b3e-97e355a97951
translation-type: tm+mt
source-git-commit: 19264af3f4a675add6f61c27f4cdaf20033b9bb7

---


# Snabbstart för utvecklare {#developer-quick-start}

Du behöver Visual Studio 2013 eller senare för att implementera SDK.

## Skaffa SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

När du har packat upp [SDK-nedladdningen](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases)får du en separat mapp för varje arkitektur och plattformskombination som stöds. Du kommer också att ha en `ADBMobileConfig.json` fil som förklaras senare i den här handboken.

## Välj rätt version {#section_E53C5AA7D5474824A89BB32C003865A1}

Olika `.dll`/ `.winmd` filer tillhandahålls för varje målplattform (Windows 8.1, Windows Phone 8.1) och den arkitektur som stöds (x86, x64, ARM). Filerna delas upp i en mappstruktur enligt följande:

![](assets/folder-structure.png)

>[!IMPORTANT]
>
>Versionen av `ADBMobile.winmd` återspeglar inte versionen av biblioteket. Filen innehåller bara metadata och har därför ett versionsnummer `.winmd` som fungerar enligt Microsoft (se `255.255.255.255` [Hur lägger jag till sammansättningsinformation för en DLL-fil för en WinRT C++ / CX-komponent?)](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/6bcccaee-aa53-4770-bd5b-1205977f1ca7/how-do-i-add-assembly-information-for-a-winrt-c-cx-component-dll?forum=winappswithnativecode)). Om du vill kontrollera vilken version av biblioteket du använder kontrollerar du den underliggande `ADBMobile.dll` filens version.

## Syntaxskillnader {#section_A02DE120B6D240F5AFFE7509755C4F14}

Windows 8.1 Universal App Store-biblioteket kan användas på flera programmeringsspråk. Exemplen i den här handboken är i WinJS (JavaScript) och kan behöva ändras om du använder ett annat språk. Observera, att när du använder winmd-metoder från winJS (JavaScript), kommer alla metoder automatiskt att få sin första bokstav nedsänkt.

Den största skillnaden mellan implementeringarna är den datastruktur som används för kontextdata.

När du använder SDK i ett WinJS-projekt ska du dessutom använda en tom sträng ( `""` eller `''`) i stället `null` för tomma strängvärden.

## Lägg till biblioteks- och konfigurationsfilen i projektet - C Sharp {#section_93C25D893B4A4CD3B996CF3C5590C8DC}

1. Starta Visual Studio och öppna din lösning.
1. Högerklicka i **lösningsutforskaren****[!UICONTROL References]** och välj **[!UIUCONTROL Lägg till referens]**.

1. Välj rätt version av biblioteket och bläddra till den associerade `ADBMobile.winmd` filen.

   Mer information finns i avsnittet *Välj rätt version* nedan.

1. Klicka på **[!UICONTROL Add]**.

1. Kontrollera att `ADBMobile.winmd` är markerat i **[!UICONTROL Reference Manager]** fönstret och klicka på **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >När du lägger till en referens till ett Windows Phone-program ska du välja `ADBMobile.winmd`det standardfiltret från **[!UICONTROL Component Files]** Alla **filer**.

1. Högerklicka **[!UICONTROL Solution Explorer]** och välj **[!UICONTROL References]** **[!UICONTROL Add Reference]**.

   Hoppa över det här steget om du även har ett C++-projekt i lösningen.

1. Markera på fliken **Windows** till vänster **[!UICONTROL Extensions]** och markera sedan och lägg till **[!UICONTROL Microsoft Visual C++ 2013 Runtime Package for Windows]**.

1. Lägg till följande rad i klassen:

   ```
   using ADBMobile;
   ```

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till din `ADBMobileConfig.json` fil och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json` filen i lösningen och välj **[!UICONTROL Properties]**.

1. Ändra **[!UICONTROL Build Action]** till **[!UICONTROL Content]**.

## Lägg till biblioteks- och konfigurationsfilen i projektet - C++ {#section_A95C1D18F6144F37ADC8F51590F3983E}

1. Starta Visual Studio och öppna din lösning.
1. Högerklicka på projektet i **[!UICONTROL Solution Explorer]** och välj **[!UICONTROL Add]** > **[!UICONTROL References]**.

1. Välj rätt version av biblioteket och lägg sedan till en referens till den associerade `ADBMobile.winmd` filen.

   Mer information finns i avsnittet *Välj rätt version* nedan.

1. Klicka på **[!UICONTROL Add]**.

1. I **[!UICONTROL Reference Manager]** fönstret kontrollerar du att `ADBMobile.winmd` är markerat och klickar på **[!UICONTROL OK]**.

   >[!TIP]
   >
   >När du lägger till en referens till ett Windows Phone-program ska du välja `ADBMobile.winmd`det standardfiltret från **[!UICONTROL Component Files]** Alla **filer**.

1. Lägg till följande rad i klassen:

   ```
   using namespace ADMS::Measurement;
   ```

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` filen och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json` filen i lösningen och välj **[!UICONTROL Properties]**.

1. Gå till **[!UICONTROL General]** fliken, ändra **[!UICONTROL Content]** till **[!UICONTROL Yes]** och klicka på **[!UICONTROL OK]**.

## Lägg till biblioteks- och konfigurationsfilen i projektet - WinJS {#section_FF83113EBF4742AFA929F4AC28F92DB5}

1. Starta Visual Studio och öppna din lösning.
1. I **Solution Explorer** högerklickar du **[!UICONTROL References]** och väljer **[!UICONTROL Add Reference**.

   Mer information finns i *Markera rätt version* nedan.

1. Välj rätt version av biblioteket och bläddra sedan till den associerade `ADBMobile.winmd` filen.

1. Klicka på **[!UICONTROL Add]**.

1. Kontrollera att `ADBMobile.winmd` är markerat i **[!UICONTROL Reference Manager]** fönstret och klicka på **[!UICONTROL OK]**.

   >[!TIP]
   >
   >När du lägger till en referens till ett Windows Phone-program ska du välja `ADBMobile.winmd`det standardfiltret från **[!UICONTROL Component Files]** Alla **filer**.

1. Högerklicka **[!UICONTROL Solution Explorer]** och välj **[!UICONTROL References]** **[!UICONTROL Add Reference]**.

   Hoppa över det här steget om du även har ett C++-projekt i lösningen.

1. Markera **[!UICONTROL Windows]** och lägg till på fliken till vänster **[!UICONTROL Extensions]** **[!UICONTROL Microsoft Visual C++ 2013 Runtime Package for Windows]**.

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` filen och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json]` filen i lösningen och välj **[!UICONTROL Properties]**.

1. Kontrollera att **[!UICONTROL File Properties]** är **[!UICONTROL Package Action]** inställt på **[!UICONTROL Content]**.

   För JavaScript-projekt är filen inställd på **[!UICONTROL Content]** som standard.

## Uppdatera konfigurationsfilen ADBMobleConfig.json {#section_0BC8CC0E4AAD4AC385FA0AEDC3C56AFE}

Filen innehåller globala SDK-inställningar och finns i projektets rot när du har slutfört stegen i `ADBMobileConfig.json` Lägg till biblioteks- och konfigurationsfilen i Project ** -avsnittet. Om din `ADBMobileConfig.json` fil inte har förkonfigurerats av Adobe Mobile Services måste du uppdatera några värden för att komma igång.

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
* **Mål**: `clientCode`
* **Målgruppshantering**: `server`

Mer information finns i [ADBMobileConfig.json-konfiguration](/help/windows-appstore/c-configuration/methods.md).

## Felsökning {#section_3A10376A60394A15BEE483323E0CD4AA}

När du vill aktivera felsökning för SDK måste du ringa `ADBMobile.Config.setDebugLogging(true);`.

För C Sharp- och JS-program måste du aktivera intern kodfelsökning genom att utföra följande steg (intern kodfelsökning är standardinställningen för C++-program):

### C Sharp

Högerklicka på projektet och välj **[!UICONTROL Properties]** > **[!UICONTROL Debug tab]**. I listrutan för felsökning väljer du **[!UICONTROL Native Only]**.

### JS

Högerklicka på projektet och välj **[!UICONTROL Properties]** > **[!UICONTROL Configuration Properties]** > **[!UICONTROL Debug tab]**. Ändra listrutan för felsökningstyp till Endast **internt**.

Så ja! Nu kan du implementera Analytics, Target och Audience Management i din Windows 8.1 Universal App Store-app.
