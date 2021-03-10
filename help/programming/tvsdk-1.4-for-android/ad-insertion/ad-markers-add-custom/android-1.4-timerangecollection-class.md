---
description: La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse a sí misma en una instancia de metadatos.
title: Clase TimeRangeCollection
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Clase TimeRangeCollection{#timerangecollection-class}

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

El parámetro `type`, que es el primer parámetro posicional en la firma de los métodos constructores, es una instancia de la enumeración `TimeRangeCollection#Type`. Esto forma parte de la clase `TimeRangeCollection`. Los valores que están definidos actualmente por esta enumeración son `MARK_RANGES`, `DELETE_RANGES` y `REPLACE_RANGES`. Puede crear objetos `TimeRangeCollection` utilizando estos tres tipos.
