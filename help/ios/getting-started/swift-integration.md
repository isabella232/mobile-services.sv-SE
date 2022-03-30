---
description: iOS Adobe Mobile SDK kan integreras smidigt i ett Swift-projekt med funktionen Mix och Match i iOS Developer Library.
solution: Experience Cloud Services,Analytics
title: Snabb integrering
topic-fix: Developer and implementation
uuid: 5fb77b57-cbf9-4bcf-8b41-65a933bf9336
exl-id: 3c1a2e28-53b0-4128-a5d9-d2403885098d
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Snabb integrering {#swift-integration}

iOS Adobe Mobile SDK kan integreras smidigt i ett Swift-projekt med funktionen Mix och Match i iOS Developer Library.

Mer information finns i [Språksamverkan](https://developer.apple.com/documentation/swift#2984801.html).

Om du till exempel använder rubrikmetoden Bridging så som beskrivs i dokumentationen kan du importera rubrikfilen för Adobe Mobile iOS SDK:

```
#import "ADBMobile.h"
```

Använd följande format för att få åtkomst till metoder från SDK i dina Swift-filer:

```
ADBMobile.{methodname}
```
