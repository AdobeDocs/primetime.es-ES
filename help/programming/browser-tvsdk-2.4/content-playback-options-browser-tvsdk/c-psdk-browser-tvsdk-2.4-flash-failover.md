---
description: El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que puede integrar con otros componentes de Primetime.
seo-description: El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que puede integrar con otros componentes de Primetime.
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Conmutación por error Flash {#flash-failover}

El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en el TVSDK del explorador, que dispone de métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK de explorador proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y definir los botones para llamar a esos métodos de TVSDK del explorador.

## Flash fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

En el TVSDK del explorador, la aplicación solo interactúa con la `Primetime.js` API. La implementación subyacente de TVSDK del explorador decide qué tecnología de reproductor utilizar en función de la plataforma actual y el tipo de recurso del medio que se va a reproducir.

La decisión para la tecnología del reproductor no se toma hasta que se llama `MediaPlayer.replaceCurrentResource` a jugar un recurso específico.

Por ejemplo:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determinar el reproductor de medios que se va a utilizar {#section_D844E386AF5848688D204DEE258ECEE6}

Este procedimiento de muestra ilustra el proceso de determinación de la tecnología del reproductor:

>[!TIP]
>
>El proceso puede variar según la dirección URL y el entorno.

1. Si se admiten las extensiones de Media Source, utilícelo sin limitaciones conocidas.
1. Si se admite, utilice la `<video>` etiqueta directamente sin MSE.
1. Asegúrese de que está utilizando al menos Adobe Flash Player versión 23.0.
1. Si no se encuentra ninguna tecnología de reproducción adecuada, `replaceCurrentResource` devuelve un error.

Una llamada posterior `replaceCurrentResource` a la misma `MediaPlayer` instancia sigue el mismo proceso. Esto le permite reproducir varios tipos de recursos utilizando la misma `MediaPlayer` instancia en la misma `<DIV>` etiqueta principal que especificó cuando se creó la `MediaPlayerView` instancia.

>[!TIP]
>
>El objeto SWF y la `<video>` etiqueta están anidados en la `<DIV>` etiqueta principal.

