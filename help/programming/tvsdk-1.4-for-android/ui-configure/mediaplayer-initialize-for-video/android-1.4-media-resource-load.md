---
description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.
seo-description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.
seo-title: Cargar un recurso de medios en MediaPlayer
title: Cargar un recurso de medios en MediaPlayer
uuid: 6ee8032f-0728-423f-a1d2-5030aa7db14f
translation-type: tm+mt
source-git-commit: 4ef05be045334a2e723da4c7c6a7ee22fb0f776c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Cargar un recurso de medios en MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.

1. Configure el elemento que se puede reproducir de MediaPlayer con el nuevo recurso que se va a reproducir.

   Reemplace el elemento que se puede reproducir en este momento en MediaPlayer llamando a `MediaPlayer.replaceCurrentItem` y pasando una instancia `MediaResource` existente.

1. Registre una implementación de la interfaz `MediaPlayer.PlaybackEventListener` con la instancia `MediaPlayer`.

   * `onPrepared`
   * `onStateChanged`y compruebe si hay INICIALIZADO y ERROR.

1. Cuando el estado del reproductor de medios cambia a INITIALIZADO, puede llamar a `MediaPlayer.prepareToPlay`

   El estado INITIALIZED indica que el medio se ha cargado correctamente. La llamada `prepareToPlay` inicio la resolución de publicidad y el proceso de colocación, si existe.

1. Cuando TVSDK llama a la rellamada `onPrepared`, el flujo de medios se ha cargado correctamente y está preparado para la reproducción.

   Cuando se carga el flujo de medios, se crea un `MediaPlayerItem`.

>Si se produce un error, `MediaPlayer` cambia al estado ERROR. También notifica a la aplicación llamando a la llamada de retorno `PlaybackEventListener.onStateChanged`.
>
>Esto pasa varios parámetros:
>* Un parámetro `state` de tipo `MediaPlayer.PlayerState` con el valor `MediaPlayer.PlayerState.ERROR`.
   >
   >
* Un parámetro `notification` de tipo `MediaPlayerNotification` que contiene información de diagnóstico sobre el evento de error.


El siguiente código de muestra simplificado ilustra el proceso de carga de un recurso de medios:

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
