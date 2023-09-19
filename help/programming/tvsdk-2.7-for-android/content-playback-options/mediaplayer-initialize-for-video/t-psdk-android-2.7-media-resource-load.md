---
description: Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir. Esta es una forma de cargar un recurso multimedia.
title: Carga de un recurso multimedia en el reproductor de contenidos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Carga de un recurso multimedia en el reproductor de contenidos {#load-a-media-resource-in-the-media-player}

Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir. Esta es una forma de cargar un recurso multimedia.

1. Configure el reproductor de contenidos para que reproduzca el nuevo recurso.

   Reemplazar el elemento que se puede reproducir actualmente llamando a `MediaPlayer.replaceCurrentResource()` y pasar un existente `MediaResource` ejemplo.

   Esto inicia el proceso de carga de recursos.

1. Registre el `MediaPlayerEvent.STATUS_CHANGED` con el evento `MediaPlayer` ejemplo. En la llamada de retorno, compruebe al menos los siguientes valores de estado:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   A través de estos eventos, la `MediaPlayer` notifica a la aplicación cuando ha cargado correctamente el recurso multimedia.
1. Cuando el estado del reproductor de contenidos cambie a `INITIALIZED`, puede llamar a `MediaPlayer.prepareToPlay()`.

   Este estado indica que el medio se ha cargado correctamente. El nuevo `MediaPlayerItem` está listo para la reproducción. Llamando `prepareToPlay()` inicia el proceso de resolución y colocación de la publicidad, si lo hay.

Si se produce un error, el reproductor multimedia cambia al `ERROR` estado.

El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso multimedia:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatus status) { 
        if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
            // The resource is successfully loaded and available. The  
            // MediaPlayer is ready to start the playback and can 
            // provide a reference to the current playable item 
            MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
            if (playerItem != null) { 
                // We can look at the properties of the loaded stream 
            } 
        } 
        else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            //Something bad happened - the resource cannot be loaded. 
            // The Metadata object in the event provides details. 
        } 
        else if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
    } 
} 
```
