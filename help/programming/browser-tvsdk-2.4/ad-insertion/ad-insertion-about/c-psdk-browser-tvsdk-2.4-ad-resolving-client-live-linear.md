---
description: Para el contenido en directo/lineal, TVSDK del explorador reemplaza una parte del contenido del flujo principal con una pausa publicitaria de la misma duración, de modo que la duración de la cronología sigue siendo la misma.
title: Resolución e inserción de anuncios lineales/activos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Resolución e inserción de anuncios lineales/activos{#live-linear-ad-resolving-and-insertion}

Para el contenido en directo/lineal, TVSDK del explorador reemplaza una parte del contenido del flujo principal con una pausa publicitaria de la misma duración, de modo que la duración de la cronología sigue siendo la misma.

Antes y durante la reproducción, el TVSDK del explorador resuelve los anuncios conocidos, reemplaza partes del contenido principal por pausas publicitarias de la misma duración y vuelve a calcular la cronología virtual, si es necesario. Las posiciones de las pausas publicitarias se especifican mediante puntos de referencia definidos por el manifiesto.

TVSDK del explorador inserta anuncios de las siguientes maneras:

* **Pre-roll**, que se encuentra al principio del contenido.

El TVSDK del explorador acepta la pausa publicitaria aunque la duración sea mayor o menor que la duración de reemplazo del punto de referencia. De forma predeterminada, el TVSDK del explorador admite `#EXT-X-CUE` Indicar como marcador de anuncio válido al resolver y colocar anuncios. Este marcador requiere el campo de metadatos. `DURATION` en segundos y el ID único de la señal. Por ejemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puede definir y suscribirse a indicaciones adicionales (etiquetas).

Una vez iniciada la reproducción, el motor de vídeo actualiza periódicamente el archivo de manifiesto. TVSDK del explorador resuelve cualquier anuncio nuevo e inserta los anuncios cuando se encuentra un punto de referencia en el flujo en directo o lineal definido en el manifiesto. Una vez resueltos e insertados los anuncios, Browser TVSDK vuelve a calcular la cronología virtual y envía un `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` evento.

>[!TIP]
>
>Para los flujos en directo, el TVSDK del explorador solo admite anuncios previos a la emisión y mid-roll MP4 y HLS.
