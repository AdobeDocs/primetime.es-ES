---
description: Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios concreto sin crear una instancia de MediaPlayer.
title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Carga de un recurso multimedia mediante MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios concreto sin crear una instancia de MediaPlayer.

A través de la clase `MediaPlayerItemLoader`, puede intercambiar un recurso de medios para el `MediaPlayerItem` correspondiente sin adjuntar una vista a una instancia `MediaPlayer`, lo que llevaría a la asignación de los recursos de hardware de descodificación de vídeo. El proceso para obtener la instancia `MediaPlayerItem` es asíncrono.

1. Implemente detectores de eventos para estos eventos `MediaPlayerItemLoader`:

   * `MediaPlayerItemLoaderEvent.ERROR` evento

      TVSDK lo utiliza para informar a la aplicación de que se ha producido un error. TVSDK proporciona una propiedad de error que contiene información de diagnóstico.

1. Registre esta instancia en `MediaPlayerItemLoader`.
1. Llame a `DefaultMediaPlayerItemLoader.load`, pasando una instancia de un objeto `MediaResource`.

   La dirección URL del objeto `MediaResource` debe señalar a la secuencia para la que desea obtener información. Por ejemplo:

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

