---
description: Para el contenido en directo o lineal, el SDK de TVSDK del explorador sustituye una parte del contenido del flujo principal por un salto de publicidad de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.
seo-description: Para el contenido en directo o lineal, el SDK de TVSDK del explorador sustituye una parte del contenido del flujo principal por un salto de publicidad de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.
seo-title: Resolución e inserción de anuncios en directo/lineal
title: Resolución e inserción de anuncios en directo/lineal
uuid: 18c6733a-e827-4b1c-9cd5-796d57cbdb05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Resolución e inserción de anuncios en directo/lineal{#live-linear-ad-resolving-and-insertion}

Para el contenido en directo o lineal, el SDK de TVSDK del explorador sustituye una parte del contenido del flujo principal por un salto de publicidad de la misma duración, de modo que la duración de la línea de tiempo permanezca igual.

Antes y durante la reproducción, el SDK de TVSDK del explorador resuelve anuncios conocidos, reemplaza partes del contenido principal por saltos de publicidad de la misma duración y, si es necesario, vuelve a calcular la línea de tiempo virtual. Las posiciones de los saltos de publicidad se especifican mediante puntos de referencia definidos por el manifiesto.

El SDK de TVSDK de explorador inserta publicidades de las siguientes formas:

* **Anteponer**, que se encuentra al principio del contenido.

El SDK del explorador acepta la pausa publicitaria aunque la duración sea mayor o menor que la duración de sustitución del punto de referencia. De forma predeterminada, el TVSDK del explorador admite el `#EXT-X-CUE` cue como un marcador de publicidad válido al resolver y colocar anuncios. Este marcador requiere el campo de metadatos `DURATION` en segundos y el identificador único de la señal. Por ejemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puede definir y suscribirse a indicaciones (etiquetas) adicionales.

Una vez iniciada la reproducción, el motor de vídeo actualiza periódicamente el archivo de manifiesto. El SDK del explorador resuelve cualquier publicidad nueva e inserta la publicidad cuando se encuentra un punto de referencia en el flujo en directo o lineal definido en el manifiesto. Una vez que se han resuelto e insertado las publicidades, el SDK de TVSDK del explorador vuelve a calcular la línea de tiempo virtual y distribuye un `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` evento.

>[!TIP]
>
>Para flujos en directo, el SDK de TVSDK de explorador solo admite anuncios en formato MP4 y HLS anteriores y en versión intermedia.

