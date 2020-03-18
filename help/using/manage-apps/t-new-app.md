---
description: Du kan använda den här informationen för att skapa en ny app och konfigurera dess nyckelmått, konfigurera SDK-alternativen för Adobe Analytics och Adobe Audience Manager, konfigurera alternativ för förvärv och ID-tjänster samt hämta konfigurationsfilen, SDK:n samt utvecklings- och testverktygen.
keywords: mobile
seo-description: Du kan använda den här informationen för att skapa en ny app och konfigurera dess nyckelmått, konfigurera SDK-alternativen för Adobe Analytics och Adobe Audience Manager, konfigurera alternativ för förvärv och ID-tjänster samt hämta konfigurationsfilen, SDK:n samt utvecklings- och testverktygen.
seo-title: Lägg till en ny app
solution: Marketing Cloud,Analytics
title: Lägg till en ny app
topic: Metrics
uuid: 706b5e4d-1318-4a9e-8c69-ffabf51fa02c
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Lägg till en ny app{#add-a-new-app}

Du kan använda den här informationen för att skapa en ny app och konfigurera dess nyckelmått; konfigurera SDK-alternativen för Adobe Analytics och Adobe Audience Manager; konfigurera alternativ för förvärv och ID-tjänster, och hämta konfigurationsfilen, SDK:er samt utvecklar- och provverktygen.

De här instruktionerna hjälper er att lägga till en ny app och konfigurera integreringar mellan Adobe Analytics och Adobe Audience Manager.

Innan du kan konfigurera din app måste du lägga till den i användargränssnittet för Adobe Mobile Services. När du har skapat appen skapas rätt konfiguration, och du kan tillhandahålla den här konfigurationen till utvecklare som implementerar Mobile SDK för appen.

1. Logga in på Adobe Mobile Services och utför någon av följande uppgifter:

   * Klicka **[!UICONTROL Create New]** för att skapa ett program.
   * Om du vill lägga till fler program klickar du på Hantera appar i den vänstra navigeringsmenyn och klickar på **[!UICONTROL Add]**.

      Mer information om inloggning finns i [Logga in](/help/using/gs/gs-signin.md).

      >[!TIP]
      >
      >Om du vill hantera befintliga program klickar du på Hantera program på den vänstra navigeringsmenyn och sedan på det program som du vill ändra. Du kan göra ändringar på sidan Programinformation.

1. Skriv information i följande fält:

   **[!UICONTROL Report Suite]**

   Ange i vilken rapportsvit som rapportdata ska samlas in och lagras i Adobe Analytics. Alla program är anslutna till en enda analysrapport. Om du skickar appdata till flera rapportsviter lägger du till en ny app för varje rapportserie. Alla program är anslutna till en enda analysrapport. Om du skickar appdata till flera rapportsviter lägger du till en ny app för varje rapportserie.

   Om du har fått administratörsbehörighet för Analytics i Adobe Mobile kan du skapa en ny rapportserie i Adobe Mobile. Om du vill skapa en ny rapportserie väljer du **[!UICONTROL New Report Suite]** och skriver information i följande fält:

   * **[!UICONTROL Report Suite ID]**

      Detta ID identifierar rapportsviten i Adobe Analytics unikt. Företagsprefixet läggs automatiskt till i början av ID:t.

   * **[!UICONTROL Copy Settings From]**

      Variabler, händelser, bearbetningsregler och andra inställningar ställs in i den nya rapportsviten precis som i den här rapportsviten. En rapportsvit som skapats i Mobiltjänster är offline-aktiverad (eller tidsstämplad) endast om rapportsviten som användes var Mobile App Template eller om du skapar en rapportsvit som är offline-aktiverad. **[!UICONTROL Copy Settings From]**

   * **[!UICONTROL Timezone]**

      Alla rapportdatum finns i den här tidszonen. Den här inställningen försöker använda en tidszon som ligger nära den som webbläsaren använder.

   * **[!UICONTROL Currency]**

      Intäkter spåras och rapporteras som denna typ av valuta.
   >[!TIP]
   >
   >Mer information om hur du använder en virtuell rapporteringssvit (VRS) finns i [Virtuella rapportsvit](/help/using/manage-apps/c-mob-vrs.md).

   * **[!UICONTROL Icon]**

      (**Valfritt**) Om du vill bläddra till och välja en ikon för ditt program klickar du på **[!UICONTROL Icon]**.

   * **[!UICONTROL Name]**

      (**Valfritt**) Ange ett beskrivande namn för programmet. Det här namnet hjälper dig att snabbt hitta ett program och ett beskrivande namn kan hjälpa dig att snabbt förstå appens syfte och inställningar.

   * **[!UICONTROL Type]**

      Välj en typ i listrutan. Vilka rapporter som visas på den vänstra navigeringsmenyn varierar beroende på vilken typ av program du väljer.

      Här är de tillgängliga typerna:

      * **[!UICONTROL Standard]**

         Du kan lämna alternativet **[!UICONTROL Standard}** markerat för de flesta appar.

      * **[!UICONTROL Publication]**

         Du kan välja det här alternativet om appen har skapats med Adobe Digital Publishing Suite.

      * **[!UICONTROL Game]**

         Det här alternativet liknar **[!UICONTROL Standard]** alternativet, förutom att terminologin som används i rapporterna **[!UICONTROL Game]** uppdateras till villkor för spel. Användare ändras till exempel till spelare. Spelspecifika rapporter visas automatiskt för spelprogram.
   * **[!UICONTROL Description]**

      (**Valfritt**) Skriv en beskrivning för programmet.



1. Klicka **[!UICONTROL Save]** för att lägga till det nya programmet.

   När appen har lagts till kan du kontrollera sidan Programinformation om hur du konfigurerar ytterligare alternativ. Mer information finns i [Hantera appinställningar](/help/using/c-manage-app-settings/c-manage-app-settings.md).