---
title: Snabbstart för utvecklare
description: Med hjälp av snabbstartsguiden för BlackBerry-utvecklare kan du förstå hur du implementerar BlackBerry-biblioteket för Adobe Mobile Services.
exl-id: 65f39667-541a-4bbd-af9b-823638aa6f42
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---

# Snabbstart för utvecklare

Den här informationen hjälper dig att förstå processen att implementera BlackBerry-biblioteket.

## Skaffa SDK

**SDK kräver BlackBerry 10 eller senare.**

När du har delat upp den hämtade SDK-filen kontrollerar du att följande filer finns i en `AdobeMobile`-mapp:

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
1. Klicka på **[!UICONTROL Browse]** bredvid fältet **[!UICONTROL Device library]**.
1. Navigera till mappen `ADBMobile-4.0.0BETA-BlackBerry`.
1. I mappen `Device-Debug` väljer du `libADBMobileShared.so` och klickar på **[!UICONTROL Open]**.
1. Klicka på **[!UICONTROL Browse]** bredvid fältet **[!UICONTROL Simulator library]**.
1. Navigera till mappen `ADBMobile-4.0.0BETA-BlackBerry`.
1. I mappen `Device-Debug` väljer du `libADBMobileShared.so` och klickar på **[!UICONTROL Open]**.
1. Klicka på **[!UICONTROL Add]** bredvid fältet **[!UICONTROL Include folders]**.
1. Navigera till mappen `ADBMobile-4.0.0BETA-BlackBerry`.
1. Lägg till mappen `public` i inkluderingsfilerna.
1. I mappen `ADBMobile-4.0.0BETA-BlackBerry` finns det en `.json`-konfigurationsfil med namnet `ADBMobileConfig.json`.

   Kopiera filen till projektets rot.
1. Högerklicka på projektet och välj **[!UICONTROL Refresh]**.

   Filen `.json` ska nu vara synlig i din **[!UICONTROL Project Explorer]**.
1. Öppna `bar-descriptor.xml`-filen för ditt projekt.
1. Välj fliken **[!UICONTROL Assets]** längst ned i fönstret.
1. Bekräfta att **[!UICONTROL (All Configurations)]** är markerat och klicka sedan på **[!UICONTROL Add Files]** i **[!UICONTROL Assets]**-avsnittet i fönstret.
   >[!TIP]
   >
   >Det finns ett fel i QNX Momentics-utvecklingsmiljön som ibland förhindrar att de knapparna visas. Om knapparna inte visas ändrar du storlek på fönstren tills de visas.

1. Klicka på **[!UICONTROL Workspace]**.
1. Leta reda på filen `ADBMobileConfig.json` i ditt projekt och klicka på **[!UICONTROL OK]**.

Programmet kan importera klasserna/gränssnitten från `adobeMobileLibrary.jar`-biblioteket med `#include <ADBMobile.hpp>`.

## Lägg till programbehörigheter

I `bar-descriptor.xml` i projektkatalogen lägger du till raden `<permission>access_internet</permission>`, eller i QNX Momentics IDE markerar du rutan **[!UICONTROL Internet]** i behörighetsavsnittet på fliken **[!UICONTROL Application]**.

## Uppdatera konfigurationsfilen `ADBMobileConfig.json`

Filen `ADBMobileConfig.json` innehåller globala SDK-inställningar. Du måste uppdatera några värden för att komma igång.

Följande är ett exempel på en `ADBMobileConfig.json`-fil:

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

Du måste åtminstone uppdatera parametrarna `rsids` och `server`. Mer information finns i [Adobe Mobile class and method reference](/help/blackberry/methods.md).

Nu kan ni implementera Analytics i er BlackBerry 10-app.
