---
description: iOS Adobe Mobile SDK kan integreras smidigt i ett Swift-projekt med hjälp av Mix- och Match-funktionen i iOS Developer Library.
seo-description: iOS Adobe Mobile SDK kan integreras smidigt i ett Swift-projekt med hjälp av Mix- och Match-funktionen i iOS Developer Library.
seo-title: Snabb integrering
solution: Experience Cloud,Analytics
title: Snabb integrering
topic: Developer and implementation
uuid: 5fb77b57-cbf9-4bcf-8b41-65a933bf9336
translation-type: tm+mt
source-git-commit: ae16f224eeaeefa29b2e1479270a72694c79aaa0
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Snabb integrering {#swift-integration}

iOS Adobe Mobile SDK kan integreras smidigt i ett Swift-projekt med hjälp av Mix- och Match-funktionen i iOS Developer Library.

Mer information finns i [Språkinteroperabilitet](https://developer.apple.com/documentation/swift#2984801.html).

Om du till exempel använder rubrikmetoden Bridging så som beskrivs i dokumentationen kan du importera SDK-rubrikfilen för Adobe Mobile iOS:

```
#import “ADBMobile.h”
```

Använd följande format för att få åtkomst till metoder från SDK i dina Swift-filer:

```
ADBMobile.{methodname}
```

