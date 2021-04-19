---
description: Ni kan leverera riktat innehåll i Android-program.
keywords: android;bibliotek;mobil;sdk
seo-description: Ni kan leverera riktat innehåll i Android-program.
seo-title: Målkonfiguration
solution: Experience Cloud,Analytics
title: Målkonfiguration
topic-fix: Developer and implementation
uuid: 09fe2c9c-7b60-49c3-bb9d-36a30ce7c350
exl-id: dbcc3114-e76b-4b18-a418-ac46a21a593e
translation-type: tm+mt
source-git-commit: 4c2a255b343128d2904530279751767e7f99a10a
workflow-type: tm+mt
source-wordcount: '76'
ht-degree: 2%

---

# Målkonfiguration {#target-configuration}

Ni kan leverera riktat innehåll i Android-program.

## Ange programkontext {#section_37CAE496FF894FCA821F7760605574CA}

**(Obligatoriskt)** Du måste anropa  `setContext()` metoden en gång i  `onCreate()` huvudaktivitetens metod.

Exempel:

```java
@Override 
public void onCreate(Bundle savedInstanceState) { 
  super.onCreate(savedInstanceState); 
  setContentView(R.layout.main); 
  Config.setContext(this.getApplicationContext()); 
}
```

Om du redan lade till det här metodanropet när du implementerade Analytics eller Audience Management behöver du inte lägga till det igen.
