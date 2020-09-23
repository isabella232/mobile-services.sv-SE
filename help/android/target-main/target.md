---
description: Ni kan leverera riktat innehåll i Android-program.
keywords: android;library;mobile;sdk
seo-description: Ni kan leverera riktat innehåll i Android-program.
seo-title: Målkonfiguration
solution: Experience Cloud,Analytics
title: Målkonfiguration
topic: Developer and implementation
uuid: 09fe2c9c-7b60-49c3-bb9d-36a30ce7c350
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 2%

---


# Målkonfiguration {#target-configuration}

Ni kan leverera riktat innehåll i Android-program.

## Ange programkontext {#section_37CAE496FF894FCA821F7760605574CA}

**(Obligatoriskt)** Metoden måste anropas en gång i huvudaktivitetens `setContext()` `onCreate()` metod.

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
