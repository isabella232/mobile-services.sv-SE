---
description: Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.
seo-description: Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.
seo-title: Spåra programkrascher
solution: Marketing Cloud,Analytics
title: Spåra programkrascher
topic: Developer and implementation
uuid: 4f81988b-198a-4ba9-ad53-78af90e43856
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Spåra programkrascher {#track-app-crashes}

Den här informationen hjälper dig att förstå hur krascher spåras och de bästa sätten att hantera falska krascher.

>[!IMPORTANT]
>
>Du bör uppgradera till iOS SDK version 4.8.6, som innehåller viktiga ändringar som förhindrar att falska krascher rapporteras.

## När rapporterar Adobe om en krasch?

Om ditt program avslutas utan att först ha bakgrundskorrierats rapporterar SDK att det kraschar nästa gång ditt program startas.

## Hur fungerar kraschrapportering?

iOS använder systemmeddelanden som gör att utvecklare kan spåra och svara på olika tillstånd och händelser under programmets livscykel.

Adobe Mobile iOS SDK har en meddelandehanterare som svarar på `UIApplicationDidEnterBackgroundNotification` meddelandet. I den här koden anges ett värde som anger att användaren har bakomliggande app. Om värdet inte hittas vid en efterföljande start rapporteras en krasch.

## Varför kraschar Adobes mått på krascher på det här sättet?

Den här metoden för att mäta krascher ger ett högnivåsvar på frågan: *Avslutade användaren min app avsiktligt?*

Kraschrapporteringsbibliotek från företag som Apteligent (tidigare Crittercism) använder en global `NSException` hanterare för att ge mer detaljerad kraschrapportering. Ditt program får inte ha fler än en sådan hanterare. Adobe bestämde sig för att inte implementera en global `NSException` hanterare för att förhindra byggfel i vetskapen om att våra kunder kanske använder andra leverantörer av kraschrapportering.

## Vad kan orsaka en falsk krasch?

Följande scenarier kan felaktigt orsaka en krasch som rapporteras av SDK:

* Om du felsöker med Xcode kraschar programmet om det startas igen när det är i förgrunden.

   >[!TIP]
   >
   >Du kan undvika en krasch i det här scenariot genom att göra en bakomliggande omgång av programmet innan du startar programmet igen från Xcode.

* Om appen finns i bakgrunden och skickar Analytics-träffar via ett annat anrop än `trackActionFromBackground`, `trackLocation`eller `trackBeacon`så avslutas appen (manuellt eller av operativsystemet) när den är i bakgrunden, och nästa start blir en krasch.

   >[!TIP]
   >
   >Bakgrundsaktivitet som ligger utanför tröskelvärdet kan också resultera i en ytterligare false-start. `lifecycleTimeout`

* Om appen startas i bakgrunden på grund av en bakgrundshämtning, platsuppdatering osv. och avslutas av operativsystemet utan att gå till förgrunden, kraschar nästa start (bakgrund eller förgrund).
* Om du tar bort Adobes pause-flagga från `NSUserDefaults`, medan appen är i bakgrunden, kraschar nästa start eller cv.

## Hur kan jag förhindra att falska krascher rapporteras?

Följande tillvägagångssätt kan hjälpa dig att förhindra att falska krascher rapporteras:

* I iOS SDK 4.8.6 lades kod till för att bättre avgöra om en ny livscykelsession verkligen är önskvärd.

   Den här koden åtgärdar falska krascher #2 och #3 i föregående avsnitt.

* Se till att du utför din utveckling mot icke-produktionsbaserade rapportsviter, som bör förhindra att fel krasch 1 inträffar.
* Ta inte bort eller ändra inga värden som AdobeMobile SDK anger `NSUserDefaults`.

   Om dessa värden ändras utanför SDK blir de rapporterade data ogiltiga.
