---
description: Ni kan skicka signaler och hämta besökarsegment från målgruppshantering.
keywords: android;bibliotek;mobil;sdk
seo-description: Ni kan skicka signaler och hämta besökarsegment från målgruppshantering.
seo-title: Audience Manager-konfiguration
solution: Experience Cloud,Analytics
title: Audience Manager-konfiguration
topic-fix: Developer and implementation
uuid: f68d5b2e-fa2c-4db6-98ad-d1855a2c45ac
exl-id: 05033748-5461-482f-a01d-1ba73f64616a
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 8%

---

# Audience Manager-konfiguration{#audience-manager-configuration}

Du kan skicka signaler och hämta besökarsegment från Audience Manager.

## Ange programkontext {#section_37CAE496FF894FCA821F7760605574CA}

**(Obligatoriskt)** Du måste anropa  `setContext()` metoden en gång i  `onCreate()` huvudaktivitetens metod.

Här är kodexemplet för den här metoden:

```java
@Override 
public void onCreate(Bundle savedInstanceState) { 
  super.onCreate(savedInstanceState); 
  setContentView(R.layout.main); 
  Config.setContext(this.getApplicationContext()); 
}
```

Om du lade till det här metodanropet när du implementerade Analytics eller Target behöver du inte lägga till det igen.
