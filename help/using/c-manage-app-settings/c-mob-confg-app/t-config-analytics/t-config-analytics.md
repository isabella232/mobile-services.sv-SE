---
description: Du kan konfigurera SDK Analytics-alternativen på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.
keywords: mobile
seo-description: Du kan konfigurera SDK Analytics-alternativen på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.
seo-title: Konfigurera alternativ för SDK-analys
solution: Experience Cloud,Analytics
title: Konfigurera alternativ för SDK-analys
topic: Metrics
uuid: fd3a21d2-6560-4e96-92fe-b99caac5e834
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Konfigurera alternativ för SDK-analys {#configure-sdk-analytics-options}

Du kan konfigurera SDK Analytics-alternativen på sidan Hantera appinställningar när du skapar en ny app eller redigerar en befintlig app.

Skriv information i följande fält under **[!UICONTROL SDK Analytics Options]**:

* **[!UICONTROL Use HTTPS]**

   Aktivera HTTPS för ökad säkerhet.

* **[!UICONTROL Backdate Session Hits]**

   Aktivera eller inaktivera möjligheten för Adobe SDK att uppdatera sessionsinfo. Sessionsinformationsträffar består för närvarande av krascher och sessionslängd. När det här alternativet är aktiverat kommer Adobe SDK att uppdatera sessionsinformationen som träffats till en sekund efter den senaste träffen i föregående session. Detta innebär att krascher och sessionsdata korrelerar med rätt datum då de inträffade. En träff blir inaktuell vid varje ny programstart. När det är inaktiverat kommer Adobe SDK att bifoga sessionsinformationen till den aktuella livscykeln.

* **[!UICONTROL Privacy]**

   Välj ett sekretessalternativ:

   * **[!UICONTROL Send Data Until Opt-Out]**
   * **[!UICONTROL Hold Data Until Opt-In]**

* **[!UICONTROL Session Timeout (Seconds)]**

   Ange timeout-värdet för sessionen.

   Standardvärdet är 300 sekunder. Anger hur lång tid (i sekunder) som måste gå mellan det att programmet startas innan det betraktas som en ny session. Den här tidsgränsen gäller även när programmet skickas till bakgrunden och återaktiveras. Den tid som programmet lägger i bakgrunden inkluderas inte i sessionslängden.

* **[!UICONTROL Batch Limit]**

   Ange hur många träffar du vill placera i kö innan du skickar data.

   Ange 0 om du vill skicka träffar direkt. Batchgränsen representerar tröskelvärdet för antalet träffar som ska skickas i efterföljande anrop. Om det här alternativet till exempel är 10 lagras varje träff före den 10:e träffen i kön. När den 10:e träffen kommer in skickas alla 10 träffar i följd.

* **[!UICONTROL More Details]**

   Klicka på **[!UICONTROL More Details]** länken för att visa rapportsvitens ID och spårningsserver, aktivera eller inaktivera spårning offline och visa den teckenkodningsmodell som används (till exempel UTF-8).

   När spårning offline är aktiverat kommer data som genereras av enheten när den är offline att tidsstämplas och skickas senare. Om det här alternativet är inaktiverat ignoreras offlinedata.
