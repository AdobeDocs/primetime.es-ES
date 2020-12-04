---
description: La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se utilizará con CustomRangeMetadata.
seo-description: La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se utilizará con CustomRangeMetadata.
seo-title: Clase ReplaceTimeRange
title: Clase ReplaceTimeRange
uuid: 19c49b26-5096-4429-b30b-bdd2502e3036
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

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

