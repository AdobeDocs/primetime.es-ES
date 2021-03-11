---
description: El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento en búfer previo para que la reproducción pueda comenzar sin demora.
title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Carga de un recurso multimedia mediante MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento en búfer previo para que la reproducción pueda comenzar sin demora.

La clase `MediaPlayerItemLoader` le ayuda a intercambiar un recurso de medios para el `MediaPlayerItem` actual sin adjuntar una vista a una instancia `MediaPlayer`, que asignaría recursos de hardware de descodificación de vídeo. Se necesitan pasos adicionales para el contenido protegido con DRM, pero este manual no los describe.

>[!IMPORTANT]
>
>TVSDK no admite un solo `QoSProvider` para que funcione con `itemLoader` y `MediaPlayer`. Si la aplicación utiliza Instant On, la aplicación debe mantener dos instancias `QoS` y administrar ambas instancias para obtener la información. Consulte [instantáneo](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) para obtener más información.

1. Cree una instancia de `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
   
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
   
           public void onBufferingBegin() { 
               //Do something 
           } 
   
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   ```

   >[!TIP]
   >
   >Cree una instancia separada de `MediaPlayerItemLoader` para cada recurso. No utilice una instancia `MediaPlayerItemLoader` para cargar varios recursos.

1. Implemente la clase `ItemLoaderListener` para recibir notificaciones de la instancia `MediaPlayerItemLoader` .

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   En la llamada de retorno `onLoadComplete()`, realice una de las siguientes acciones:

   * Asegúrese de que todo lo que pueda afectar al almacenamiento en búfer, por ejemplo, seleccionar WebVTT o pistas de audio, esté completo e invoque `prepareBuffer()` para aprovechar el uso instantáneo.
   * Adjunte el elemento a la instancia `MediaPlayer` utilizando `replaceCurrentItem()`.

   Si llama a `prepareBuffer()`, recibirá el evento BUFFER_PREPARED en su controlador `onBufferPrepared` cuando finalice la preparación.

1. Llame a `load` en la instancia `MediaPlayerItemLoader` y pase el recurso que se va a cargar, y opcionalmente el ID de contenido y una instancia `MediaPlayerItemConfig`.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para almacenar en búfer desde un punto distinto al principio del flujo, llame a `prepareBuffer()` con la posición (en milisegundos) en la que comenzará el almacenamiento en búfer.
1. Utilice los métodos `replaceCurrentItem()` y `play()` de `MediaPlayer` para comenzar a reproducirse a partir de ese momento.
1. Espere a que aparezca el estado inactivo y llame a `replaceCurrentItem`.
1. Reproduzca el elemento.

   * Si el elemento está cargado pero no almacenado en búfer:

      1. Espere a que se inicialice el estado.
      1. Llame a `prepareToPlay()`.
      1. Espere el estado PREPARADO.
      1. Llame a `play()`.
   * Si el elemento está en búfer:

      1. Espere al evento de preparación del búfer.
      1. Llame a `play()`.