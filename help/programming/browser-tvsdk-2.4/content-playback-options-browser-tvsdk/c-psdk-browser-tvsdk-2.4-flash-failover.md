---
description: El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor de Primetime) que puede integrar con otros componentes de Primetime.
title: Failover de Flash
exl-id: 76bd9214-767a-4f26-977d-81fbac3e0c42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Failover de Flash {#flash-failover}

El TVSDK del explorador proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor de Primetime) que puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en el explorador TVSDK, que tiene métodos para reproducir y administrar vídeos. Por ejemplo, el TVSDK del explorador proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y establecer los botones para llamar a esos métodos TVSDK del explorador.

## reserva de Flash {#section_92D3884A13A6431F9A9CC5C79715D888}

En el TVSDK del explorador, la aplicación interactúa únicamente con el `Primetime.js` API. La implementación TVSDK del explorador subyacente decide qué tecnología de reproductor utilizar en función de la plataforma actual y el tipo de recurso de los medios que se van a reproducir.

La decisión sobre la tecnología del reproductor no se toma hasta que realice una llamada a `MediaPlayer.replaceCurrentResource` para reproducir un recurso específico.

Por ejemplo:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determinar el reproductor multimedia que se va a utilizar {#section_D844E386AF5848688D204DEE258ECEE6}

Este procedimiento de ejemplo ilustra el proceso de determinar la tecnología del reproductor:

>[!TIP]
>
>El proceso puede variar según la dirección URL y el entorno.

1. Si las extensiones de fuente de medios son compatibles, utilícelas sin limitaciones conocidas.
1. Si se admite, utilice el `<video>` etiqueta directamente sin MSE.
1. Asegúrese de utilizar al menos la versión 23.0 del Flash Player de Adobe.
1. Si no se encuentra ninguna tecnología de reproducción adecuada, `replaceCurrentResource` devuelve un error.

Una subsiguiente `replaceCurrentResource` invoque en el mismo `MediaPlayer` La instancia de sigue el mismo proceso. Esto le permite reproducir varios tipos de recursos utilizando el mismo `MediaPlayer` instancia en el mismo elemento principal `<DIV>` que especificó al crear la etiqueta `MediaPlayerView` se ha creado la instancia.

>[!TIP]
>
>El objeto SWF y `<video>` están anidadas en el elemento principal `<DIV>` etiqueta.
