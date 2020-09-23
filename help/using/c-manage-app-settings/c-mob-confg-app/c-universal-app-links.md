---
description: Tack vare iOS- och Applänkar (Android) kan du ansluta till djupa länkar i iOS- och Android-appar.
keywords: mobile
seo-description: Tack vare iOS- och Applänkar (Android) kan du ansluta till djupa länkar i iOS- och Android-appar.
seo-title: Apple Universal Links och Android App Links
solution: Experience Cloud,Analytics
title: Apple Universal Links och Android App Links
topic: Metrics
uuid: 8d6441dc-4307-4454-95ea-d77ec796f918
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---


# Apple Universal Links och Android App Links{#universal-links-and-app-links}

Tack vare iOS- och Applänkar (Android) kan du ansluta till djupa länkar i iOS- och Android-appar.

>[!IMPORTANT]
>
>Från och med iOS 9.2 stöds inte djuplänkning. Du måste använda Apple Universal Links för att kunna länka till din app eller webbplats.

## Universallänkar {#section_F8147944679A42E59CF4FD8814E5EF12}

Med universella länkar kan du ansluta till djupa länkar i din iOS-app och stöds i iOS 9.2 eller senare. När en universell länk används dirigeras länken direkt till länken i appen. Om ditt program inte är installerat öppnas en URL för din webbplats i en webbläsare i stället. Mer information om universallänkar finns i [Stöd för universallänkar](https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html).

## Applänkar

