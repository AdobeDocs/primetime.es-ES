---
description: El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que se puede integrar con otros componentes de Primetime.
seo-description: El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que se puede integrar con otros componentes de Primetime.
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Failover de Flash {#flash-failover}

El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que se puede integrar con otros componentes de Primetime.

Utilice las herramientas de la plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en el SDK de TVSDK del explorador, que dispone de métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK de explorador proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y definir los botones para llamar a esos métodos de TVSDK del explorador.

## Flash de reserva {#section_92D3884A13A6431F9A9CC5C79715D888}

En el TVSDK del explorador, la aplicación solo interactúa con la API `Primetime.js`. La implementación subyacente de TVSDK del explorador decide qué tecnología de reproductor utilizar en función de la plataforma actual y el tipo de recurso del medio que se va a reproducir.

La decisión de la tecnología del reproductor no se toma hasta que llama a `MediaPlayer.replaceCurrentResource` para reproducir un recurso específico.

Por ejemplo:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determinar el reproductor de medios para utilizar {#section_D844E386AF5848688D204DEE258ECEE6}

Este procedimiento de muestra ilustra el proceso de determinación de la tecnología del reproductor:

>[!TIP]
>
>El proceso puede variar según la dirección URL y el entorno.

1. Si se admiten las extensiones de Media Source, utilícelo sin limitaciones conocidas.
1. Si se admite, utilice la etiqueta `<video>` directamente sin MSE.
1. Asegúrese de que está utilizando al menos Adobe Flash Player versión 23.0.
1. Si no se encuentra ninguna tecnología de reproducción adecuada, `replaceCurrentResource` devuelve un error.

Una llamada subsiguiente `replaceCurrentResource` en la misma instancia `MediaPlayer` sigue el mismo proceso. Esto le permite reproducir varios tipos de recursos utilizando la misma instancia `MediaPlayer` en la misma etiqueta principal `<DIV>` que especificó cuando se creó la instancia `MediaPlayerView`.

>[!TIP]
>
>El objeto SWF y la etiqueta `<video>` están anidados en la etiqueta principal `<DIV>`.

