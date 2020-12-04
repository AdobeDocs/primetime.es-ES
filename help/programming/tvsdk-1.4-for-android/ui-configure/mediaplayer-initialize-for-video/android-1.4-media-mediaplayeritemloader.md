---
description: Otra forma de resolver un recurso de medios es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.
seo-description: Otra forma de resolver un recurso de medios es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.
seo-title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Cargar un recurso de medios mediante MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Otra forma de resolver un recurso de medios es con MediaPlayerItemLoader. Esto resulta útil cuando desea obtener información sobre un flujo de medios determinado sin crear una instancia de MediaPlayer.

A través de la clase `MediaPlayerItemLoader`, puede intercambiar un recurso de medios para la `MediaPlayerItem` correspondiente sin adjuntar una vista a una instancia `MediaPlayer`, lo que llevaría a la asignación de los recursos de hardware de descodificación de vídeo. El proceso para obtener la instancia `MediaPlayerItem` es asíncrono.

1. Implementar la interfaz de llamada de retorno `MediaPlayerItemLoader.LoaderListener`.

       Esta interfaz define dos métodos:
   
   * `LoaderListener.onError` función callback

      TVSDK lo utiliza para informar a la aplicación de que se ha producido un error. TVSDK proporciona un código de error como parámetros y una cadena de descripción que contiene información de diagnóstico.

   * `LoaderListener.onError` función callback

      TVSDK lo utiliza para informar a la aplicación de que la información solicitada está disponible en forma de una instancia `MediaPlayerItem` que se pasa como parámetro a la llamada de retorno.

1. Registre esta instancia en TVSDK pasándola como parámetro al constructor de `MediaPlayerItemLoader`.
1. Llamar a `MediaPlayerItemLoader.load`, pasando una instancia de un objeto `MediaResource`.

   La dirección URL del objeto `MediaResource` debe apuntar a la secuencia para la que desea obtener información. Por ejemplo:

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

