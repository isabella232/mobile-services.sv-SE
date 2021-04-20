---
description: Den här informationen hjälper dig att arbeta med ATS (App Transport Security), som är en ny uppsättning säkerhetskrav för iOS 9.
seo-description: Den här informationen hjälper dig att arbeta med ATS (App Transport Security), som är en ny uppsättning säkerhetskrav för iOS 9.
seo-title: Transportsäkerhet för appar
solution: Experience Cloud,Analytics
title: Transportsäkerhet för appar
topic-fix: Developer and implementation
uuid: e9ee13cf-9802-492e-8b11-95f028e34e61
exl-id: 2fe94e76-06d6-4ad1-95ba-193ae3df4d58
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---

# App Transport Security {#app-transport-security}

Den här informationen hjälper dig att arbeta med ATS (App Transport Security), som är en ny uppsättning säkerhetskrav för iOS 9.

Från och med iOS 9 introducerade Apple transportsäkerhet för appar, en uppsättning krav som uppfyller bästa praxis för säkra anslutningar. Mer information finns i *NSAppTransportSecurity* i [Key Reference for Information Property List](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/).

Om du vill att Adobe Mobile SDK version 4.7 eller senare ska fungera sömlöst med ATS använder du alternativet Aktivera SSL på sidan Hantera appinställningar. Mer information finns i [Hantera appinställningar](/help/using/c-manage-app-settings/c-manage-app-settings.md) eller [ADBMomobile JSON-konfiguration](/help/ios/configuration/json-config/json-config.md).

Genom att välja alternativet **[!UICONTROL Use HTTPS]** på sidan Hantera appinställningar i Adobe Mobile Services skickas alla träffar från Analytics, Audience Manager, Target och Adobe Experience Platform Identity Services via HTTPS.

Du kan också placera följande servrar i listan över tillåtna servrar:

| Produkt | Instruktioner |
|--- |--- |
| Analytics  | Om du vill tillåta Analytics-servern lägger du till din spårningsserverdomän i filen info.plist som en undantagsdomän för ATS.  Spårningsserverdomänen finns i avsnittet Analytics (Analyser) i filen `ADBMobileConfig.json` eller i avsnittet Analytics (Analyser) på sidan Manage App Settings (Hantera appinställningar). |
| Audience Manager | Din Audience Manager-domän finns i egenskapen server för ditt publikenManager-objekt i din `ADBMobileConfig.json`-fil.  Om du använder Audience Manager i din app och SSL inte är aktiverat lägger du till den här servern som en undantagsdomän för ATS i din `Info.plist`-fil |
| Målgrupp | Du kan lägga till målslutpunkten i Info.plist-filen som en undantagsdomän för ATS.  Om du vill hitta målslutpunkten söker du efter `clientCodeproperty` i målobjektet för `ADBMobileConfig.json`-filen. Slutpunkten blir `https://{clientCode}.tt.omtrdc.net`.  Om din `clientCodeproperty` till exempel är `“myCompany”` blir slutpunkten `https://myCompany.tt.omtrdc.net`. |
| Adobe Experience Platform Identity Service | Du kan lägga till Experience Cloud-servern som en undantagsdomän för ATS i din `Info.plist`-fil. Den här domänen är `dpm.demdex.net`. |
| Mobiltjänster: Förvärv | Tillåt förvärvsservern som en undantagsdomän för ATS i din `Info.plist`-fil. Den här domänen är `c00.adobe.com`. |
| Mobiltjänster: Meddelanden i appen | Om du använder meddelanden i appen kan du behöva lägga till poster i undantagsdomänen för ATS för varje URL som du använder som inte är HTTPS. Den här listan innehåller värdbaserade bilder och URL:er som är inbäddade i ditt anpassade helskärmsmeddelande i HTML.  Mer information om hur du konfigurerar undantagsdomäner i en `info.plist`-fil finns i *NSExceptionDomains*-raden i *Tabell 2: Primära nycklar för App Transport Security-ordlista*. Se även *Table 3 Exception domains dictionary keys* i [Information Property List Key Reference](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/). |

>[!TIP]
>
>Dessa överväganden påverkar anslutningarna som görs av Adobe Mobile SDK och påverkar inte webbvyn eller andra anslutningar som görs av din app.
