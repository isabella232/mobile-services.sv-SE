---
description: iOS Adobe Mobile SDK kan integreras smidigt i ett Swift-projekt med hjälp av Mix- och Match-funktionen i iOS Developer Library.
solution: Experience Cloud,Analytics
title: Snabb integrering
topic-fix: Developer and implementation
uuid: 5fb77b57-cbf9-4bcf-8b41-65a933bf9336
exl-id: 3c1a2e28-53b0-4128-a5d9-d2403885098d
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Snabb integrering {#swift-integration}

iOS Adobe Mobile SDK kan integreras smidigt i ett Swift-projekt med hjälp av Mix- och Match-funktionen i iOS Developer Library.

Mer information finns i [Språkinteroperabilitet](https://developer.apple.com/documentation/swift#2984801.html).

Om du till exempel använder rubrikmetoden Bridging så som beskrivs i dokumentationen kan du importera SDK-rubrikfilen för Adobe Mobile iOS:

```
#import "ADBMobile.h"
```

Använd följande format för att få åtkomst till metoder från SDK i dina Swift-filer:

```
ADBMobile.{methodname}
```
