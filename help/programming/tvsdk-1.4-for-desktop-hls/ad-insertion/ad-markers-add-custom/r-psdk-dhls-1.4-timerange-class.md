---
description: Los marcadores de publicidad personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de línea de tiempo a TVSDK.
seo-description: Los marcadores de publicidad personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de línea de tiempo a TVSDK.
seo-title: Clase TimeRange
title: Clase TimeRange
uuid: 5d0c979e-cc63-4fdd-becc-b0e3987b0891
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Clase TimeRange{#timerange-class}

Los marcadores de publicidad personalizados le permiten pasar un conjunto de especificaciones de TimeRange que representan segmentos de línea de tiempo a TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada especificación `TimeRange` del conjunto representa un segmento en la línea de tiempo de reproducción que TVSDK mantiene internamente y que debe marcarse adecuadamente como un período relacionado con la publicidad.

La clase `TimeRange` es una estructura de datos sencilla que expone la posición de inicio y la posición final en la línea de tiempo. Estas dos propiedades de sólo lectura abstraen la idea de un intervalo de tiempo en la línea de tiempo de reproducción.

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

