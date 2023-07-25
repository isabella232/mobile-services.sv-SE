---
title: Adobe Mobile Services - frågor och svar
description: Få svar på vanliga frågor om lanseringen av Adobe Mobile Services.
source-git-commit: 0a4e0c9e6172231d8a9f9b561d0a7b7fb230473a
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Adobe Mobile Services - frågor och svar

Adobe Mobile-tjänstens sista giltighetsdatum är **31 december 2022**.

## Vad händer?

Mobiltjänster upphör den 31 december 2022. Mobiltjänster, som har stöd för ett mobilorienterat gränssnitt, förvärv, djuplänkning, meddelanden i appen, push-meddelanden och geopositionering, stöds inte längre efter detta datum.

## Vad ingår och vad ingår inte?

Detta gäller endast Adobe Mobile Services, den fristående plattformen på [mobilemarketing.adobe.com](https://mobilemarketing.adobe.com). SDK:n för mobilversion 4 som använder det här gränssnittet upphörde den 31 augusti 2021.

Den här sista livscykeln innehåller INTE Adobe Analytics för mobilappar, som ingår i Adobe Experience Platform Mobile SDK:er. Dessa funktioner, som bland annat beteenden i appen, livscykelanalys, uppföljning av meddelandeinteraktion och målgruppsprofiler, får fortsatt stöd från Adobe.

## Varför upphör funktionen?

I takt med att Adobe fortsätter att utöka sina funktioner för mobilmarknadsföring kommer funktioner som tidigare fanns i Mobiltjänster att lanseras i Adobe Experience Cloud-lösningar eller erbjudas via Adobe Exchange Premier Partners. Den här övergången ger er kraftfullare och flexiblare funktioner för mobilmarknadsföring.

## Vad händer med befintliga bearbetningsregler som skapats i Mobile Services?

[Bearbetar regler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) som har skapats eller genererats i gränssnittet för mobila tjänster migreras automatiskt till Adobe Analytics innan Mobile Services-tjänstens slutdatum infaller. Flyttade bearbetningsregler fungerar på samma sätt som andra bearbetningsregler i Adobe Analytics, där du fritt kan visa eller redigera dem. Ingen användaråtgärd krävs för den här migreringen.

När Mobile Services är solnedgång hanteras all bearbetningsregellogik exklusivt inom Adobe Analytics, vanligtvis med användning av [Sammanhangsdatavariabler](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html).

## Vilka övergångsalternativ finns?

Adobe erbjuder tre övergångsvägar beroende på hur din organisation använder dem.

1. **Meddelanden och push-meddelanden i appen**: Adobe kan överföra dina arbetsflöden för meddelanden till Adobe Journey Optimizer. Produkten hjälper organisationer att optimera och personalisera upplevelser under hela kundresan, inklusive mobilmeddelanden.
1. **Förvärv och djuplänkning**: Förvärv och djuplänkning erbjuds via programmet Adobe Exchange Premier Partners. Adobe partnerskap kan ta fram lämpliga introduktioner för att säkerställa att ni hittar den lösning som passar era behov bäst.
1. **Platstjänst**: Platstjänsten erbjuder kostnadsfria geografiska platser. Se [Platstjänstdokumentation](https://experienceleague.adobe.com/docs/places/using/home.html).

## Var kan jag gå om jag har frågor?

Se [Adobe Mobile Services - sista sidan i livscykeln Spark](https://spark.adobe.com/page/C6D30y09zaRpD/) för mer information. Kontakta din Adobe-representant om du har ytterligare frågor.
