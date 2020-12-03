---
description: I Adobe Analytics kan du hantera roller på startsidan för Admin Tools.
seo-description: I Adobe Analytics kan du hantera roller på startsidan för Admin Tools.
seo-title: Roller och behörigheter
title: Roller och behörigheter
uuid: ad350f8d-ef51-4519-98aa-3025bc0f5588
translation-type: tm+mt
source-git-commit: c7cac006340e01d0fd1f6afe3419e6fd17294a98
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 6%

---


# Roller och behörigheter{#roles-and-permissions}

I Adobe Analytics kan du hantera roller på startsidan för Admin Tools.

## Översikt {#section_91B8192891E14E5285718C8118912500}

Följande roller hanterar behörigheter i gränssnittet för mobila tjänster:

### Analysadministratör

En Analytics Admin hanterar användargrupper och tilldelar behörigheter, varav en är Mobile App Admin. Experience Cloud Admin länkar din Adobe ID till ditt Adobe Analytics-konto så att du kan logga in på användargränssnittet för mobila tjänster med hjälp av din Adobe ID. Mer information om Experience Cloud Administrator finns i [Administration - Användarhantering och Frågor och svar](https://docs.adobe.com/content/help/sv-SE/core-services/interface/manage-users-and-products/admin-getting-started.html).

>[!TIP]
>
>En befintlig Analytics Admin kan tilldela rollen Analytics Admin till alla användare.

Mer information om den här rollen finns i följande innehåll:

* [Översikt över användarhantering](https://docs.adobe.com/content/help/en/analytics/admin/user-product-management/user-management/users.html)

* [Behörighetsändringar för användare och grupper](https://docs.adobe.com/content/help/en/analytics/admin/user-product-management/user-management/permissions-changes.html)

### Administratör för mobilapp

Den här rollen är administratör för användargränssnittet för mobila tjänster.

>[!IMPORTANT]
>
>För vissa funktioner, till exempel push-meddelanden, måste Analytics Admin markera kryssrutan i Användarhantering **[!UICONTROL Segment Creation]** .

## Hantera åtkomst {#section_E6939C2695AA4A0DBF432D50B2670920}

Här finns mer information om hur du får tillgång till alternativ i gränssnittet för mobila tjänster:

### Program och rapportsviter

Alla mobiltjänstappar är knutna till rapportsviter. Om användarna inte har tillgång till en rapportsserie har de inte tillgång till den rapportsvitens associerade app.

### Mobiltjänster och analysfunktioner

Om ditt företag inte har något Analytics-avtal för att komma åt en funktion i användargränssnittet, till exempel Push Messaging, har ingen användare i ditt företag åtkomst till den funktionen, oavsett behörighetsnivå.

## Roller och behörigheter {#section_20AA029D5B8C413C8659777E79B11620}

Här är rollerna i gränssnittet för mobila tjänster, med deras relevanta behörigheter:

### Analysadministratör

* Alla administratörsbehörigheter för användare och mobilappar
* Skapa app med nytt rapportpaket
* Ta bort app från mobiltjänster

   >[!IMPORTANT]
   >
   >Även om appen har tagits bort i gränssnittet för mobiltjänster finns rapportsviten fortfarande i Analytics.

* Hantera appinställningar

   * Aktivera livscykelrapportering
   * Aktivera platsrapportering
   * Skapa/uppdatera/ta bort variabler och mätvärden

### Administratör för mobilapp

* Alla användarbehörigheter
* Skapa app med befintlig rapportsvit
* Hantera appinställningar

   * Konfigurera appens SDK-alternativ för mobiler
   * Konfigurera appens gränssnittsinställningar
   * Konfigurera länkade App Store-appar
   * Konfigurera alternativ för Universal Link för appen
   * Konfigurera push-tjänstcertifikat och API-nycklar
   * Skapa/uppdatera/aktivera/inaktivera/duplicera/arkivera/ta bort återanslag
   * Skapa/uppdatera/arkivera/ta bort länkmål

* Skapa/uppdatera/arkivera marknadsföringslänkar
* Skapa/importera/uppdatera/ta bort länkar för äldre anskaffning
* Skapa/importera/uppdatera/ta bort platser (intressepunkter), konfiguration
* Skapa/Uppdatera/Skicka/Schemalägg/Avbryt/Duplicera/Arkivera/Ta bort push-meddelanden
* Skapa/uppdatera/aktivera/inaktivera/duplicera/arkivera/ta bort meddelanden i appen

Mer information om grupper och användare finns i:

* [Inställningar för användargrupp](https://docs.adobe.com/content/help/sv-SE/analytics/admin/user-product-management/user-groups/groups.html)
* [Lägga till en användare i en grupp](https://docs.adobe.com/content/help/en/analytics/admin/user-product-management/user-management/t-add-user-to-group.html)

### Användare av mobiltjänster

Den här rollen har endast behörighet att visa och kan ge feedback i gränssnittet för mobila tjänster.

* Ge feedback om gränssnittet för mobiltjänster
* Visa appar

   >[!IMPORTANT]
   >
   >Användare kan bara se de rapportsviter som de har tillgång till i Adobe Analytics.

* Visa appinställningar

   * Hämta app-SDK-konfiguration
   * Visa alla inställningar för användargränssnitt och SDK
   * Visa konfiguration för variabler och mått
   * Visa återanslag
   * Visa länkmål

* Visa och kör rapporter
* Visa marknadsföringslänkar
* Visa och exportera länkar för äldre förvärv
* Visa och exportera platser (intressepunkter), konfiguration
* Visa push-meddelanden
* Visa meddelanden i appen
