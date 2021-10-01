---
description: Bearbetningsregler används för att kopiera data som du skickar i kontextdatavariabler till eVars, props och andra variabler för rapportering.
solution: Experience Cloud,Analytics
title: Bearbetar regler och kontextdata
topic-fix: Developer and implementation
uuid: 51338ccd-fa52-4d9c-97c4-947a4100465d
exl-id: a3968160-42c4-4671-b541-c14639b8a451
source-git-commit: d1ebb2bbc4742f5288f90a90e977d252f3f30aa3
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Bearbetar regler och kontextdata{#processing-rules-and-context-data}

Bearbetningsregler används för att kopiera data som du skickar i kontextdatavariabler till eVars, props och andra variabler för rapportering.

Mer information finns i följande innehåll:

* [Utbildning](https://tv.adobe.com/embed/1181/16506/)  av bearbetningsregler@ Summit 2013
* Bli behörig att använda bearbetningsregler

   Mer information om bearbetningsregler finns i [Översikt över bearbetningsregler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) i Adobe Analytics-dokumentationen.

Tänk på följande information när du arbetar med bearbetningsregler:

* Gruppera dina kontextdatavariabler med hjälp av namnutrymmen, eftersom det gör det lättare att upprätthålla en logisk ordning.

   Om du till exempel vill samla in information om en produkt kan du definiera följande variabler:

   ```js
   "product.type":"hat" 
   "product.team":"mariners" 
   "product.color":"blue"
   ```

* Sammanhangsdatavariabler sorteras i bokstavsordning i bearbetningsregelgränssnittet, som gör att du snabbt kan se vilka variabler som finns i samma namnutrymme.

   Undvik att namnge kontextdatanycklar genom att använda eVar- eller prop-nummer:

   ```js
   "eVar1":"jimbo"
   ```

   Detta kan göra det *något* enklare när du utför engångsmappning i bearbetningsregler, men du förlorar läsbarheten under felsökning och framtida koduppdateringar, vilket kan vara svårare. Använd i stället beskrivande namn för nycklar och värden:

   ```js
   "username":"jimbo"
   ```

* Kontextvariabler som definierar räknarhändelser ska anges till 1:

   ```js
   "logon":"1"
   ```

* Sammanhangsdatavariabler som definierar stegvisa händelser kan ha händelsen som nyckel och mängden som ska ökas som värde:

   ```js
   "levels completed":"6"
   ```

>[!TIP]
>
>Adobe reserverar namnutrymmet `a.`. Förutom den begränsningen, för att undvika kollisioner, är det enda kravet att kontextdatavariabler är unika i ditt inloggningsföretag.
