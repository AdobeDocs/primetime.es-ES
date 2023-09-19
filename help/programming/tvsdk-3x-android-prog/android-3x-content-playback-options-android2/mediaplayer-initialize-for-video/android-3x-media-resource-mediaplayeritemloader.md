---
description: El uso de MediaPlayerItemLoader le ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en flujos de almacenamiento en búfer previo para que la reproducción pueda comenzar sin demora.
title: Cargar un recurso multimedia mediante MediaPlayerItemLoader
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Cargar un recurso multimedia mediante MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

El uso de MediaPlayerItemLoader le ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en flujos de almacenamiento en búfer previo para que la reproducción pueda comenzar sin demora.

El `MediaPlayerItemLoader` La clase le ayuda a intercambiar un recurso multimedia por el `MediaPlayerItem` sin adjuntar una vista a `MediaPlayer` , que asignaría recursos de hardware de descodificación de vídeo. Se necesitan pasos adicionales para el contenido protegido por DRM, pero este manual no los describe.

>[!IMPORTANT]
>
>TVSDK no admite un único `QoSProvider` para trabajar con ambos `itemLoader` y `MediaPlayer`. Si la aplicación utiliza Instant On, debe mantener dos `QoS` y administrar ambas instancias para la información. Consulte [Instant-on](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) para obtener más información.

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
   >Cree una instancia independiente de `MediaPlayerItemLoader` para cada recurso. No use uno `MediaPlayerItemLoader` para cargar varios recursos.

1. Implementación de `ItemLoaderListener` clase para recibir notificaciones de `MediaPlayerItemLoader` ejemplo.

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

   En el `onLoadComplete()` callback, realice una de las siguientes acciones:

   * Asegúrese de que todo lo que pueda afectar al almacenamiento en búfer, por ejemplo, la selección de pistas de audio o WebVTT, esté completo e invoque `prepareBuffer()` para aprovechar las ventajas de la activación instantánea.
   * Adjunte el elemento al `MediaPlayer` mediante el uso de `replaceCurrentItem()`.

   Si llama a `prepareBuffer()`, recibirá el evento BUFFER_PREPARED en su `onBufferPrepared` cuando finalice la preparación.
1. Llamada `load` en el `MediaPlayerItemLoader` y pasan el recurso que se va a cargar, y opcionalmente el ID de contenido y un `MediaPlayerItemConfig` ejemplo.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para almacenar en búfer desde un punto que no sea el principio de la secuencia, llame a `prepareBuffer()` con la posición (en milisegundos) en la que se va a iniciar el almacenamiento en búfer.
1. Utilice el `replaceCurrentItem()` y `play()` métodos de `MediaPlayer` para empezar a jugar desde ese punto.
1. Esperar al estado inactivo e invocar `replaceCurrentItem`.
1. Reproduzca el elemento.

   * Si el elemento se carga pero no se almacena en búfer:

      1. Esperar al estado inicializado.
      1. Llamada `prepareToPlay()`.
      1. Espere al estado PREPARADO.
      1. Llamada `play()`.

   * Si el elemento se almacena en búfer:

      1. Espere al evento preparado para el búfer.
      1. Llamada `play()`.
