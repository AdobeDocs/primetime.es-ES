---
description: 'El contenido de Reproducción de Evento completo (FER) es un flujo en directo convertido a VOD mediante la adición de la etiqueta #EXT-X-ENDLIST al final del archivo de manifiesto. El flujo conserva sus marcadores de señal de anuncio.'
seo-description: 'El contenido de Reproducción de Evento completo (FER) es un flujo en directo convertido a VOD mediante la adición de la etiqueta #EXT-X-ENDLIST al final del archivo de manifiesto. El flujo conserva sus marcadores de señal de anuncio.'
seo-title: Resolución e inserción de publicidades FER
title: Resolución e inserción de publicidades FER
uuid: 85da0e92-17fe-4001-a53c-085dadd09756
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Resolución e inserción de publicidades FER{#fer-ad-resolving-and-insertion}

El contenido de Reproducción de Evento completo (FER) es un flujo en directo convertido a VOD mediante la adición de la etiqueta #EXT-X-ENDLIST al final del archivo de manifiesto. El flujo conserva sus marcadores de señal de anuncio.

El SDK TVSDK del explorador trata un flujo FER como VOD, por lo que el modo de señalización de publicidad es `SERVER_MAP` de forma predeterminada. Sin embargo, dado que el flujo retiene sus marcadores de señal de publicidad, puede establecer el modo de señalización de publicidad en `MANIFEST_CUES`, que permite utilizar los marcadores de señal de publicidad para la inserción de publicidad.

Para activar la inserción de anuncios mediante marcadores de señal para un flujo FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

El comportamiento de resolución e inserción de anuncios FER es similar a la resolución e inserción de anuncios activos. El TVSDK del explorador hace lo siguiente:

1. Inserta cualquier anuncio previo al principio del contenido.
1. Resuelve las publicidades especificadas por los puntos de referencia definidos en el manifiesto.
1. Reemplaza partes del contenido principal con pausas publicitarias de la misma duración
1. Vuelve a calcular la línea de tiempo virtual, si es necesario.

**Restricción:TVSDK** del explorador solo admite la reproducción de flujos HLS FER. Además, los anuncios de lanzamiento intermedio de MP4 no son compatibles con los flujos FER.
