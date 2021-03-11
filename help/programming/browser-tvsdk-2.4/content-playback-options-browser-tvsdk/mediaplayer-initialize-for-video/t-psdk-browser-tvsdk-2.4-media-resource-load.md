---
description: Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir.
title: Carga de un recurso de medios en MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Cargar un recurso de medios en MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Cargue un recurso creando una instancia de MediaResource directamente y cargando el contenido del vídeo que desea reproducir.

1. Establezca el elemento que se puede reproducir del objeto `MediaPlayer` con el nuevo recurso que se va a reproducir.

   Reemplace el elemento que actualmente se puede reproducir del objeto `MediaPlayer` existente llamando a `replaceCurrentResource` y pasando una instancia `MediaResource` existente.

1. Espere a que el TVSDK del explorador distribuya `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status` que sea igual a cualquiera de las siguientes opciones:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      A través de estos eventos, el objeto MediaPlayer notifica a la aplicación si el recurso multimedia se ha cargado correctamente.

1. Cuando el estado del reproductor de contenidos cambia a `MediaPlayerStatus.INITIALIZED`, puede llamar a `MediaPlayer.prepareToPlay`.

   El estado INITIALIZED indica que el medio se ha cargado correctamente. Al llamar a `prepareToPlay` se inicia el proceso de resolución y colocación de publicidad, si existe.
1. Cuando el SDK del explorador distribuye el evento `MediaPlayerStatus.PREPARED` , el flujo de medios se ha cargado correctamente (se ha creado un MediaPlayerItem) y está preparado para la reproducción.

Si se produce un error, el `MediaPlayer` cambia al `MediaPlayerStatus.ERROR`.

También notifica a su aplicación mediante el envío del evento `MediaPlayerStatus.ERROR` .

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


El siguiente código de ejemplo simplificado ilustra el proceso de carga de un recurso de medios:

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
