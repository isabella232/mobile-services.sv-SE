---
description: The Technology report allows you to see the different device types, operating systems, operating system versions, and mobile carriers on which your app is being used.
keywords: mobil
solution: Experience Cloud Services,Analytics
title: Teknikrapport
topic-fix: Reports,Metrics
uuid: 4b7322c4-8920-43cd-bb72-5a5bd515ae84
exl-id: 767c1538-68b1-4193-bd3d-3eb80e5b36f7
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Technology report {#technology}

The **[!UICONTROL Technology]** kan du se de olika enhetstyper, operativsystem, operativsystemversioner och mobiloperatörer som appen används på.

Den här rapporten innehåller en solbränsvisualisering för era befintliga data, och du kan använda rapporten för att identifiera målgruppssegment (samlingar av besökare) för målinriktning. Creating and managing audiences is similar to creating and using segments, except that you can make the audiences available in the  Experience Cloud.

## Navigation and Usage {#section_83CA60E1AE6245FEBCBFF3205615C4DF}

Den här visualiseringen innehåller till exempel basrapporten och uppdelningar, använder höjd för att visa måtten i fokus och prestandaskillnaderna mellan mätvärdena. Varje ring representerar ett målgruppssegment i ringens kategori. Du kan vidta åtgärder för en viss målgrupp, till exempel använda ett klisterfilter, dölja ett mätvärde och visa mätvärden.

>[!TIP]
>
>Förutom den här informationen kan du se en självstudiekurs i produkten som beskriver hur du interagerar med soldiagram. To start the tutorial, click **[!UICONTROL Technology Breakdown]** in the title bar of the report, click **[!UICONTROL Customize]**, and click the **[!UICONTROL i]** icon.

![](assets/report_technology.png)

Soldiagram är interaktivt och du kan utföra följande uppgifter:

* Mouse over the any part of the chart to display more information.
* Change the time period by clicking the **[!UICONTROL Calendar]** icon.
* Klicka på ett segment i ringen för att välja den målgrupp där du kan utföra åtgärder, som att zooma in, dölja målgrupper, skapa meddelanden i appen eller ett klisterfilter.
* I det övre högra hörnet väljer du **[!UICONTROL Device Type]** och **[!UICONTROL Device]** för att visa information om enheter och enhetstyper.

* Klicka på ett sekundärt mått till höger för att lägga till det i visualiseringen.

   Du kan visa det sekundära måttet med färg, höjd eller båda.

The following table describes the standard reports and how they are populated in Mobile Services:

| Rapport | Populationsmetod | Beskrivning |
|--- |--- |--- |
| Enhet | Livscykelstatistik | Vanliga mått uppdelade efter enhetstyp. |
| Operativsystem | Automatic | Common metrics broken down by operating system. |
| Operativsystemsversion | Livscykelstatistik | Vanliga mått uppdelade efter operativsystemsversion. |
| Operatörer | Automatisk | Vanliga mätvärden uppdelade efter transportföretag. |

>[!TIP]
>
>In the **[!UICONTROL Carriers]** report, Wi-fi users are reported as `none`.


## Lägg till uppdelningar och mått {#section_15833511E82648869E7B1EFC24EF7B82}

Du kan lägga till uppdelningar och sekundära mätvärden, vilket ändrar höjden på varje publik i förhållande till de andra målgrupperna i diagrammet.

>[!IMPORTANT]
>
>Ju fler ringar du lägger till i solbrännet, desto längre tid tar det att bearbeta.

Om du vill lägga till uppdelningar och sekundära mått klickar du på **[!UICONTROL Technology Breakdown]** i rapportens namnlist och klicka på **[!UICONTROL Customize]**.

När du klickar **[!UICONTROL Add Breakdown]** eller **[!UICONTROL Add Metric]** visas ett nytt objekt med samma namn som det föregående objektet i listan. Klicka på den nyligen skapade detaljnivån eller mätvärdet för att öppna en listruta där du kan välja ett nytt objekt.

## Skapa anteckningsfilter {#section_B4E355CD1FE34E4C8ADC38139ED67FC8}

Klicka på ett segment i ringen för att välja målgruppen som du vill skapa ett klisterfilter för och klicka på **[!UICONTROL Sticky Filter]**. Med det här filtret kan du använda de aktuella filtren och köra en ny rapport baserad på filtren.

## Dela rapporter {#section_560DD5CED5144249B7E49461E2422100}

After you create a report, your settings are used to create a custom URL that you can copy and share.
