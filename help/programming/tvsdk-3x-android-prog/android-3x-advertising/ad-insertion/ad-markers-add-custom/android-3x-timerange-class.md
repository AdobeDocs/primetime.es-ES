---
description: Los marcadores de anuncios personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de cronología a TVSDK.
title: clase TimeRange
exl-id: f86dee89-15de-4caa-b05c-3e08516b32ce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# clase TimeRange {#timerange-class}

Los marcadores de anuncios personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de cronología a TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada `TimeRange` La especificación del conjunto representa un segmento en la cronología de reproducción que TVSDK mantiene internamente y que debe marcarse adecuadamente como un periodo relacionado con el anuncio.

El `TimeRange` es una estructura de datos sencilla que expone la posición inicial y final en la cronología. Estas dos propiedades de solo lectura abstraen la idea de un intervalo de tiempo en la cronología de reproducción.

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
