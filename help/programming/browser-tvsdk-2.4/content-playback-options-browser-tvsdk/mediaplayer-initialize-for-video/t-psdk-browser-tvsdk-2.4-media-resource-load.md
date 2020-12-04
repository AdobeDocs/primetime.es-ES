---
description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir.
seo-description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir.
seo-title: Cargar un recurso de medios en MediaPlayer
title: Cargar un recurso de medios en MediaPlayer
uuid: ac31ccfe-161d-41a2-9a6e-38fae11ceab5
translation-type: tm+mt
source-git-commit: 7d61a6cd8cb2c381f85a19d9ccac3d235ffceaf1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Cargar un recurso de medios en MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir.

1. Configure el elemento que se puede reproducir del objeto `MediaPlayer` con el nuevo recurso que se va a reproducir.

   Reemplace el elemento del objeto `MediaPlayer` que se puede reproducir en ese momento llamando a `replaceCurrentResource` y pasando una instancia `MediaResource` existente.

1. Espere a que el TVSDK del explorador distribuya `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status` que sea igual a cualquiera de los siguientes:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      A través de estos eventos, el objeto MediaPlayer notifica a la aplicación si el recurso multimedia se ha cargado correctamente.

1. Cuando el estado del reproductor de medios cambia a `MediaPlayerStatus.INITIALIZED`, puede llamar a `MediaPlayer.prepareToPlay`.

   El estado INITIALIZED indica que el medio se ha cargado correctamente. La llamada `prepareToPlay` inicio la resolución de publicidad y el proceso de colocación, si existe.
1. Cuando TVSDK del explorador distribuye el evento `MediaPlayerStatus.PREPARED`, el flujo de medios se ha cargado correctamente (se ha creado un elemento MediaPlayerItem) y está preparado para la reproducción.

Si se produce un error, `MediaPlayer` cambia a `MediaPlayerStatus.ERROR`.

También notifica a la aplicación mediante el envío del evento `MediaPlayerStatus.ERROR`.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


El siguiente código de muestra simplificado ilustra el proceso de carga de un recurso de medios:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
