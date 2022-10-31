---
description: I Adobe Analytics kan du hantera roller på startsidan för Admin Tools.
title: Roller och behörigheter
uuid: ad350f8d-ef51-4519-98aa-3025bc0f5588
exl-id: 70f0b427-60d5-4a79-a8d3-e03274edd917
source-git-commit: 7cfaa5f6d1318151e87698a45eb6006f7850aad4
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# Roller och behörigheter{#roles-and-permissions}

{#eol}

I Adobe Analytics kan du hantera roller på startsidan för Admin Tools.

## Översikt {#section_91B8192891E14E5285718C8118912500}

Följande roller hanterar behörigheter i gränssnittet för mobila tjänster:

### Analysadministratör

En Analytics Admin hanterar användargrupper och tilldelar behörigheter, varav en är Mobile App Admin. Experience Cloud Admin länkar din Adobe ID till ditt Adobe Analytics-konto så att du kan logga in på användargränssnittet för mobila tjänster med hjälp av din Adobe ID. Mer information om Experience Cloud Administrator finns i [Hantera användare och produkter i Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/administration/admin-getting-started.html) i guiden Komponenter i Experience Cloud Central Interface.

>[!TIP]
>
>En befintlig Analytics Admin kan tilldela rollen Analytics Admin till alla användare.

### Administratör för mobilapp

Den här rollen är administratör för användargränssnittet för mobila tjänster.

>[!IMPORTANT]
>
>För vissa funktioner, till exempel push-meddelanden, måste Analytics Admin välja **[!UICONTROL Segment Creation]** kryssrutan i Användarhantering.

## Hantera åtkomst {#section_E6939C2695AA4A0DBF432D50B2670920}

Här finns mer information om hur du får tillgång till alternativ i gränssnittet för mobila tjänster:

### Program och rapportsviter

Alla mobiltjänstappar är knutna till rapportsviter. Om användarna inte har tillgång till en rapportsserie har de inte tillgång till den rapportsvitens associerade app.

### Mobiltjänster och analysfunktioner

Om ditt företag inte har något Analytics-avtal för att komma åt en funktion i användargränssnittet, till exempel Push Messaging, har ingen användare i ditt företag åtkomst till den funktionen, oavsett behörighetsnivå.

## Roller och behörigheter {#section_20AA029D5B8C413C8659777E79B11620}

Här är rollerna i gränssnittet för mobila tjänster, med deras relevanta behörigheter:

### Administratörsbehörigheter för analyser

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

### Administratörsbehörigheter för mobilappar

* Alla användarbehörigheter
* Skapa app med befintlig rapportsvit
* Hantera appinställningar

   * Konfigurera appens SDK-alternativ för mobiler
   * Konfigurera appens gränssnittsinställningar
   * Konfigurera länkade App Store-program
   * Konfigurera alternativ för Universal Link för appen
   * Konfigurera push-tjänstcertifikat och API-nycklar
   * Skapa/uppdatera/aktivera/inaktivera/duplicera/arkivera/ta bort återanslag
   * Skapa/uppdatera/arkivera/ta bort länkmål

* Skapa/uppdatera/arkivera marknadsföringslänkar
* Skapa/importera/uppdatera/ta bort länkar för äldre anskaffning
* Skapa/importera/uppdatera/ta bort platser (intressepunkter), konfiguration
* Skapa/Uppdatera/Skicka/Schemalägg/Avbryt/Duplicera/Arkivera/Ta bort push-meddelanden
* Skapa/uppdatera/aktivera/inaktivera/duplicera/arkivera/ta bort meddelanden i appen

Mer information om grupper och användare finns i följande innehåll i Adobe Analytics-dokumentationen:

* [Inställningar för användargrupp (äldre)](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html)
* [Lägga till en användare i en grupp](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html)

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
