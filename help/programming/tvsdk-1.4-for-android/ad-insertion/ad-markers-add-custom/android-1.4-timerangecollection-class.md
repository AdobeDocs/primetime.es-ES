---
description: La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse a sí misma en una instancia de metadatos.
title: clase TimeRangeCollection
exl-id: 1af41267-c222-43ac-84ca-0bf37b6a59de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# clase TimeRangeCollection{#timerangecollection-class}

La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse a sí misma en una instancia de metadatos.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}
```

El `type` parameter, que es el primer parámetro de posición en la firma de los métodos constructores, es una instancia de `TimeRangeCollection#Type` enumeración. Esto forma parte de la `TimeRangeCollection` clase. Los valores definidos actualmente por esta enumeración son `MARK_RANGES`, `DELETE_RANGES`, y `REPLACE_RANGES`. Puede crear `TimeRangeCollection` que utilizan estos tres tipos.
