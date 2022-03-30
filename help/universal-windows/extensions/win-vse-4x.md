---
description: Med dessa tillägg kan du enklare lägga till referenser till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.
solution: Experience Cloud Services,Analytics
title: Windows Visual Studio-tillägg för Experience Cloud SDK 4.x
topic-fix: Developer and implementation
uuid: e48faf54-8b08-4224-9d80-e553a983129e
exl-id: 8ed91dc1-8f30-4788-8471-21bb54256b0b
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Windows Visual Studio-tillägg för Experience Cloud SDK 4.x {#windows-visual-studio-extensions-for-experience-cloud-solutions-x-sdk}

Det här tillägget är ett mycket enklare sätt att lägga till en referens för Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.

## Installera biblioteket från GitHub {#section_F55DB6241EF1475286C05FEAEBF996A3}

1. Hämta Windows Universal SDK från [GitHub](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases).
1. Zippa upp den hämtade filen lokalt.
1. Dubbelklicka på **[!UICONTROL ADBMobileUniversalWindowsVSIX.vsix]** för att öppna installationsprogrammet.
1. Välj **[!UICONTROL Global Location]** och installera biblioteket.

## Lägg till referenser till ditt projekt {#section_00C14FE9243D4330BE1F4BB56FCF08B1}

1. Öppna ditt Windows 10-projekt.
1. Öppna dialogrutan Referenshanteraren.

   ![](assets/ref_manager.png)

1. På **[!UICONTROL Extensions]** flik, leta upp och markera **[!UICONTROL Adobe Mobile SDK]**.
1. Klicka **[!UICONTROL OK]** för att spara den.

   Adobe Mobile SDK kommer att läggas till i ditt projekt. Om **[!UICONTROL Microsoft Visual C++ Runtime]** paketet har inte lagts till ännu. Paketet läggs också till i projektet.

1. Välj en plattformstyp i Configuration Manager och börja testa programmet.
