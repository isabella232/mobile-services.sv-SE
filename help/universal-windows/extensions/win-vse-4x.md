---
description: Med dessa tillägg kan du enklare lägga till referenser till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.
seo-description: Med dessa tillägg kan du enklare lägga till referenser till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.
seo-title: Windows Visual Studio-tillägg för Experience Cloud SDK 4.x
solution: Experience Cloud,Analytics
title: Windows Visual Studio-tillägg för Experience Cloud SDK 4.x
topic-fix: Developer and implementation
uuid: e48faf54-8b08-4224-9d80-e553a983129e
exl-id: 8ed91dc1-8f30-4788-8471-21bb54256b0b
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Windows Visual Studio-tillägg för Experience Cloud SDK 4.x {#windows-visual-studio-extensions-for-experience-cloud-solutions-x-sdk}

Det här tillägget är ett mycket enklare sätt att lägga till en referens för Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.

## Installera biblioteket från GitHub {#section_F55DB6241EF1475286C05FEAEBF996A3}

1. Hämta Windows Universal SDK från [GitHub](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases).
1. Zippa upp den hämtade filen lokalt.
1. Dubbelklicka på **[!UICONTROL ADBMobileUniversalWindowsVSIX.vsix]**-filen för att öppna installationsprogrammet.
1. Välj **[!UICONTROL Global Location]** och installera biblioteket.

## Lägg till referenser till ditt projekt {#section_00C14FE9243D4330BE1F4BB56FCF08B1}

1. Öppna ditt Windows 10-projekt.
1. Öppna dialogrutan Referenshanteraren.

   ![](assets/ref_manager.png)

1. Leta reda på och välj **[!UICONTROL Adobe Mobile SDK]** på fliken **[!UICONTROL Extensions]**.
1. Klicka på **[!UICONTROL OK]** för att spara den.

   Adobe Mobile SDK kommer att läggas till i ditt projekt. Om **[!UICONTROL Microsoft Visual C++ Runtime]**-paketet ännu inte har lagts till läggs det här paketet även till i ditt projekt.

1. Välj en plattformstyp i Configuration Manager och börja testa programmet.
