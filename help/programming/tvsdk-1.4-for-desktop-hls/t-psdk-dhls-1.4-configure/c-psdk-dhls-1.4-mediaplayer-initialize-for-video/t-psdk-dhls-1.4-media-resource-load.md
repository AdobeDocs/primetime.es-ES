---
description: Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir. Esta es una forma de cargar un recurso de medios.
title: Carga de un recurso de medios en MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Cargar un recurso de medios en MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir. Esta es una forma de cargar un recurso de medios.

1. Establezca el elemento que se puede reproducir del objeto `MediaPlayer` con el nuevo recurso que se va a reproducir.

   Reemplace el elemento que MediaPlayer puede reproducir actualmente llamando a `MediaPlayer.replaceCurrentResource` y pasando una instancia `MediaResource` existente.

1. Compruebe al menos los siguientes cambios:

   * INICIALIZADO
   * PREPARADO
   * ERROR

      Mediante estos eventos, el objeto `MediaPlayer` puede notificar a la aplicación cuando el recurso de medios se carga correctamente.

1. Cuando el estado del reproductor de contenidos cambia a INITIALIZADO, puede llamar a `MediaPlayer.prepareToPlay`

   El estado INITIALIZED indica que el medio se ha cargado correctamente. Al llamar a `prepareToPlay` se inicia el proceso de resolución y colocación de publicidad, si existe.

1. Cuando el estado del reproductor de contenidos cambia a PREPARADO, el flujo de medios se ha cargado correctamente y está preparado para la reproducción.

   Cuando se carga el flujo de medios, se crea un `MediaPlayerItem`.

Si se produce un error, MediaPlayer cambia al estado ERROR. También notifica a su aplicación enviando el evento `STATUS_CHANGED` a su llamada de retorno `MediaPlayerStatusChangeEvent`.

Esto pasa varios parámetros:
* Un parámetro `type` de tipo cadena con el valor `ERROR`.

* Un parámetro `MediaError` que puede utilizar para obtener una notificación que contenga información de diagnóstico sobre el evento de error.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso de medios:

```
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
   switch(event.status) { 
      case MediaPlayerStatus.INITIALIZED: 
          // at this point, the resource is successfully loaded 
          // the media player will provide a reference to the current 
          // "playable item" ( is guarantee to be valid and not-null). 
          var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
          // we can take a look at the media item characteristics like 
          // alternate audio tracks, profile information, if is a live stream 
          // if is drm protected 
          mediaPlayer.prepareToPlay(); 
          break; 
    case MediaPlayerStatus.PREPARED: 
         // at this point, the resource is successfully processed all  
         // advertisement placements have been executed and the the  
         // MediaPlayer is ready to start the playback 
        if (autoPlay) { 
            mediaPlayer.play(); 
        } 
        break; 
    case MediaPlayerStatus.ERROR: 
        // something bad happened - the resource cannot be loaded 
        // details about the problem are provided via the event.error property 
        break; 
        // implementation of the other methods in the PlaybackEventListener interface 
        ... 
    } 
}
```
