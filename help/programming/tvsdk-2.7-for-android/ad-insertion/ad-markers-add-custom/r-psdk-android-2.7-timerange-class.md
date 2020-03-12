---
description: Los marcadores de publicidad personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de línea de tiempo a TVSDK.
seo-description: Los marcadores de publicidad personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de línea de tiempo a TVSDK.
seo-title: Clase TimeRange
title: Clase TimeRange
uuid: e5a176af-29b9-4aa6-848e-5aba7988584b
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Clase TimeRange {#timerange-class}

Los marcadores de publicidad personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de línea de tiempo a TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada `TimeRange` especificación del conjunto representa un segmento en la línea de tiempo de reproducción que TVSDK mantiene internamente y que debe marcarse adecuadamente como un período relacionado con la publicidad.

La `TimeRange` clase es una estructura de datos sencilla que expone la posición inicial y la posición final en la línea de tiempo. Estas dos propiedades de sólo lectura abstraen la idea de un intervalo de tiempo en la línea de tiempo de reproducción.

>[!TIP]
>
>Ambos valores se expresan en milisegundos.

Este es un resumen de la `TimeRange` clase:

```java
public final class TimeRange {
    // the start/end values are provided at construction time
    public static TimeRange createRange(long begin, long duration) {...} 

    // only getters are available
    public long getBegin() {...} 
    public long getEnd() {...} 
    public long getDuration() {...}
}
```

