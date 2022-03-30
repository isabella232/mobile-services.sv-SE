---
description: Ni kan leverera riktat innehåll i Android-program.
keywords: android;bibliotek;mobil;sdk
solution: Experience Cloud Services,Analytics
title: Målkonfiguration
topic-fix: Developer and implementation
uuid: 09fe2c9c-7b60-49c3-bb9d-36a30ce7c350
exl-id: dbcc3114-e76b-4b18-a418-ac46a21a593e
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 3%

---

# Målkonfiguration {#target-configuration}

Ni kan leverera riktat innehåll i Android-program.

## Ange programkontext {#section_37CAE496FF894FCA821F7760605574CA}

**(Obligatoriskt)** The `setContext()` -metoden måste anropas en gång i `onCreate()` huvudaktivitetens metod.

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
