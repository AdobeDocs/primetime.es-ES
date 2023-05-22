---
description: Para el contenido en directo/lineal, TVSDK reemplaza una parte del contenido del flujo principal con una pausa publicitaria de la misma duración, de modo que la duración de la cronología sigue siendo la misma.
title: Resolución e inserción de un anuncio en directo/lineal
exl-id: 2fe55c07-54d2-4a8a-a4e1-9e5ccae17ff9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Resolución e inserción de anuncios en directo/lineales {#resolve-and-insert-live-linear-ad}

Para el contenido en directo/lineal, TVSDK reemplaza una parte del contenido del flujo principal con una pausa publicitaria de la misma duración, de modo que la duración de la cronología sigue siendo la misma.

Antes y durante la reproducción, TVSDK resuelve los anuncios conocidos, reemplaza partes del contenido principal por pausas publicitarias de la misma duración y vuelve a calcular la cronología virtual, si es necesario. Las posiciones de las pausas publicitarias se especifican mediante puntos de referencia definidos por el manifiesto.

TVSDK inserta anuncios de las siguientes maneras:

* **Pre-roll**, que se coloca antes del contenido.
* **Mid-roll**, que se coloca en medio del contenido.

TVSDK acepta la pausa publicitaria incluso si la duración es mayor o menor que la duración de sustitución del punto de referencia. De forma predeterminada, TVSDK admite `#EXT-X-CUE` Indicar como marcador de anuncio válido al resolver y colocar anuncios. Este marcador requiere el campo de metadatos. `DURATION` valor que se expresará en segundos y el ID único de la señal. Por ejemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puede definir y suscribirse a indicaciones adicionales (etiquetas).

Una vez iniciada la reproducción, el motor de vídeo actualiza periódicamente el archivo de manifiesto. TVSDK resuelve cualquier anuncio nuevo e inserta los anuncios cuando se encuentra un punto de referencia en el flujo en directo o lineal definido en el manifiesto. Una vez resueltos e insertados los anuncios, TVSDK vuelve a calcular la cronología virtual y envía un `TimelineItemsUpdatedEventListener.onTimelineUpdated` evento.
