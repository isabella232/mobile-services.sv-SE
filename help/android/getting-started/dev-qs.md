---
description: Den här informationen hjälper dig att implementera Android-biblioteket och samla in livscykelvärden, som starter, uppgraderingar, sessioner, engagerade användare och så vidare.
keywords: android;bibliotek;mobil;sdk
seo-description: Den här informationen hjälper dig att implementera Android-biblioteket och samla in livscykelvärden, som starter, uppgraderingar, sessioner, engagerade användare och så vidare.
seo-title: Kärnimplementering och livscykel
solution: Experience Cloud,Analytics
title: Kärnimplementering och livscykel
topic-fix: Developer and implementation
uuid: af4d11ac-8245-46a0-9b3a-4a0a29cfbbb2
exl-id: 67aba85a-42a0-473a-bb05-e5fcb35263d9
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---

# Core-implementering och livscykel {#core-implementation-and-lifecycle}

Den här informationen hjälper dig att implementera Android-biblioteket och samla in livscykelvärden, som starter, uppgraderingar, sessioner, engagerade användare och så vidare.

## Hämta SDK {#section_99FE1A17A36D4A2C943939023CF6265C}

>[!IMPORTANT]
>
>Om du vill hämta SDK måste du använda Android 2.2 eller senare.

1. Slutför stegen i följande avsnitt för att konfigurera en utvecklingsrapportssvit och hämta en förifylld version av konfigurationsfilen:

   * [Skapa en rapportsvit](/help/android/getting-started/requirements.md)
   * [Ladda ned SDK](/help/android/getting-started/requirements.md)

1. Hämta och zippa upp filen `[Your_App_Name_]AdobeMobileLibrary-4.*-Android.zip` och verifiera att följande programvarukomponenter finns:

   * `adobeMobileLibrary.jar`, som är det bibliotek som ska användas med Android-enheter och -simulatorer.

   * `ADBMobileConfig.json`, som är SDK-konfigurationsfilen som är anpassad för ditt program.
   >[!IMPORTANT]
   >
   >Om du hämtar SDK-filen utanför användargränssnittet för Adobe Mobile Services måste filen `ADBMobileConfig.json` konfigureras manuellt. Om det är första gången du använder Analytics och Mobile SDK och du vill konfigurera en utvecklingsrapportsvit och hämta en förifylld version av konfigurationsfilen, se [Innan du börjar](/help/android/getting-started/requirements.md).

## Lägg till SDK- och config-filen i IntelliJ IDEA- eller Eclipse-projektet {#section_B89510FBB4C646AEA73A185B966E54D3}

**IntelliJ IDEA-projekt**

Så här lägger du till SDK- och konfigurationsfilen i projektet:

1. Lägg till filen `ADBMobileConfig.json` i mappen `assets` i ditt projekt.

1. Högerklicka på projektet på projektnavigeringspanelen.
1. Välj **[!UICONTROL Open Module Settings]**.
1. Under **[!UICONTROL Project Settings]** väljer du **[!UICONTROL Libraries]**.
1. Klicka på ikonen **[!UICONTROL +]** för att lägga till ett nytt bibliotek.
1. Välj **[!UICONTROL Java]** och navigera till filen `adobeMobileLibrary.jar`.
1. Välj de moduler där du tänker använda mobilbiblioteket.
1. Klicka på **[!UICONTROL Apply]** och **[!UICONTROL OK]** för att stänga fönstret Modulinställningar.

**Eclipse-projekt**

Så här lägger du till SDK- och konfigurationsfilen i projektet:

1. Lägg till filen `ADBMobileConfig.json` i mappen `assets` i ditt projekt.
1. Högerklicka på projektnamnet i **[!UICONTROL Eclipse IDE]**.
1. Klicka på  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]**.
1. Välj `adobeMobileLibrary.jar`.
1. Klicka på **[!UICONTROL Open]**.
1. Högerklicka på projektet igen och välj **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]**.
1. Kontrollera att **`adobeMobileLibrary.jar`** är markerat på fliken **[!UICONTROL Order and Export]**.

## Lägg till programbehörigheter {#section_2EAF73ABF6424647B219A63B33B02CD5}

AppMeasurement Library kräver följande behörigheter för att skicka data och registrera offlinespårningsanrop:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Om du vill lägga till de här behörigheterna lägger du till följande rader i din `AndroidManifest.xml`-fil som finns i programmets projektkatalog:

```java
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

## Ange programkontext {#set-application-context}

Följande kod ska läggas till i `onCreate`-metoden för din huvudaktivitet:

```java
   @Override
   public void onCreate(BundlesavedInstanceState){
     super.onCreate(savedInstanceState)
     setContentView(R.layout.main);
     Config.setContext(this.getApplicationContext());
   }
```

## Implementera livscykelvärden {#section_BA686C09021F474AADDE8690BBB910F7}

När du har aktiverat livscykeln skickas en träff varje gång appen startas för att mäta öppningar, uppgraderingar, sessioner, engagerade användare och många andra mätvärden. Mer information finns i [Livscykelvärden](/help/android/metrics.md).

**Utför följande steg i varje programaktivitet:**

1. Importera biblioteket:

   ```java
   import com.adobe.mobile.*;
   ```

1. Starta livscykeldatainsamlingen i funktionen `onResume`:

   ```java
   @Override 
   public void onResume() { 
       Config.collectLifecycleData(this); 
       // -or- Config.collectLifecycleData(this, contextData); 
   }
   ```

1. Pausa livscykeldatainsamlingen i funktionen `onPause`:

   ```java
   @Override 
   public void onPause() { 
       Config.pauseCollectingLifecycleData(); 
   }
   ```

>[!IMPORTANT]
>
>Du måste lägga till dessa samtal till varje aktivitet för att få en korrekt kraschrapportering. Mer information finns i [Spåra programkrascher](/help/android/analytics-main/crashes.md).

## Inkludera ytterligare data vid livscykelanrop

Om du vill inkludera ytterligare data med livscykelmätningsanrop skickar du en extra parameter till `collectLifecycleData` som innehåller kontextdata:

```java
@Override 
public void onResume() {
    HashMap<String, Object> contextData = new HashMap<String, Object>(); 
    contextData.put("myapp.category", "Game"); 
    Config.collectLifecycleData(this, contextData); 
}
```

Ytterligare kontextdatavärden som skickas med `collectLifecycleData` måste mappas till anpassade variabler i Adobe Mobile-tjänster:

![](assets/map-variable-lifecycle.png)

Andra livscykelvärden samlas in automatiskt. Mer information finns i [Livscykelvärden](/help/android/metrics.md).

## Gör följande {#section_BF709684E1DD40EA9169BC1D0D4B37C2}

Utför följande uppgifter:

* [Spåra applägen](/help/android/analytics-main/states.md)
* [Spåra appåtgärder](/help/android/analytics-main/actions.md)
