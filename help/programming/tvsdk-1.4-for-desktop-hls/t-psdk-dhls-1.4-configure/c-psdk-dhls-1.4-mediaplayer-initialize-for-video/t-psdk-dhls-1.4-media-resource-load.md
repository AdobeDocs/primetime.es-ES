---
description: Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir. Esta es una forma de cargar un recurso multimedia.
title: Cargar un recurso multimedia en MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Cargar un recurso multimedia en MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir. Esta es una forma de cargar un recurso multimedia.

1. Configure su `MediaPlayer` elemento reproducible del objeto con el nuevo recurso que se va a reproducir.

   Reemplaza el elemento que se puede reproducir actualmente de MediaPlayer llamando a `MediaPlayer.replaceCurrentResource` y pasar un existente `MediaResource` ejemplo.

1. Compruebe si hay al menos los cambios siguientes:

   * INICIALIZADO
   * PREPARADO
   * ERROR

     A través de estos eventos, la `MediaPlayer` puede notificar a la aplicación cuando el recurso de medios se carga correctamente.

1. Cuando el estado del reproductor de contenidos cambie a INITIALIZED, puede llamar a `MediaPlayer.prepareToPlay`

   El estado INITIALIZED indica que el medio se ha cargado correctamente. Llamando `prepareToPlay` inicia el proceso de resolución y colocación de la publicidad, si lo hay.

1. Cuando el estado del reproductor de contenidos cambia a PREPARADO, el flujo de contenidos se ha cargado correctamente y está preparado para la reproducción.

   Cuando se carga el flujo de medios, una `MediaPlayerItem` se ha creado.

Si se produce un error, MediaPlayer cambia al estado ERROR. También notifica a la aplicación enviando el `STATUS_CHANGED` a su `MediaPlayerStatusChangeEvent` devolución de llamada.

Esto pasa varios parámetros:
* A `type` parámetro de tipo cadena con el valor `ERROR`.

* A `MediaError` parámetro que puede utilizar para obtener una notificación que contenga información de diagnóstico sobre el evento de error.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso multimedia:

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
