---
description: Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir. Esta es una forma de cargar un recurso de medios.
title: Carga de un recurso de medios en el reproductor de medios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Carga de un recurso de medios en el reproductor de medios {#load-a-media-resource-in-the-media-player}

Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir. Esta es una forma de cargar un recurso de medios.

1. Configure el reproductor de medios para que reproduzca el nuevo recurso.

   Reemplace el elemento que se puede reproducir actualmente llamando a `MediaPlayer.replaceCurrentResource()` y pasando una instancia `MediaResource` existente.

   Esto inicia el proceso de carga de recursos.

1. Registre el evento `MediaPlayerEvent.STATUS_CHANGED` con la instancia `MediaPlayer` . En la rellamada, compruebe al menos los siguientes valores de estado:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   Mediante estos eventos, el objeto `MediaPlayer` notifica a la aplicación cuando ha cargado correctamente el recurso de medios.
1. Cuando el estado del reproductor de contenidos cambia a `INITIALIZED`, puede llamar a `MediaPlayer.prepareToPlay()`.

   Este estado indica que el medio se ha cargado correctamente. El nuevo `MediaPlayerItem` está listo para la reproducción. Al llamar a `prepareToPlay()` se inicia el proceso de resolución y colocación de publicidad, si existe.

Si se produce un error, el reproductor de contenidos cambia al estado `ERROR`.

El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso de medios:

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
