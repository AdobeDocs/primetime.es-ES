---
description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.
seo-description: Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.
seo-title: Carga de un recurso de medios en el reproductor de medios
title: Carga de un recurso de medios en el reproductor de medios
uuid: 1a27b83b-afa6-48c7-a701-e11b2d280810
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Carga de un recurso de medios en el reproductor de medios {#load-a-media-resource-in-the-media-player}

Cargue un recurso creando una instancia directa de MediaResource y cargando el contenido del vídeo que se va a reproducir. Esta es una forma de cargar un recurso de medios.

1. Configure el reproductor de medios para que reproduzca el nuevo recurso.

   Reemplace el elemento que se puede reproducir actualmente llamando `MediaPlayer.replaceCurrentResource()` y pasando una `MediaResource` instancia existente.

   Esto inicia el proceso de carga de recursos.

1. Registre el `MediaPlayerEvent.STATUS_CHANGED` evento con la `MediaPlayer` instancia. En la llamada de retorno, compruebe al menos los siguientes valores de estado:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`
   A través de estos eventos, el `MediaPlayer` objeto notifica a la aplicación cuando ha cargado correctamente el recurso multimedia.
1. Cuando el estado del reproductor de medios cambia a `INITIALIZED`, puede llamar a `MediaPlayer.prepareToPlay()`.

   Este estado indica que el medio se ha cargado correctamente. El nuevo `MediaPlayerItem` está listo para la reproducción. La llamada `prepareToPlay()` inicia el proceso de resolución y colocación de la publicidad, si existe.

Si se produce un error, el reproductor de medios cambia al `ERROR` estado.

El siguiente código de muestra simplificado ilustra el proceso de carga de un recurso de medios:

```java>
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
