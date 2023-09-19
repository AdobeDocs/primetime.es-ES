---
description: Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir. Esta es una forma de cargar un recurso multimedia.
title: Cargar un recurso multimedia en MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Cargar un recurso multimedia en MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir. Esta es una forma de cargar un recurso multimedia.

1. Configure el elemento reproducible del MediaPlayer con el nuevo recurso que se va a reproducir.

   Reemplaza el elemento que se puede reproducir actualmente de MediaPlayer llamando a `MediaPlayer.replaceCurrentItem` y pasar un existente `MediaResource` ejemplo.

1. Registre una implementación de `MediaPlayer.PlaybackEventListener` interfaz con el `MediaPlayer` ejemplo.

   * `onPrepared`
   * `onStateChanged`y compruebe si hay INITIALIZED y ERROR.

1. Cuando el estado del reproductor de contenidos cambie a INITIALIZED, puede llamar a `MediaPlayer.prepareToPlay`

   El estado INITIALIZED indica que el medio se ha cargado correctamente. Llamando `prepareToPlay` inicia el proceso de resolución y colocación de la publicidad, si lo hay.

1. Cuando TVSDK llama a `onPrepared` llamada de retorno, el flujo de medios se ha cargado correctamente y está preparado para la reproducción.

   Cuando se carga el flujo de medios, una `MediaPlayerItem` se ha creado.

>Si se produce un error, la variable `MediaPlayer` cambia al estado ERROR. También notifica a la aplicación llamando a su `PlaybackEventListener.onStateChanged`devolución de llamada.
>
>Esto pasa varios parámetros:
>* A `state` parámetro de tipo `MediaPlayer.PlayerState` con el valor de `MediaPlayer.PlayerState.ERROR`.
>
>* A `notification` parámetro de tipo `MediaPlayerNotification` que contiene información de diagnóstico sobre el evento de error.

El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso multimedia:

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
