---
description: Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir. Esta es una forma de cargar un recurso de medios.
title: Carga de un recurso de medios en MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Cargar un recurso de medios en MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir. Esta es una forma de cargar un recurso de medios.

1. Establezca el elemento que se puede reproducir en MediaPlayer con el nuevo recurso que se va a reproducir.

   Reemplace el elemento que MediaPlayer puede reproducir actualmente llamando a `MediaPlayer.replaceCurrentItem` y pasando una instancia `MediaResource` existente.

1. Registre una implementación de la interfaz `MediaPlayer.PlaybackEventListener` con la instancia `MediaPlayer`.

   * `onPrepared`
   * `onStateChanged`, y compruebe si hay INICIALIZADO y ERROR.

1. Cuando el estado del reproductor de contenidos cambia a INITIALIZADO, puede llamar a `MediaPlayer.prepareToPlay`

   El estado INITIALIZED indica que el medio se ha cargado correctamente. Al llamar a `prepareToPlay` se inicia el proceso de resolución y colocación de publicidad, si existe.

1. Cuando TVSDK llama a la llamada de retorno `onPrepared` , el flujo de medios se ha cargado correctamente y está preparado para la reproducción.

   Cuando se carga el flujo de medios, se crea un `MediaPlayerItem`.

>Si se produce un error, el `MediaPlayer` cambia al estado ERROR. También notifica a la aplicación llamando a la llamada de retorno `PlaybackEventListener.onStateChanged`.
>
>Esto pasa varios parámetros:
>* Un parámetro `state` de tipo `MediaPlayer.PlayerState` con el valor `MediaPlayer.PlayerState.ERROR`.
   >
   >
* Un parámetro `notification` de tipo `MediaPlayerNotification` que contiene información de diagnóstico sobre el evento de error.


El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso de medios:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 
```
