---
description: Med dessa tillägg kan du enklare lägga till referenser till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.
seo-description: Med dessa tillägg kan du enklare lägga till referenser till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.
seo-title: Windows Visual Studio-tillägg för Experience Cloud SDK 4.x
solution: Experience Cloud,Analytics
title: Windows Visual Studio-tillägg för Experience Cloud SDK 4.x
topic: Developer and implementation
uuid: 7d0ea312-340b-46ea-a737-b70a6766a536
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Windows Visual Studio-tillägg för Experience Cloud SDK 4.x {#windows-visual-studio-extensions-for-experience-cloud-solutions-x-sdk}

Med dessa tillägg kan du enklare lägga till referenser till Windows SDK för Experience Cloud Solutions 4.x i ditt projekt.

## Installera biblioteket från GitHub {#section_F55DB6241EF1475286C05FEAEBF996A3}

1. Hämta Windows Universal SDK från [GitHub](https://github.com/Adobe-Marketing-Cloud/mobile-services/releases).
1. Zippa upp den hämtade filen lokalt.
1. Dubbelklicka på filen ADBMmobileWindowsStoreVSIX.vsix eller ADBMomobileWindowsPhoneVSIX.vsix för att öppna installationsprogrammet.

1. Välj **[!UICONTROL Global Location]** och installera biblioteket.

## Lägg till referenser till ditt projekt {#section_00C14FE9243D4330BE1F4BB56FCF08B1}

1. Öppna ditt Windows 8.1- eller Windows Phone 8.1-projekt.
1. Öppna dialogrutan Referenshanteraren.

   ![](assets/ref_manager.png)

1. På fliken **[!UICONTROL Extensions]** i Windows 8.1 eller Windows Phone 8.1 letar du upp och väljer **[!UICONTROL Adobe Mobile SDK]**.
1. Klicka **[!UICONTROL OK]** för att spara den.

   Adobe Mobile SDK läggs till i ditt projekt, och om det inte redan har lagts till läggs även paketet till **[!UICONTROL Microsoft Visual C++ Runtime]** .

1. Välj en plattformstyp i Configuration Manager och börja testa programmet.

