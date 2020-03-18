---
description: Ni kan skicka signaler och hämta besökarsegment från målgruppshantering.
keywords: android;library;mobile;sdk
seo-description: Ni kan skicka signaler och hämta besökarsegment från målgruppshantering.
seo-title: Audience Manager-konfiguration
solution: Marketing Cloud,Analytics
title: Audience Manager-konfiguration
topic: Developer and implementation
uuid: f68d5b2e-fa2c-4db6-98ad-d1855a2c45ac
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Audience Manager-konfiguration{#audience-manager-configuration}

Du kan skicka signaler och hämta besökarsegment från Audience Manager.

## Ange programkontext {#section_37CAE496FF894FCA821F7760605574CA}

**(Obligatoriskt)** Metoden måste anropas en gång i huvudaktivitetens `setContext()` `onCreate()` metod.

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
