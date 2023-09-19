---
description: La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se va a utilizar con CustomRangeMetadata.
title: ReplaceTimeRange, clase
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 0%

---

# ReplaceTimeRange, clase {#replacetimerange-class}

La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se va a utilizar con CustomRangeMetadata.

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}
```
