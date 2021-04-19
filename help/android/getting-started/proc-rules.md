---
description: Bearbetningsregler används för att kopiera data som du skickar i kontextdatavariabler till eVars, props och andra variabler för rapportering.
seo-description: Bearbetningsregler används för att kopiera data som du skickar i kontextdatavariabler till eVars, props och andra variabler för rapportering.
seo-title: Bearbetar regler och kontextdata
solution: Experience Cloud,Analytics
title: Bearbetar regler och kontextdata
topic-fix: Developer and implementation
uuid: ea892228-86f5-4980-acb8-45ae43c6996d
exl-id: 543201fd-8118-485f-8235-26ec8f9bbb11
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---

# Bearbetar regler och kontextdata {#processing-rules-and-context-data}

Bearbetningsregler används för att kopiera data som du skickar i kontextdatavariabler till eVars, props och andra variabler för rapportering. Mer information finns i [Bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html).

Tänk på följande information när du arbetar med bearbetningsregler:

* Gruppera dina kontextdatavariabler med hjälp av namnutrymmen, eftersom det gör det lättare att upprätthålla en logisk ordning. Om du till exempel vill samla in information om en produkt kan du definiera följande variabler:

   ```js
   "product.type":"hat" 
   "product.team":"mariners" 
   "product.color":"blue"
   ```

* Sammanhangsdatavariabler sorteras i bokstavsordning i bearbetningsregelgränssnittet, som gör att du snabbt kan se vilka variabler som finns i samma namnutrymme.

   Undvik att namnge kontextdatanycklar genom att använda evar- eller prop-numret:

   ```js
   "eVar1":"jimbo"
   ```

   Detta kan göra det *något* enklare när du slutför engångsmappningen i bearbetningsregler, men du förlorar läsbarheten under felsökning och framtida koduppdateringar, vilket kan vara svårare. Vi rekommenderar i stället att du använder beskrivande namn för nycklar och värden:

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
>Adobe reserverar namnutrymmet `"a."`. För att undvika kollisioner är det enda andra kravet att kontextdatavariabler är unika i ditt inloggningsföretag.
