---
description: Para el contenido en directo/lineal, TVSDK reemplaza un fragmento del contenido del flujo principal con una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo sea la misma.
title: Resolver e insertar publicidad en directo/lineal
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Resuelva e inserte anuncios en directo/lineal {#resolve-and-insert-live-linear-ad}

Para el contenido en directo/lineal, TVSDK reemplaza un fragmento del contenido del flujo principal con una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo sea la misma.

Antes y durante la reproducción, TVSDK resuelve los anuncios conocidos, reemplaza partes del contenido principal por pausas publicitarias de la misma duración y vuelve a calcular la cronología virtual, si es necesario. Las posiciones de las pausas publicitarias se especifican mediante puntos de referencia definidos por el manifiesto.

TVSDK inserta anuncios de las siguientes maneras:

* **Anuncio previo a la emisión**, que se coloca antes del contenido.
* **Mid-roll**, que se coloca en medio del contenido.

TVSDK acepta la pausa publicitaria incluso si la duración es mayor o menor que la duración de sustitución de puntos de referencia. De forma predeterminada, TVSDK admite el `#EXT-X-CUE` cue como marcador de anuncio válido al resolver y colocar anuncios. Este marcador requiere que el valor del campo de metadatos `DURATION` se exprese en segundos y el ID exclusivo del cue. Por ejemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puede definir y suscribirse a indicaciones adicionales (etiquetas).

Una vez iniciada la reproducción, el motor de vídeo actualiza periódicamente el archivo de manifiesto. TVSDK resuelve cualquier anuncio nuevo e inserta los anuncios cuando se encuentra un punto de referencia en el flujo en directo o lineal definido en el manifiesto. Después de resolver e insertar los anuncios, TVSDK vuelve a calcular la cronología virtual y envía un evento `TimelineItemsUpdatedEventListener.onTimelineUpdated`.
