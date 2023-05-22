---
description: Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.
title: Cargar un recurso multimedia mediante MediaPlayerItemLoader
exl-id: 9d129497-8a71-433a-a542-f49be519893b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Cargar un recurso multimedia mediante MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.

A través de `MediaPlayerItemLoader` , puede intercambiar un recurso multimedia por el recurso correspondiente `MediaPlayerItem` sin adjuntar una vista a `MediaPlayer` , lo que llevaría a la asignación de los recursos de hardware de descodificación de vídeo. El proceso de obtención de la `MediaPlayerItem` La instancia de es asíncrona.

1. Implementación de `MediaPlayerItemLoader.LoaderListener` interfaz de devolución de llamada.

       Esta interfaz define dos métodos:
   
   * `LoaderListener.onError` función callback

      TVSDK utiliza esto para informar a la aplicación de que se ha producido un error. TVSDK proporciona un código de error como parámetros y una cadena de descripción que contiene información de diagnóstico.

   * `LoaderListener.onError` función callback

      TVSDK utiliza esto para informar a su aplicación de que la información solicitada está disponible en forma de `MediaPlayerItem` instancia de que se pasa como parámetro a la llamada de retorno.

1. Registre esta instancia en TVSDK pasándola como un parámetro al constructor del `MediaPlayerItemLoader`.
1. Llamada `MediaPlayerItemLoader.load`, pasando una instancia de `MediaResource` objeto.

   La dirección URL del `MediaResource` debe apuntar a la secuencia de la que desea obtener información. Por ejemplo:

   ```java
   // instantiate the listener interface 
   MediaPlayerItemLoader.LoaderListener _itemLoaderListener = 
     new MediaPlayerItemLoader.LoaderListener() { 
       @Override 
       public void onError(MediaErrorCode mediaErrorCode, String description) { 
           // something went wrong - look at the error code and description 
       } 
       @Override 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
           // information is available - look at the data in the "playerItem" object 
       } 
   } 
   
   // instantiate the MediaPlayerItemLoader object (pass the listener as parameter) 
   MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(_itemLoaderListener); 
   
   // create the MediaResource instance and set the URL to point to the actual media stream 
   MediaResource mediaResource =  
     MediaResource.createFromUrl("https://test.com/test_media.m3u8", null); 
   
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```
