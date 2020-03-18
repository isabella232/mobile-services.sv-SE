---
description: Ni kan leverera riktat innehåll i Android-program.
keywords: android;library;mobile;sdk
seo-description: Ni kan leverera riktat innehåll i Android-program.
seo-title: Målkonfiguration
solution: Marketing Cloud,Analytics
title: Målkonfiguration
topic: Developer and implementation
uuid: 09fe2c9c-7b60-49c3-bb9d-36a30ce7c350
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

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
