---
description: Med dessa tillägg kan du enkelt lägga till en referens till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.
seo-description: Med dessa tillägg kan du enkelt lägga till en referens till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.
seo-title: Windows Visual Studio-tillägg för Experience Cloud Solutions 4.x SDK
solution: Marketing Cloud,Analytics
title: Windows Visual Studio-tillägg för Experience Cloud Solutions 4.x SDK
topic: Developer and implementation
uuid: e48faf54-8b08-4224-9d80-e553a983129e
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Windows Visual Studio-tillägg för Experience Cloud Solutions 4.x SDK {#windows-visual-studio-extensions-for-experience-cloud-solutions-x-sdk}

Det här tillägget är ett mycket enklare sätt att lägga till en referens till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.

## Installera biblioteket från GitHub {#section_F55DB6241EF1475286C05FEAEBF996A3}

1. Hämta Windows Universal SDK från [GitHub](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases).
1. Zippa upp den hämtade filen lokalt.
1. Dubbelklicka på **[!UICONTRTOL filen ADBMomobileUniversalWindowsVSIX.vsix]** för att öppna installationsprogrammet.
1. Välj **[!UICONTROL Global Location]** och installera biblioteket.

## Lägg till referenser till ditt projekt {#section_00C14FE9243D4330BE1F4BB56FCF08B1}

1. Öppna ditt Windows 10-projekt.
1. Öppna dialogrutan Referenshanteraren.

   ![](assets/ref_manager.png)

1. På **[!UICONTROL Extensions]** fliken letar du upp och väljer **[UICONTROL Adobe Mobile SDK]**.
1. Klicka **[!UICONTROL OK]** för att spara den.

   Adobe Mobile SDK kommer att läggas till i ditt projekt. Om **[UICONTROL-paketet för Microsoft Visual C++ Runtime]** ännu inte har lagts till läggs det här paketet även till i ditt projekt.

1. Välj en plattformstyp i Configuration Manager och börja testa programmet.

