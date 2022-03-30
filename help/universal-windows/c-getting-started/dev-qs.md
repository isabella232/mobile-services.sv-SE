---
description: Information om hur du implementerar biblioteket för universella Windows-plattformar.
solution: Experience Cloud Services,Analytics
title: Snabbstart för utvecklare
topic-fix: Developer and implementation
uuid: 11c06fcf-d5e4-4858-9a4e-3bf66cdd2a48
exl-id: 28fc2a96-907e-41fc-a798-3e8d43fc7616
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 1%

---

# Snabbstart för utvecklare{#developer-quick-start}

Här finns information om hur du implementerar biblioteket för universella Windows-plattformar.

>[!IMPORTANT]
>
>För att implementera SDK måste du ha Visual Studio 2013 eller senare.

## Skaffa SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

När du har packat upp [SDK-nedladdning](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases) -filen kommer du att ha en separat mapp för varje arkitektur och plattformskombination som stöds. Du får också en `ADBMobileConfig.json` -fil. Mer information om den här filen finns i [Konfigurationsfil för ADBMobileConfig.json](/help/universal-windows/c-configuration/c.json.md).

## Välj rätt version {#section_E53C5AA7D5474824A89BB32C003865A1}

Annat `.dll/.winmd` filer tillhandahålls för varje arkitektur som stöds (x86, x64, ARM).

>[!IMPORTANT]
>
>Versionen av `ADBMobile.winmd` återspeglar inte versionen av biblioteket. The `.winmd` filen innehåller bara metadata och har ett versionsnummer `255.255.255.255`, som är godkänt enligt Microsoft. Mer information finns i [Hur lägger jag till sammansättningsinformation för en DLL-fil för en WinRT C++-/CX-komponent?](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/6bcccaee-aa53-4770-bd5b-1205977f1ca7/how-do-i-add-assembly-information-for-a-winrt-c-cx-component-dll?forum=winappswithnativecode). Om du vill kontrollera vilken version av biblioteket du använder kontrollerar du versionen av det underliggande `ADBMobile.dll` -fil.

## Syntaxskillnader {#section_A02DE120B6D240F5AFFE7509755C4F14}

Det universella Windows-plattformsbiblioteket kan användas på flera programmeringsspråk. Exemplen i den här handboken är i WinJS (JavaScript). Om du använder ett annat språk kan du behöva ändra. När du använder winmd-metoder från winJS får alla metoder automatiskt sin första bokstav nedsänkt.

Den största skillnaden mellan implementeringarna är den datastruktur som används för kontextdata. När du använder SDK i ett WinJS-projekt ska du dessutom använda en tom sträng ( `""` eller `''`) istället för `null` för tomma strängvärden.

## Lägg till biblioteket och konfigurationsfilen i projektet - C# {#section_93C25D893B4A4CD3B996CF3C5590C8DC}

1. Starta Visual Studio och öppna din lösning.
1. I **[!UICONTROL Solution Explorer]**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

1. Välj rätt version av biblioteket och bläddra till den associerade ADBMoble.winmd-filen.

   Mer information finns i *Välj rätt version* på den här sidan.

1. Klicka **Lägg till**.

1. Kontrollera att filen ADBMoble.winmd är incheckad i **[!UICONTROL Reference Manager]** fönster och klicka **[!UICONTROL OK]**.

1. I **[!UICONTROL Solution Explorer]**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

   Om du även har ett C++-projekt i lösningen hoppar du över det här steget.

1. I **[!UICONTROL Windows]** till vänster väljer du **[!UICONTROL Extensions]**, markera och lägga till **[!UICONTROL Visual C++ 2015 Runtime for Universal Windows Platform Apps]**.

1. Lägg till följande rad i klassen:

   ```csharp
   using ADBMobile;
   ```

