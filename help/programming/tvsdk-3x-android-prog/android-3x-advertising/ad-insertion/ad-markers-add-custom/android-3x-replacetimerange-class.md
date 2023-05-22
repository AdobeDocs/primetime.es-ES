---
description: La clase de utilidad ReplaceTimeRange es una extensión de la clase TimeRange que se va a utilizar con CustomRangeMetadata.
title: ReplaceTimeRange, clase
exl-id: 8d4e9263-bcc0-4300-86ac-6aa7afe5914b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
