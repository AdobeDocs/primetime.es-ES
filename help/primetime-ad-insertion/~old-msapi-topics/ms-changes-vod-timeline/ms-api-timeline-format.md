---
description: Puede especificar o anular las escalas de tiempo de los saltos de publicidad en el contenido de VOD mediante una lista con formato de segmentos de contenido y anuncios llamados pods.
title: Formato de cronología de VOD
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Formato de cronología de VOD {#vod-timeline-format}

Puede especificar o anular las escalas de tiempo de los saltos de publicidad en el contenido de VOD mediante una lista con formato de segmentos de contenido y anuncios llamados pods.

## Pods {#section_606E9456E25E41C8B8537A023DDD96CE}

Un pod es una pausa publicitaria o un segmento de contenido. Una línea de tiempo consta de una secuencia de pods, separados por punto y coma. Existen los siguientes tipos de pods:

### Pausa para anuncios

```
B,duration,maximum_number_of_ads,position
```

La duración es en segundos, con una precisión de 0,001 (milisegundos); el número de anuncios es un número entero. La posición es una de las siguientes: * **n** Ninguno — sin anuncio * **p** Anuncio previo a la emisión: antes del contenido **m** Mid-roll: dentro del contenido * **t** Post-roll: después del contenido

Por ejemplo, `B,60,2,p` representa una pausa de un minuto para un máximo de 2 anuncios antes del contenido.

### Segmento de contenido: capítulo

```
C,duration,number_of_lots
```

La duración se expresa en segundos con una precisión de 0,001 (milisegundos); el número de lotes (secciones de contenido) es un número entero. Por ejemplo, `C,300,1` representa una sola sección de contenido de cinco minutos.