1. Högerklicka på projektet och klicka på **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json` i lösningen och väljer **[!UICONTROL Properties]**.

1. Ändra **[!UICONTROL Build Action]** till **[!UICONTROL Content]**.

## Lägg till biblioteks- och konfigurationsfilen i projektet - C++ {#section_A95C1D18F6144F37ADC8F51590F3983E}

1. Starta Visual Studio och öppna din lösning.
1. I **[!UICONTROL Solution Explorer]**, högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL References]**.

1. Välj rätt version av biblioteket och lägg till en referens till den associerade ADBMoble.winmd-filen.

   Mer information finns i *Välj rätt version* på den här sidan.

1. Klicka på **[!UICONTROL Add]**.

1. Verifiera att `ADBMobile.winmd` är markerad i **[!UICONTROL Reference Manager]** fönster och klicka **[!UICONTROL OK]**.

1. Lägg till följande rad i klassen:

   ```c++
   using namespace ADBMobile;
   ```

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json` i lösningen och väljer **[!UICONTROL Properties]**.

1. På **[!UICONTROL General]** flik, ändra **[!UICONTROL Content]** till **[!UICONTROL Yes]** och klicka **[!UICONTROL OK]**.

## Lägg till biblioteks- och konfigurationsfilen i projektet - WinJS {#section_FF83113EBF4742AFA929F4AC28F92DB5}

1. Starta Visual Studio och öppna din lösning.

1. I **[!UICONTROL Solution Explorer]**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

1. Välj rätt version av biblioteket och bläddra till den associerade ADBMoble.winmd-filen.

1. Klicka på **[!UICONTROL Add]**.

1. Kontrollera att filen ADBMoble.winmd är incheckad i **[!UICONTROL Reference Manager]** fönster och klicka **[!UICONTROL OK]**.

1. I **[!UICONTROL Solution Explorer]**, högerklicka **[!UICONTROL References]** och markera **[!UICONTROL Add Reference]**.

   Om du även har ett C++-projekt i lösningen hoppar du över det här steget.

1. I **[!UICONTROL Windows]** till vänster väljer du **[!UICONTROL Extensions]** och markera och lägga till **[!UICONTROL Visual C++ 2015 Runtime for Universal Windows Platform Apps]**.

1. Högerklicka på projektet och välj **[!UICONTROL Add]** > **[!UICONTROL Existing Item]**.

1. Bläddra till `ADBMobileConfig.json` och klicka på **[!UICONTROL Add]**.

1. Högerklicka på `ADBMobileConfig.json` i lösningen och väljer **[!UICONTROL Properties]**.

1. Med **[!UICONTROL File Properties]** vald, kontrollera **[!UICONTROL Package Action]** är inställd på **[!UICONTROL Content]**.

   För JavaScript-projekt är filen som standard inställd på Innehåll.

## Uppdatera konfigurationsfilen ADBMobileConfig.json {#section_0BC8CC0E4AAD4AC385FA0AEDC3C56AFE}

The `ADBMobileConfig.json` filen innehåller globala SDK-inställningar och finns i projektets rot när du har slutfört stegen i *Lägg till biblioteks- och konfigurationsfilen i ditt projekt* -avsnitt. Om `ADBMobileConfig.json` filen inte har förkonfigurerats av Adobe Mobile Services. Du måste uppdatera några värden för att komma igång.

Här är ett exempel på en `ADBMobileConfig.json` fil:

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

* **Adobe Analytics**: `rsids` och `server`

* **Adobe Target**: `clientCode`

* **Adobe Audience Manager**: `server`

Mer information finns i [SDK-metoder](/help/universal-windows/c-configuration/methods.md).

## Felsökning {#section_3A10376A60394A15BEE483323E0CD4AA}

Om du vill aktivera felsökning för SDK:n ringer du `ADBMobile.Config.setDebugLogging(true);`.

För C Sharp- och JavaScript-program måste du aktivera intern kodfelsökning genom att utföra följande steg (intern kodfelsökning är standardinställningen för C++-program):

### C Sharp

1. Högerklicka på projektet och klicka på  **[!UICONTROL Properties]** > **[!UICONTROL Debug tab]**.

1. Ändra listrutan för felsökningstyp till **Endast inbyggd**.

### JavaScript

1. Högerklicka på projektet och klicka på **[!UICONTROL Properties]** > **[!UICONTROL Configuration Properties]** > **[!UICONTROL Debug tab]**.

1. Ändra listrutan för felsökningstyp till **[!UICONTROL Native Only]**.

Så ja! Nu kan du implementera Analytics, Target och Audience Management i din universella Windows Platform-app.
