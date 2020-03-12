---
description: Puede especificar o anular las líneas de tiempo para los saltos de publicidad en el contenido de VOD mediante una lista formateada de segmentos de publicidad y contenido llamados pods.
seo-description: Puede especificar o anular las líneas de tiempo para los saltos de publicidad en el contenido de VOD mediante una lista formateada de segmentos de publicidad y contenido llamados pods.
seo-title: Formato de línea de tiempo VOD
title: Formato de línea de tiempo VOD
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Formato de línea de tiempo VOD {#vod-timeline-format}

Puede especificar o anular las líneas de tiempo para los saltos de publicidad en el contenido de VOD mediante una lista formateada de segmentos de publicidad y contenido llamados pods.

## Pods {#section_606E9456E25E41C8B8537A023DDD96CE}

Un pod es una pausa publicitaria o un segmento de contenido. Una línea de tiempo consiste en una secuencia de pods, separados por punto y coma. Existen los siguientes tipos de pods:

### Salto de publicidad

```
B,duration,maximum_number_of_ads,position
```

La duración es en segundos, con una precisión de 0,001 (milisegundos); el número de publicidades es un número entero. La posición es una de las siguientes:
* **n** ninguno — sin anuncio* **p** previo — antes del contenido* **m** Mid-roll — dentro del contenido* **t** Post-roll — después del contenido

Por ejemplo, `B,60,2,p` representa un desglose de un minuto para un máximo de 2 publicidades antes del contenido.

### Segmento de contenido: capítulo

```
C,duration,number_of_lots
```

La duración es en segundos, con una precisión de 0,001 (milisegundos); número de lotes (secciones de contenido) es un número entero. Por ejemplo, `C,300,1` representa una sola sección de contenido de cinco minutos.