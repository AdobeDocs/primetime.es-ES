---
description: El SDK de explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor Primetime), que puede integrar con otros componentes de Primetime.
title: Failover de Flash
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Failover de Flash {#flash-failover}

El SDK de explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor Primetime), que puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en el explorador TVSDK, que tiene métodos para reproducir y administrar vídeos. Por ejemplo, el SDK de explorador proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y establecer los botones para llamar a esos métodos TVSDK del explorador.

## reserva de Flash {#section_92D3884A13A6431F9A9CC5C79715D888}

En el SDK de TVSDK del explorador, la aplicación solo interactúa con la API `Primetime.js`. La implementación subyacente del SDK de TVSDK del explorador decide qué tecnología de reproductor utilizar en función de la plataforma actual y el tipo de recurso del medio que se va a reproducir.

La decisión para la tecnología del reproductor no se toma hasta que llama a `MediaPlayer.replaceCurrentResource` para reproducir un recurso específico.

Por ejemplo:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determinar el reproductor de contenidos que se va a utilizar {#section_D844E386AF5848688D204DEE258ECEE6}

Este procedimiento de ejemplo ilustra el proceso de determinación de la tecnología del reproductor:

>[!TIP]
>
>El proceso puede variar según la dirección URL y el entorno.

1. Si se admiten extensiones de fuente de medios, utilícelo sin limitaciones conocidas.
1. Si es compatible, utilice la etiqueta `<video>` directamente sin MSE.
1. Compruebe que está utilizando al menos la versión 23.0 del Flash Player de Adobe.
1. Si no se encuentra ninguna tecnología de reproducción adecuada, `replaceCurrentResource` devuelve un error.

Una llamada `replaceCurrentResource` posterior en la misma instancia `MediaPlayer` sigue el mismo proceso. Esto le permite reproducir varios tipos de recursos utilizando la misma instancia `MediaPlayer` en la misma etiqueta principal `<DIV>` que especificó cuando se creó la instancia `MediaPlayerView`.

>[!TIP]
>
>El objeto SWF y la etiqueta `<video>` están anidadas en la etiqueta principal `<DIV>`.

