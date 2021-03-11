---
description: Puede especificar o anular las líneas de tiempo para las pausas publicitarias en el contenido de VOD usando una lista formateada de segmentos de anuncios y contenido llamados pods.
title: Formato de la cronología de VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Formato de cronología de VOD {#vod-timeline-format}

Puede especificar o anular las líneas de tiempo para las pausas publicitarias en el contenido de VOD usando una lista formateada de segmentos de anuncios y contenido llamados pods.

## Pods {#section_606E9456E25E41C8B8537A023DDD96CE}

Un pod es una pausa publicitaria o un segmento de contenido. Una cronología consiste en una secuencia de pods, separados por punto y coma. Existen los siguientes tipos de pods:

### Pausa publicitaria

```
B,duration,maximum_number_of_ads,position
```

La duración se expresa en segundos, con una precisión de 0,001 (milisegundos); número de anuncios es un número entero. La posición es una de las siguientes:
* **n** Ninguno — sin publicidad
* **p** Anuncio previo a la emisión: antes del contenido
* **m** Mid-roll: dentro del contenido
* **t** Anuncio posterior a la emisión: después del contenido

Por ejemplo, `B,60,2,p` representa un desglose de un minuto para un máximo de 2 anuncios antes del contenido.

### Segmento de contenido: capítulo

```
C,duration,number_of_lots
```

La duración se expresa en segundos, con una precisión de 0,001 (milisegundos); número de lotes (secciones de contenido) es un número entero. Por ejemplo, `C,300,1` representa una sola sección de contenido de cinco minutos.