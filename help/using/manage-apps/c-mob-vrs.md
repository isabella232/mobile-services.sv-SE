---
description: En virtuell rapportsvit (VRS) är en rapportsserie som skapas genom att en eller flera segmentdefinitioner tillämpas på en rapportsvit. På så sätt kan användare underhålla sina data i en rapportserie men hantera data som om de fanns i separata rapportsviter.
title: Virtual Report Suites
uuid: 3f467cad-43e7-4cd0-889b-89f8c61febbd
exl-id: c9ce7f7c-2023-4a9d-9e4d-bacc21f9ad40
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 4%

---

# Virtuella rapportsviter {#virtual-report-suites}

En virtuell rapportsvit (VRS) är en rapportsserie som skapas genom att en eller flera segmentdefinitioner tillämpas på en rapportsvit. På så sätt kan användare underhålla sina data i en rapportserie, men hantera data som om de fanns i separata rapportsviter.

Appar som använder VRS gör samma sak som appar som använder en vanlig rapportserie, förutom att hantera följande funktioner:

* Behandlingsregler
* eVars/props/listvars/events
* Tidsstämpelaktiverat alternativ
* Dimension-flaggor (livscykel, plats osv.)
* Klassificeringar

Dessa värden hanteras i den överordnade rapportsviten och delas med de VRS som tillhör samma överordnade rapportsvit.

Följande områden är tillgängliga i användargränssnittet för mobila tjänster i Adobe, oberoende av den överordnade rapportsviten:

* Konfigurationsfilen
* Hantera intressepunkter
* Hantera länkmål
* Hantera återanslående
* Meddelandelänkar
* Förvärv

Ett VRS kan hjälpa dig att utföra följande uppgifter:

* Begränsa dataåtkomst

   Ett multi-nationellt företag har en app som skickar data till en rapportsvit för alla geografiska platser. Företaget vill dock begränsa affärsanvändaren i en region från att visa data i en annan region. Företagets administratör kan skapa ett VRS för att segmentera användare efter region och ge tillstånd till det VRS endast till den affärsanvändare som hanterar regionen.

   Den här begränsningen förhindrar affärsanvändare att visa data som inte är relaterade till deras region. En affärsanvändare i EMEA behöver till exempel inte se data för APAC-regionen.

* Möjliggör kontroll över meddelanden i appen/push, POI, inköp och återanslående med alla data som skickas till en rapportserie.

   Ett flernationellt företag vill att alla data ska skickas till samma rapportsserie för alla geografiska platser. Företaget vill dock att marknadsföringsteamet från varje region ska hantera sina egna meddelanden i appen/push. Företagets administratör kan skapa regionala VRS och varje team kan hantera sina egna appar baserat på det VRS.

   Det regionala teamet bygger sin app med hjälp av konfigurationsfilen från VRS. Data skickas till den överordnade rapportsviten, men meddelanden i appen/push, POI, värvning och återanslående styrs i appen som skapades från VRS.

## Skapa en virtuell rapportsvit i Adobe Analytics {#section_D56B90B2653847D68ECA1F9B39204330}

>[!IMPORTANT]
>
>Endast Adobe Analytics-administratörer kan skapa och ändra virtuella rapportsviter i Adobe Analytics. Mer information om hur du skapar en virtuell rapportserie finns i [Skapa virtuella rapportsviter](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-workflow/vrs-create.html) i Adobe Analytics-dokumentationen.

Varje VRS har ett unikt ID. Om du vill visa det överordnade rapportsvitens-ID i användargränssnittet för Adobe Mobile Services klickar du på **[!UICONTROL More Details]** på sidan Hantera appinställningar i avsnittet **[!UICONTROL App Information]**.

I användargränssnittet för Adobe-mobiltjänster kan du använda ett VRS-system för att skapa en app och segmentera data till en viss grupp i organisationen. På så sätt kan t.ex. en affärsanvändare i Spanien inte se de data som är relevanta för en affärsanvändare i Japan.

>[!TIP]
>
>Du kan inte ändra de värden som ärvs från den överordnade rapportsviten.

Ett VRS är en segmentdefinition på serversidan som är kopplad till en överordnad rapportserie. Därför kan du inte samla in data till ett VRS eftersom SDK endast skickar träffar till den överordnade rapportsviten, som i sin tur registrerar träffar.

