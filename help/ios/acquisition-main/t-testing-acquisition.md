---
description: Följande information hjälper dig att skicka en länk till en äldre kampanj som baseras på ett enhets fingeravtryck.
solution: Experience Cloud Services,Analytics
title: Testar tidigare förvärv
uuid: e0591f4a-e26b-4fe4-97c1-a6831a926fa5
exl-id: 431dc400-952a-4515-9d14-ba2efef4b2c4
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Testa tidigare förvärv {#testing-legacy-acquisition}

Följande information hjälper dig att skicka en länk till en äldre kampanj som baseras på ett enhets fingeravtryck.

Om mobilappen ännu inte finns i Google Play kan du välja vilken mobilapp som helst som mål när du skapar kampanjlänken. Detta påverkar bara vilken app förvärvsservern dirigerar om dig till, efter att du klickat på länken för förvärv, inte möjligheten att testa länken för förvärv.

1. Navigera till **[!UICONTROL Use Legacy Acquisition Links]** i Adobe Mobile Services och generera en webbadress för anskaffningskampanj.

   Mer information finns i [Använd äldre förvärvslänkar](/help/using/acquisition-main/c-marketing-links-builder/t-create-edit-adobe-links/c-use-legacy-acquisition-links/c-use-legacy-acquisition-links.md).

1. Klicka på den genererade länken på den mobila enhet där du vill installera appen.

   Adobe (`c00.adobe.com`) lagra fingeravtrycket och sedan omdirigera till App Store. Appen behöver inte laddas ned för testning.

1. Starta programmet för första gången på samma mobila enhet som du använde i steg 2.

   Det enklaste sättet att se till att detta händer är att ta bort och installera programmet igen.

Kom ihåg följande information:

* Hämtningsservern tillhandahåller en attribueringsmatchning som baseras på IP-adressen och användaragentinformationen som spelades in i länkklicket (steg 2) och när appen startas (steg 3).
* Med HTTP-övervakningsverktyg kan träffar som skickas från appen övervakas för att bekräfta förvärvsattribueringen.

>[!TIP]
>
>Variationer i användaragenten som skickas kan göra att attribueringen misslyckas.
