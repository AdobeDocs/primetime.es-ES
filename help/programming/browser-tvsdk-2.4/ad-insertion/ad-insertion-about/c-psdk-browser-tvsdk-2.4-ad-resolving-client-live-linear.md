---
description: Para el contenido en directo/lineal, el SDK de explorador sustituye un fragmento del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo sea la misma.
title: Resolución e inserción de anuncios en directo/lineal
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Resolución e inserción de anuncios en directo/lineal{#live-linear-ad-resolving-and-insertion}

Para el contenido en directo/lineal, el SDK de explorador sustituye un fragmento del contenido del flujo principal por una pausa publicitaria de la misma duración, de modo que la duración de la línea de tiempo sea la misma.

Antes y durante la reproducción, el SDK de explorador resuelve los anuncios conocidos, reemplaza partes del contenido principal por pausas publicitarias de la misma duración y vuelve a calcular la cronología virtual, si es necesario. Las posiciones de las pausas publicitarias se especifican mediante puntos de referencia definidos por el manifiesto.

El TVSDK del explorador inserta los anuncios de las siguientes maneras:

* **Anuncio previo a la emisión**, que se encuentra al principio del contenido.

El TVSDK del explorador acepta la pausa publicitaria incluso si la duración es mayor o menor que la duración de sustitución de puntos de referencia. De forma predeterminada, el SDK de explorador admite la señal `#EXT-X-CUE` como un marcador de anuncio válido al resolver y colocar anuncios. Este marcador requiere el campo de metadatos `DURATION` en segundos y el ID exclusivo del cue. Por ejemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puede definir y suscribirse a indicaciones adicionales (etiquetas).

Una vez iniciada la reproducción, el motor de vídeo actualiza periódicamente el archivo de manifiesto. El TVSDK del explorador resuelve cualquier publicidad nueva e inserta la publicidad cuando se encuentra un punto de referencia en el flujo en directo o lineal definido en el manifiesto. Después de resolver e insertar los anuncios, el SDK de TVSDK del explorador vuelve a calcular la cronología virtual y envía un evento `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.

>[!TIP]
>
>Para emisiones en directo, el SDK de explorador TVSDK solo admite anuncios previos y finales de MP4 y HLS.

