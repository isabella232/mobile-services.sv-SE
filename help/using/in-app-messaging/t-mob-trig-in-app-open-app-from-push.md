---
description: Du kan ange att utlösaren för meddelanden i appen ska vara det push-meddelande-ID som skickas när en användare öppnar appen från push-meddelandet.
title: Utlös ett meddelande i appen när appen öppnas från ett push-meddelande
uuid: e1c8e29d-1c2b-47b2-8ab2-6b6e15df86f6
exl-id: 4496222f-b6f0-4fa1-86c6-149b590244d3
source-git-commit: 7cfaa5f6d1318151e87698a45eb6006f7850aad4
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Utlös ett meddelande i appen när appen öppnas från ett push-meddelande{#trigger-an-in-app-message-when-the-app-is-opened-from-a-push-message}

{#eol}

Du kan ange att utlösaren för meddelanden i appen ska vara det push-meddelande-ID som skickas när en användare öppnar appen från push-meddelandet.

1. Hämta push-meddelande-ID:t för det push-meddelande som ska skickas till användaren.

   Du kan hitta ID:t för push-meddelandet i URL:en när du skapar meddelandet.

   Här är ett exempel:

   ![](assets/brandon_task1.png)

1. Spara och aktivera meddelandet i appen med följande utlösare:

   `"a.push.payloadID" =`

   >[!TIP]
   >
   >ID:t för push-meddelandet är det ID som du placerade i steg 1.

   Den här utlösaren måste läggas till manuellt eftersom den inte är tillgänglig i **[!UICONTROL Trigger]** nedrullningsbar lista.

   ![](assets/brandon_task2.png)

1. Spara och skicka push-meddelandet som har det push-ID som du hittade i steg 1.
1. Klicka igenom push-meddelandet för att öppna programmet och verifiera att meddelandet i appen visas när appen öppnas.

   Tänk på följande information när du testar:

   * När du har sparat meddelandet i appen tar det ca 45 sekunder för den värdbaserade konfigurationsfilen att uppdateras med det nya meddelandet.
   * Programmet söker efter uppdateringar av konfigurationsfiler (det nya meddelandet i appen) när det finns ett **new** starta så att du måste se till att programmet startar en ny start när du klickar på push-meddelandet.
   Det innebär vanligtvis att du måste se till att tidsgränsen för sessionen har uppnåtts. Standardtidsgränsen är 5 minuter.
