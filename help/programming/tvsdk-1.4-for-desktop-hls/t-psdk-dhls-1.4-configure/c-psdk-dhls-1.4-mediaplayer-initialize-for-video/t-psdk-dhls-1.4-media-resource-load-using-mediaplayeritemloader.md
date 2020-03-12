---
description: Otra forma de resolver un recurso de medios es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.
seo-description: Otra forma de resolver un recurso de medios es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.
seo-title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
uuid: a7ec8f58-7357-4757-a402-e879dd6caec8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Carga de un recurso multimedia mediante MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Otra forma de resolver un recurso de medios es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.

A través de la `MediaPlayerItemLoader` clase, puede intercambiar un recurso de medios para el correspondiente `MediaPlayerItem` sin adjuntar una vista a una `MediaPlayer` instancia, lo que llevaría a la asignación de los recursos de hardware de descodificación de vídeo. El proceso de obtención de la `MediaPlayerItem` instancia es asíncrono.

1. Implementar detectores de eventos para estos `MediaPlayerItemLoader` eventos:

   * `MediaPlayerItemLoaderEvent.ERROR` event

      TVSDK lo utiliza para informar a la aplicación de que se ha producido un error. TVSDK proporciona una propiedad de error que contiene información de diagnóstico.

1. Registre esta instancia en el `MediaPlayerItemLoader`.
1. Llamada `DefaultMediaPlayerItemLoader.load`, pasando una instancia de un `MediaResource` objeto.

   La dirección URL del `MediaResource` objeto debe apuntar al flujo del que desea obtener información. Por ejemplo:

   ```
   private function onLoadError(event:MediaPlayerItemLoaderEvent):void { 
       // something went wrong - look at the error code and description 
       // contained within the event.error 
   } 
   private function onLoadCompleted(event:MediaPlayerItemLoaderEvent):void { 
       // information is available - look at the data in the "event.item" object 
   } 
   // instantiate the MediaPlayerItemLoader object and register event listeners 
   var itemLoader:MediaPlayerItemLoader = new DefaultMediaPlayerItemLoader(); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.ERROR, onLoadError); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.COMPLETED, onLoadCompleted); 
   // create the MediaResource instance and set the URL to point to the actual media stream 
   var mediaResource:MediaResource = 
     MediaResource.createFromURL("https://example.com/media/test_media.m3u8", null); 
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

