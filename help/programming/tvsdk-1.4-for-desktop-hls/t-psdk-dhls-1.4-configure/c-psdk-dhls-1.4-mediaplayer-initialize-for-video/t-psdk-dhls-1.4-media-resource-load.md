---
description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.
seo-description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.
seo-title: Cargar un recurso de medios en MediaPlayer
title: Cargar un recurso de medios en MediaPlayer
uuid: 8af3e8d1-359d-483c-b394-b95054f7265a
translation-type: tm+mt
source-git-commit: 84924d84bfa436a8807c2e8d74d1dc268d457051

---


# Cargar un recurso de medios en MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.

1. Configure el elemento que se puede reproducir del `MediaPlayer` objeto con el nuevo recurso que se va a reproducir.

   Reemplace el elemento que se puede reproducir en este momento en MediaPlayer llamando `MediaPlayer.replaceCurrentResource` y pasando una `MediaResource` instancia existente.

1. Compruebe al menos los cambios siguientes:

   * INICIALIZADO
   * PREPARADO
   * ERROR

      Mediante estos eventos, el `MediaPlayer` objeto puede notificar a la aplicación cuando el recurso de medios se cargue correctamente.

1. Cuando el estado del reproductor de medios cambia a INICIALIZADO, puede llamar a `MediaPlayer.prepareToPlay`

   El estado INITIALIZED indica que el medio se ha cargado correctamente. La llamada `prepareToPlay` inicio el proceso de resolución y colocación de la publicidad, si existe.

1. Cuando el estado del reproductor de medios cambia a PREPARADO, el flujo de medios se ha cargado correctamente y está preparado para la reproducción.

   Cuando se carga el flujo de medios, `MediaPlayerItem` se crea un.

Si se produce un error, MediaPlayer cambia al estado ERROR. También notifica a la aplicación enviando el `STATUS_CHANGED` evento a la `MediaPlayerStatusChangeEvent` llamada de retorno.

Esto pasa varios parámetros:
* Un `type` parámetro de tipo cadena con el valor `ERROR`.

* Parámetro `MediaError` que puede utilizar para obtener una notificación que contenga información de diagnóstico sobre el evento de error.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

El siguiente código de muestra simplificado ilustra el proceso de carga de un recurso de medios:

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
