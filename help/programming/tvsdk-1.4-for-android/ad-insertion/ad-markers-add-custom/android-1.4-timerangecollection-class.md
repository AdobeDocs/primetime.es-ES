---
description: La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse en una instancia de metadatos.
seo-description: La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse en una instancia de metadatos.
seo-title: Clase TimeRangeCollection
title: Clase TimeRangeCollection
uuid: 5705dc9d-4325-44b0-b5aa-196d09c3a67e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Clase TimeRangeCollection{#timerangecollection-class}

La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse en una instancia de metadatos.

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

El `type` parámetro, que es el primer parámetro posicional en la firma de los métodos constructores, es una instancia de la `TimeRangeCollection#Type` enumeración. Esto es parte de la `TimeRangeCollection` clase. Los valores definidos actualmente por esta enumeración son `MARK_RANGES`, `DELETE_RANGES`y `REPLACE_RANGES`. Puede crear `TimeRangeCollection` objetos utilizando estos tres tipos.