## Virtuellt rapportpaket för Adobe Mobile Services och datainsamling {#section_8ED8FBA5B44044D9ABC2151A39C577D4}

I Adobe Mobile Services kan du skapa en app som baseras på en överordnad rapportsvit eller en virtuell rapportsvit. När du skapar en app som baseras på en virtuell rapportserie rekommenderar vi att du justerar VRS-segmentet med definitionen av appen.

>[!TIP]
>
>Push-certifieringar bifogas på appnivå i gränssnittet för mobila tjänster.

För att dina push-meddelanden ska kunna skickas korrekt måste målgruppssegmentet definieras korrekt. Mer information finns i [Målgrupp: Definiera och konfigurera målgruppssegment för push-meddelanden](/help/using/in-app-messaging/t-create-push-message/c-audience-push-message.md).

## Förstå tidszoner {#section_498E1EED22D741C3BDED44F01FACA72A}

Tidszonsegenskapen på sidan Hantera programinställningar skiljer sig från tidszonsegenskapen som du använder för att skapa VRS i Adobe Analytics. Egenskapen på sidan Hantera programinställningar ärvs från den överordnade rapportsviten, som används för att skicka data till Adobe Analytics. Den egenskap du anger när du skapar VRS i Adobe Analytics används för att visa rapporter i gränssnittet för mobila tjänster och kan skilja sig från den överordnade rapportsviten.

## Välj en virtuell rapportsvit i gränssnittet för mobila tjänster {#section_3212D0FC01FD43DCAF30FBAA354CD6E4}

Om du vill använda ett VRS-system när du skapar ett program väljer du VRS i listrutan **[!UICONTROL Report Suite]** på sidan Appinformation. Den här listan innehåller överordnade och virtuella rapporteringsprogram.

>[!IMPORTANT]
>
>Om du vill välja ett VRS-system från listan letar du reda på ett alternativ med den blå punkten och namnkonventionen `vrs_` *`<company_name>`* `_` *`<unique name>`*.

## Egenskaper för Virtual Report Suite {#section_20ECE6243F664C4FB4347ADB4FF0458A}

Här är egenskaperna för VRS:

>[!TIP]
>
>De skrivskyddade egenskaperna ärvs från den överordnade rapportsviten.

| Egenskap | Ärvs från huvudrapporteringssviten | Redigerbar? | Anteckningar |
|--- |--- |--- |--- |
| `target.clientCode` | Nej | Ja |  |
| `target.timeout` | Nej | Ja |  |
| `audienceManager.server` | Nej | Ja |  |
| `audienceManager.analyticsForwardingEnabled` | Ja | Ja |  |
| `audienceManager.timeout` | Nej | Ja |  |
| `acquisition.server` | Nej | Nej |  |
| `acquisition.appid` | Nej | Nej |  |
| `analytics.rsids` | Ja | Nej |  |
| `analytics.server` | Nej | Nej |  |
| `analytics.ssl` | Nej | Ja |  |
| `analytics.offlineEnabled` | Ja |  |  |
| `analytics.charset` | Ja | Nej |  |
| `analytics.lifecycleTimeout` | Nej | Ja | Bör vara den överordnade rapporteringssviten om användarna inte vill att deras data ska vara inkonsekventa. |
| `analytics.privacyDefault` | Nej | Ja |  |
| `analytics.batchLimit` | Nej | Ja |  |
| `analytics.timezone` | Ja | Ja, när du först skapar appen. | Den här tidszonsegenskapen används för att skicka data till Adobe Analytics och skiljer sig från tidszonsegenskapen som ställs in när ett VRS skapas. |
| `analytics.timezoneOffset` | Ja | Nej |  |
| `analytics.referrerTimeout` | Nej | Ja |  |
| `analytics.backdateSessionInfo` | Ja | Ja |  |

## Ytterligare information {#section_4C4446F1FBE64F659BC0A2362C9F3E59}

Här är ytterligare information om virtuella rapportsviter:

* Mer information om VRS finns i [Översikt över virtuella rapportsviter](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-about.html).
* Mer information om planering av VRS-implementering finns i [Arbetsflöde för virtuell rapportsvit](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-workflow/vrs-workflow.html).
