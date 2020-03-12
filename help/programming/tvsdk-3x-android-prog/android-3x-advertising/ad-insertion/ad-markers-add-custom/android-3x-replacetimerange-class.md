---
description: La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se utilizará con CustomRangeMetadata.
seo-description: La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se utilizará con CustomRangeMetadata.
seo-title: Clase ReplaceTimeRange
title: Clase ReplaceTimeRange
uuid: d554c17a-2bdc-4c4a-bb8f-2d357511bb32
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Clase ReplaceTimeRange {#replacetimerange-class}

La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se utilizará con CustomRangeMetadata.

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
