---
description: Slutför följande krav innan du kan använda förvärvslänkar.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Förutsättningar för värvning
topic-fix: Metrics
uuid: a224499a-5a51-4ca5-a37b-06792b774671
exl-id: 31201bec-e823-47b1-8912-2f8d69cea5be
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---

# Förutsättningar för värvning{#acquisition-prerequisites}

Slutför följande krav innan du använder hämtningslänkar.

För att spåra marknadslänkar måste du uppfylla följande krav:

1. Se till att du har ett rapporteringsprogram för mobilappar.

   Du måste skapa en ny rapportserie för mobilappar eller ha en befintlig rapportsvit som kan samla in, spåra och rapportera data som samlas in från dina Marketing Links. Mer information om hur du skapar en ny rapportserie för mobilappar finns i [Lägg till en ny app](/help/using/manage-apps/t-new-app.md).

1. Verifiera din SDK-version.

   Den senaste funktionen för spårning av Marketing Link kräver SDK version 4.9 eller senare.

   **Funktioner som stöds**

   | SDK-version | [Legacy Acquisition Builder](/help/using/acquisition-main/c-marketing-links-builder/t-create-edit-adobe-links/c-use-legacy-acquisition-links/c-use-legacy-acquisition-links.md) | [Manuell länkning](/help/using/acquisition-main/c-marketing-links-builder/acquisition-link-manual.md) | [Marketing Links Builder](/help/using/acquisition-main/c-marketing-links-builder/c-marketing-links-builder.md) |
   |--- |--- |--- |--- |
   | 4.1 till 4.5 | Ja | Nej | Nej |
   | 4.6 till 4.9 | Ja | Ja | Nej |
   | 4.9 eller senare | Ja | Ja | Ja |

1. Aktivera alternativ för SDK-förvärv

   Spårning måste vara aktiverat i SDK-konfigurationen innan länkar kan spåras och rapporteras på. Mer information finns i [Konfigurera värvning](/help/using/acquisition-main/t-enable-acquisition.md).

1. Lägg till App Store-appar

   Du måste lägga till appen från Apple App Store eller från Google Play. Mer information finns i [Lägg till en app från en appbutik](/help/using/manage-apps/c-app-store/t-app-store-app.md).
