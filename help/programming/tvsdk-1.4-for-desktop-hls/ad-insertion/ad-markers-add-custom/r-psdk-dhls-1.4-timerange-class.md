---
description: Los marcadores de anuncios personalizados le permiten pasar a TVSDK un conjunto de especificaciones de intervalo de tiempo que representan segmentos de cronología.
title: Clase TimeRange
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Clase TimeRange{#timerange-class}

Los marcadores de anuncios personalizados le permiten pasar a TVSDK un conjunto de especificaciones de intervalo de tiempo que representan segmentos de cronología.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada especificación `TimeRange` del conjunto representa un segmento en la línea de tiempo de reproducción que TVSDK mantiene internamente y que debe marcarse apropiadamente como un periodo relacionado con la publicidad.

La clase `TimeRange` es una estructura de datos sencilla que expone la posición de inicio y la posición final en la cronología. Estas dos propiedades de solo lectura abstraen la idea de un intervalo de tiempo en la línea de tiempo de reproducción.

>[!TIP]
>
>Ambos valores se expresan en milisegundos.

Este es un resumen de la clase TimeRange:

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```

