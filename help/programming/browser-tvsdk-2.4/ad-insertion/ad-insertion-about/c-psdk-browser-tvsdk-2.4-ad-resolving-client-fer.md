---
description: 'El contenido de Reproducción de eventos completos (FER) es una emisión en directo convertida a VOD al añadir la etiqueta #EXT-X-ENDLIST al final del archivo de manifiesto. El flujo conserva sus marcadores de señal de anuncio.'
title: FER resolución de publicidad e inserción
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# FER resolución de publicidad e inserción{#fer-ad-resolving-and-insertion}

El contenido de Reproducción de eventos completos (FER) es una emisión en directo convertida a VOD al añadir la etiqueta #EXT-X-ENDLIST al final del archivo de manifiesto. El flujo conserva sus marcadores de señal de anuncio.

El SDK del explorador considera un flujo FER como VOD, por lo que el modo de señalización de anuncio predeterminado es `SERVER_MAP`. Sin embargo, dado que el flujo conserva sus marcadores de señal de anuncio, puede establecer el modo de señalización de anuncio en `MANIFEST_CUES`, que permite utilizar los marcadores de señal de anuncio para la inserción de anuncio.

Para activar la inserción de anuncios utilizando marcadores de señal para un flujo FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

El comportamiento de resolución e inserción de anuncios FER es similar al de resolución e inserción de anuncios en directo. El TVSDK del explorador hace lo siguiente:

1. Inserta cualquier anuncio pre-roll al principio del contenido.
1. Resuelve anuncios especificados por los puntos de referencia definidos en el manifiesto.
1. Reemplaza partes del contenido principal con pausas publicitarias de la misma duración
1. Vuelva a calcular la cronología virtual, si es necesario.

**Restricción:** El SDK de explorador solo admite la reproducción de flujos HLS FER. Además, los anuncios mid-roll de MP4 no son compatibles con los flujos FER.
