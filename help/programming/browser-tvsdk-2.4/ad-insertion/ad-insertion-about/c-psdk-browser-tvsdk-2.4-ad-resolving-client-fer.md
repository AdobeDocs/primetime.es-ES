---
description: El contenido de Reproducción completa de eventos (FER) es un flujo en directo convertido a VOD que agrega la etiqueta
title: Resolución e inserción de anuncios FER
exl-id: 9075932d-4e77-4249-af5d-0b392033907f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Resolución e inserción de anuncios FER{#fer-ad-resolving-and-insertion}

El contenido de Reproducción completa de eventos (FER) es un flujo en directo convertido a VOD que agrega la etiqueta #EXT-X-ENDLIST al final del archivo de manifiesto. El flujo conserva sus marcadores de señal de anuncio.

TVSDK del explorador trata un flujo FER como VOD, por lo que de forma predeterminada el modo de señalización de publicidad es `SERVER_MAP`. Sin embargo, dado que el flujo conserva sus marcadores de señal de anuncio, puede establecer el modo de señalización de anuncio en `MANIFEST_CUES`, que permite utilizar los marcadores de señal de anuncio para la inserción de anuncios.

Para activar la inserción de anuncios con marcadores de señal para un flujo FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

El comportamiento de resolución e inserción de anuncios FER es similar al de resolución e inserción de anuncios en directo. El TVSDK del explorador hace lo siguiente:

1. Inserta anuncios previos a la emisión al principio del contenido.
1. Resuelve los anuncios especificados por los puntos de referencia definidos en el manifiesto.
1. Reemplaza partes del contenido principal por pausas publicitarias de la misma duración
1. Vuelve a calcular la escala de tiempo virtual, si es necesario.

**Restricción:** El TVSDK del explorador solo admite la reproducción de flujos FER de HLS. Además, los anuncios mid-roll de MP4 no son compatibles con flujos FER.
