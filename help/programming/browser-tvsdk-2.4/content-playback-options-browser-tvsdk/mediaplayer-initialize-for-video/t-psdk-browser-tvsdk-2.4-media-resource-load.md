---
description: Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir.
title: Cargar un recurso multimedia en MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Cargar un recurso multimedia en MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando directamente una instancia de MediaResource y cargando el contenido de vídeo que desea reproducir.

1. Configure su `MediaPlayer` elemento reproducible del objeto con el nuevo recurso que se va a reproducir.

   Reemplace el existente `MediaPlayer` elemento reproducible actualmente del objeto llamando a `replaceCurrentResource` y pasar un existente `MediaResource` ejemplo.

1. Espere a que el TVSDK del explorador se distribuya `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status` que sea igual a cualquiera de las siguientes opciones:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

     Mediante estos eventos, el objeto MediaPlayer notifica a la aplicación si el recurso multimedia se ha cargado correctamente.

1. Cuando el estado del reproductor de contenidos cambie a `MediaPlayerStatus.INITIALIZED`, puede llamar a `MediaPlayer.prepareToPlay`.

   El estado INITIALIZED indica que el medio se ha cargado correctamente. Llamando `prepareToPlay` inicia el proceso de resolución y colocación de la publicidad, si lo hay.
1. Cuando el TVSDK del explorador envía el `MediaPlayerStatus.PREPARED` evento el flujo de medios se ha cargado correctamente (se crea un MediaPlayerItem) y está preparado para la reproducción.

Si se produce un error, la variable `MediaPlayer` cambia al `MediaPlayerStatus.ERROR`.

También notifica a la aplicación enviando el `MediaPlayerStatus.ERROR` evento.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso multimedia:

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