Med applänkar kan du ansluta till djupa länkar i Android-appen och stöds i Android 6.0 eller senare. När en App Link nås dirigerar Android om länken direkt till den överordnade länken i din app. Om ditt program inte är installerat öppnas en URL för din webbplats i en webbläsare i stället. Mer information om applänkar finns i [Hantera Android-applänkar](https://developer.android.com/training/app-links/index.html).

## Skapa en marknadsföringslänk med en universell länk eller en applänk {#section_609ADEFFB9B441C4A8C45E936D0DC859}

Du kan skapa en marknadsföringslänk som använder en universell länk eller en applänk.

### Konfigurera en universell länk

1. Om du vill konfigurera universallänkar i din iOS-app går du till [Hantera universallänkar i Apple](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/handling_universal_links).

2. Konfigurera webbplatsassociationsdokumenten i Adobe Mobile Services:

   a. På startsidan för Mobiltjänster väljer du den app som du vill konfigurera universallänkar för.

   b. Klicka **[!UICONTROL Manage App Settings]**.

   c. Kontrollera att iOS-appen som hanterar universallänkarna har lagts till i **[!UICONTROL Add App Store Apps]** -avsnittet.

   >[!TIP]
   >
   >Om avsnittet inte visas klickar du på **[!UICONTROL Add App Store Apps]** **[!UICONTROL Add App Store App]** länken.

   d. I **[!UICONTROL Universal Links and App Links Options]** avsnittet väljer du en iOS-app och skriver ett program-ID.

   f. Klicka **[!UICONTROL Save]**.

   Du måste ange minst ett iOS-programval och ett program-ID, annars får du ett felmeddelande.

   >[!IMPORTANT]
   >
   >Du kan uppdatera dokumenten genom att klicka på Uppdatera under Alternativ för universallänkar och applänkar. När du klickar **[!UICONTROL Update]** visas ett varningsmeddelande om att alla universallänkar eller applänkar som du har skapat tidigare kommer att påverkas.

### Använd en universell länk

1. Skapa en Marketing Link som använder universallänkar i Adobe Mobile Services:

   a. Välj appen från startsidan för Mobiltjänster och klicka på **[!UICONTROL Acquisition]** > **[!UICONTROL Marketing Link Builder]**.

   b. Klicka **[!UICONTROL Create New]**.

   c. Under **[!UICONTROL Marketing Link Options]** väljer du **[!UICONTROL Use Universal Links or App Links]**.

   d. Om du konfigurerade platsassociationsdokumenten i avsnittet *Konfigurera platsassociationsdokument i Adobe Mobile Services* ovan, är det här alternativet markerat som standard.

   Om du inte konfigurerade dokumenten är **[!UICONTROL Use Universal Links or App Links]** alternativet inaktiverat och **[!UICONTROL Use Interstitials]** markerat som standard.

   e. Om **[!UICONTROL Use Universal Links or App Links]** alternativet är markerat visas **[!UICONTROL Custom Path]** fältet.

   Detta gör att användare kan definiera URL-sökvägen efter domänen med valfri frågeparameter. Om du till exempel skriver `my/universal/link?os=9.2`blir den fullständiga URL:en för Marketing Link `https://[marketing link domain]/my/universal/link?[AMS default query parameters]&os=9.2`.

   f. Klicka på **[!UICONTROL Decisions]** fliken och konfigurera beslutsträdet.

   h. Om iOS-appen är installerad hanterar appen länken med dess logik. Slutmålet fungerar bara som reserv när programmet inte är installerat. Eftersom appen inte är installerad kan slutmålet bara vara en webblänk eller en appbutik.

   i. Klicka **[!UICONTROL Save]**.

>[!TIP]
>
>När en marknadsföringslänk har sparats går det inte att ändra alternativen för marknadsföringslänkar. Detta beror på att du inte vill ändra beteendet för de marknadsföringslänkar som redan har distribuerats.


### Konfigurera en applänk

1. Om du vill konfigurera applänkar i Android-appen går du till [Lägg till Android-applänkar](https://developer.android.com/studio/write/app-link-indexing).

1. Konfigurera webbplatsassociationsdokumenten i Adobe Mobile Services:

   a. På startsidan för Mobiltjänster väljer du det program som du vill konfigurera applänkar för.

   b. Klicka **[!UICONTROL Manage App Settings]**.

   c. Kontrollera att Android-appen som hanterar universallänkar eller applänkar har lagts till i **[!UICONTROL Add App Store Apps]** -avsnittet.

   >[!TIP]
   >
   >Om det här avsnittet inte visas klickar du på **[!UICONTROL Add App Store App]** länken.

   d. Bläddra till **[!UICONTROL Universal Links and App Links Options]** avsnittet.

   e. Klicka på **[!UICONTROL App Links (Android)]** fliken.

   f. Välj en Android-app och skriv ett SHA-256-certifikatfingeravtryck.

   g. Klicka **[!UICONTROL Save]**.

   Du måste ange minst ett val av Android-program och ett SHA-256-certifikat, annars får du ett felmeddelande.

   >[!IMPORTANT]
   >
   >Du kan uppdatera dokumenten genom att klicka **[!UICONTROL Update]** i **[!UICONTROL Universal Links and App Links Options]** avsnittet. När du klickar **[!UICONTROL Update]** visas ett varningsmeddelande om att alla universallänkar eller applänkar som du har skapat tidigare kommer att påverkas.

### Använd en applänk

1. Skapa en Marketing Link som använder applänkar i Adobe Mobile Services:

   a. Välj appen från startsidan för Mobiltjänster och klicka på **[!UICONTROL Acquisition]** > **[!UICONTROL Marketing Link Builder]**.

   b. Klicka **[!UICONTROL Create New]**.

   c. Markera i **[!UICONTROL Marketing Link Options]** avsnittet **[!UICONTROL Use Universal Links or App Links]**.

   d. Om du konfigurerade platsassociationsdokumenten från steg 2 väljs det här alternativet som standard.

   Annars är **[!UICONTROL Use Universal Links or App Links]** alternativet inaktiverat och **[!UICONTROL Use Interstitials]** markerat som standard.

   e. Om **[!UICONTROL Use Universal Links or App Links]** du väljer det här alternativet visas **[!UICONTROL Custom Path]** fältet.

   Detta gör att användare kan definiera URL-sökvägen efter domänen med valfri frågeparameter. Om du till exempel skriver `my/app/link?os=6.0`blir den fullständiga URL:en för Marketing Link `https://[marketing link domain]/my/app/link?[AMS default query parameters]&os=6.0`.

   f. Klicka på **[!UICONTROL Decisions]** fliken och konfigurera beslutsträdet.

   g. Om Android-appen är installerad hanterar appen länken med dess logik.

   Slutmålet fungerar bara som reserv när programmet inte är installerat. Eftersom appen inte är installerad kan slutmålet bara vara en webblänk eller en appbutik.

   h.  Klicka **[!UICONTROL Save]**.

>[!TIP]
>
>När en marknadsföringslänk har sparats **[!UICONTROL Marketing Links Options]** kan den inte ändras. Detta beror på att du inte vill ändra beteendet för de marknadsföringslänkar som redan har distribuerats.

## Använda marknadsföringslänkar

Du kan nu använda dessa marknadsföringslänkar i meddelanden och andra områden i din app.

>[!IMPORTANT]
>
>Du ser inte antalet klickspårningar med universallänkar eller applänkar och du kan inte heller använda interstitialer.

