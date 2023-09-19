---
description: Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.
title: Cargar un recurso multimedia mediante MediaPlayerItemLoader
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Cargar un recurso multimedia mediante MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.

A través de `MediaPlayerItemLoader` , puede intercambiar un recurso multimedia por el recurso correspondiente `MediaPlayerItem` sin adjuntar una vista a `MediaPlayer` , lo que llevaría a la asignación de los recursos de hardware de descodificación de vídeo. El proceso de obtención de la `MediaPlayerItem` La instancia de es asíncrona.

1. Implementar detectores de eventos para estos `MediaPlayerItemLoader` eventos:

   * `MediaPlayerItemLoaderEvent.ERROR` evento

     TVSDK utiliza esto para informar a la aplicación de que se ha producido un error. TVSDK proporciona una propiedad de error que contiene información de diagnóstico.

1. Registre esta instancia en `MediaPlayerItemLoader`.
1. Llamada `DefaultMediaPlayerItemLoader.load`, pasando una instancia de `MediaResource` objeto.

   La dirección URL del `MediaResource` debe apuntar a la secuencia de la que desea obtener información. Por ejemplo:

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
