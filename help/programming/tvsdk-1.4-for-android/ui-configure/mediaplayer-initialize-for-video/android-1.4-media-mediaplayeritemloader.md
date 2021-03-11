---
description: Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios concreto sin crear una instancia de MediaPlayer.
title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Carga de un recurso multimedia mediante MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Otra forma de resolver un recurso multimedia es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios concreto sin crear una instancia de MediaPlayer.

A través de la clase `MediaPlayerItemLoader`, puede intercambiar un recurso de medios para el `MediaPlayerItem` correspondiente sin adjuntar una vista a una instancia `MediaPlayer`, lo que llevaría a la asignación de los recursos de hardware de descodificación de vídeo. El proceso para obtener la instancia `MediaPlayerItem` es asíncrono.

1. Implemente la interfaz de llamada de retorno `MediaPlayerItemLoader.LoaderListener` .

       Esta interfaz define dos métodos:
   
   * `LoaderListener.onError` función callback

      TVSDK lo utiliza para informar a la aplicación de que se ha producido un error. TVSDK proporciona un código de error como parámetros y una cadena de descripción que contiene información de diagnóstico.

   * `LoaderListener.onError` función callback

      TVSDK lo utiliza para informar a su aplicación de que la información solicitada está disponible en forma de instancia `MediaPlayerItem` que se pasa como parámetro a la rellamada.

1. Registre esta instancia en TVSDK pasándola como parámetro al constructor del `MediaPlayerItemLoader`.
1. Llame a `MediaPlayerItemLoader.load`, pasando una instancia de un objeto `MediaResource`.

   La dirección URL del objeto `MediaResource` debe señalar a la secuencia para la que desea obtener información. Por ejemplo:

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

