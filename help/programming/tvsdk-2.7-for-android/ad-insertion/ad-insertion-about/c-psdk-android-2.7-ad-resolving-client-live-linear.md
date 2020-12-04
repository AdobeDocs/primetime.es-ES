---
description: Para el contenido en directo o lineal, TVSDK sustituye una parte del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.
seo-description: Para el contenido en directo o lineal, TVSDK sustituye una parte del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.
seo-title: Resolver e insertar publicidad en directo/lineal
title: Resolver e insertar publicidad en directo/lineal
uuid: c9d54fc9-1d54-41c3-a872-d27afdd16314
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Resolver e insertar publicidades en directo/lineales {#resolve-and-insert-live-linear-ad}

Para el contenido en directo o lineal, TVSDK sustituye una parte del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.

Antes y durante la reproducción, TVSDK resuelve los anuncios conocidos, reemplaza partes del contenido principal con pausas publicitarias de la misma duración y, si es necesario, vuelve a calcular la línea de tiempo virtual. Las posiciones de los saltos de publicidad se especifican mediante puntos de referencia definidos por el manifiesto.

TVSDK inserta publicidades de las siguientes formas:

* **Anteponer**, que se coloca antes del contenido.
* **Mid-roll**, que se coloca en medio del contenido.

TVSDK acepta la pausa publicitaria aunque la duración sea más larga o más corta que la duración de sustitución de puntos de referencia. De forma predeterminada, TVSDK admite la señal `#EXT-X-CUE` como un marcador de publicidad válido al resolver y colocar publicidades. Este marcador requiere que el valor del campo de metadatos `DURATION` se exprese en segundos y el identificador único del cue. Por ejemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puede definir y suscribirse a indicaciones (etiquetas) adicionales.

Después de los inicios de reproducción, el motor de vídeo actualiza periódicamente el archivo de manifiesto. TVSDK resuelve cualquier publicidad nueva e inserta la publicidad cuando se encuentra un punto de referencia en el flujo activo o lineal definido en el manifiesto. Una vez que las publicidades se resuelven y se insertan, TVSDK vuelve a calcular la línea de tiempo virtual y distribuye un evento `TimelineItemsUpdatedEventListener.onTimelineUpdated`.
