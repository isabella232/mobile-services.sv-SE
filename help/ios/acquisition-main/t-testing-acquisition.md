---
description: Följande information hjälper dig att skicka en länk till en äldre kampanj som baseras på ett enhets fingeravtryck.
seo-description: Följande information hjälper dig att skicka en länk till en äldre kampanj som baseras på ett enhets fingeravtryck.
seo-title: Testar tidigare förvärv
solution: Experience Cloud,Analytics
title: Testar tidigare förvärv
uuid: e0591f4a-e26b-4fe4-97c1-a6831a926fa5
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---


# Testa tidigare förvärv {#testing-legacy-acquisition}

Följande information hjälper dig att skicka en länk till en äldre kampanj som baseras på ett enhets fingeravtryck.

Om mobilappen ännu inte finns i Google Play kan du välja vilken mobilapp som helst som mål när du skapar kampanjlänken. Detta påverkar bara vilken app förvärvsservern dirigerar om dig till, efter att du klickat på länken för förvärv, inte möjligheten att testa länken för förvärv.

1. Navigera till **[!UICONTROL Use Legacy Acquisition Links]** i Adobe Mobile Services och generera en URL för anskaffningskampanj.

   Mer information finns i [Använda länkar](/help/using/acquisition-main/c-marketing-links-builder/t-create-edit-adobe-links/c-use-legacy-acquisition-links/c-use-legacy-acquisition-links.md)för äldre anskaffning.

1. Klicka på den genererade länken på den mobila enhet som du vill installera appen på.

   Adobe-servrar (`c00.adobe.com`) lagrar fingeravtrycket och dirigerar sedan om till App Store. Appen behöver inte laddas ned för testning.

1. Starta programmet för första gången på samma mobila enhet som du använde i steg 2.

   Det enklaste sättet att se till att detta händer är att ta bort och installera programmet igen.

Kom ihåg följande information:

* Hämtningsservern tillhandahåller en attribueringsmatchning som baseras på IP-adressen och användaragentinformationen som spelades in i länkklicket (steg 2) och när appen startas (steg 3).
* Med HTTP-övervakningsverktyg kan träffar som skickas från appen övervakas för att bekräfta förvärvsattribueringen.

>[!TIP]
>
>Variationer i användaragenten som skickas kan göra att attribueringen misslyckas.
