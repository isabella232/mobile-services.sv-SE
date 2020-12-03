---
title: Snabbstart för utvecklare
seo-title: BlackBerry Developer Quick Start for Adobe Mobile Services
description: Med hjälp av snabbstartsguiden för BlackBerry-utvecklare kan du förstå hur du implementerar BlackBerry-biblioteket för Adobe Mobile Services.
seo-description: Med hjälp av snabbstartsguiden för BlackBerry-utvecklare kan du förstå hur du implementerar BlackBerry-biblioteket för Adobe Mobile Services.
translation-type: tm+mt
source-git-commit: 19264af3f4a675add6f61c27f4cdaf20033b9bb7
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---


# Snabbstart för utvecklare

Den här informationen hjälper dig att förstå processen att implementera BlackBerry-biblioteket.

## Skaffa SDK

**SDK kräver BlackBerry 10 eller senare.**

När du har delat upp den hämtade SDK-filen kontrollerar du att följande filer finns i en `AdobeMobile` mapp:

* `Device-Coverage/libADBMobileShared.so`
* `Device-Debug/libADBMobileShared.so`
* `Device-Profile/libADBMobileShared.so`
* `Device-Release/libADBMobileShared.so`
* `public/ADBMediaAnalytics.hpp`
* `public/ADBMediaSharedHeader.hpp`
* `public/ADBMediaState.hpp`
* `public/ADBMobile.hpp`
* `Simulator-Coverage/libADBMobileShared.so`
* `Simulator-Debug/libADBMobileShared.so`
* `Simulator-Profile/libADBMobileShared.so`

## Lägg till SDK:er i ditt projekt

1. Högerklicka på projektet och välj **[!UICONTROL Configure]** > **[!UICONTROL Add Library]**.
1. Markera **[!UICONTROL External library]** och klicka på **[!UICONTROL Next]**.
1. Klicka **[!UICONTROL Browse]** bredvid **[!UICONTROL Device library]** fältet.
1. Navigate to the `ADBMobile-4.0.0BETA-BlackBerry` folder.
1. I `Device-Debug` mappen markerar du `libADBMobileShared.so` och klickar på **[!UICONTROL Open]**.
1. Klicka **[!UICONTROL Browse]** bredvid **[!UICONTROL Simulator library]** fältet.
1. Navigate to the `ADBMobile-4.0.0BETA-BlackBerry` folder.
1. I `Device-Debug` mappen markerar du `libADBMobileShared.so` och klickar på **[!UICONTROL Open]**.
1. Klicka **[!UICONTROL Add]** bredvid **[!UICONTROL Include folders]** fältet.
1. Navigate to the `ADBMobile-4.0.0BETA-BlackBerry` folder.
1. Lägg till `public` mappen i inkluderingsfilerna.
1. I `ADBMobile-4.0.0BETA-BlackBerry` mappen finns det en `.json` konfigurationsfil med namnet `ADBMobileConfig.json`.

   Kopiera filen till projektets rot.
1. Högerklicka på projektet och välj **[!UICONTROL Refresh]**.

   Nu bör `.json` filen vara synlig i din **[!UICONTROL Project Explorer]**.
1. Öppna `bar-descriptor.xml` filen för ditt projekt.
1. Klicka på **[!UICONTROL Assets]** fliken längst ned i fönstret.
1. Bekräfta att du **[!UICONTROL (All Configurations)]** har markerat och klicka sedan på **[!UICONTROL Add Files]** i **[!UICONTROL Assets]** fönsteravsnittet.
   >[!TIP]
   >
   >Det finns ett fel i QNX Momentics-utvecklingsmiljön som ibland förhindrar att de knapparna visas. Om knapparna inte visas ändrar du storlek på fönstren tills de visas.

1. Klicka på **[!UICONTROL Workspace]**.
1. Leta reda på `ADBMobileConfig.json` filen i projektet och klicka på **[!UICONTROL OK]**.

Programmet kan importera klasserna/gränssnitten från `adobeMobileLibrary.jar` biblioteket med hjälp av `#include <ADBMobile.hpp>`.

## Lägg till programbehörigheter

Lägg till raden `bar-descriptor.xml` i projektkatalogen `<permission>access_internet</permission>`eller markera rutan i behörighetsavsnittet på **[!UICONTROL Internet]** **[!UICONTROL Application]** fliken.

## Uppdatera `ADBMobileConfig.json` konfigurationsfilen

Filen `ADBMobileConfig.json` innehåller globala SDK-inställningar. Du måste uppdatera några värden för att komma igång.

Följande är ett exempel på en `ADBMobileConfig.json` fil:

```json
{
    "version" : "1.0",
    "analytics" : {
        "rsids" : "coolApp",
        "server" : "my.CoolApp.com",
        "charset" : "UTF-8",
        "ssl" : true,
        "offlineEnabled" : true,
        "lifecycleTimeout" : 5,
        "privacyDefault" : "optedin",
    }
}
```

Du måste åtminstone uppdatera parametrarna `rsids` och `server` . Mer information finns i [Adobe Mobile-klass och metodreferens](/help/blackberry/methods.md).

Nu kan ni implementera Analytics i er BlackBerry 10-app.
