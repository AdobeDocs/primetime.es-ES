---
description: El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento previo en búfer para que la reproducción pueda comenzar sin demora.
seo-description: El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento previo en búfer para que la reproducción pueda comenzar sin demora.
seo-title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
uuid: 504063af-1dd4-4268-88e7-ad5a247fdff7
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# Carga de un recurso multimedia mediante MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento previo en búfer para que la reproducción pueda comenzar sin demora.

La `MediaPlayerItemLoader` clase le ayuda a intercambiar un recurso de medios para el actual `MediaPlayerItem` sin adjuntar una vista a una `MediaPlayer` instancia, lo que asignaría recursos de hardware de descodificación de vídeo. Se necesitan pasos adicionales para el contenido protegido con DRM, pero este manual no los describe.

>[!IMPORTANT]
>
>TVSDK no admite un solo `QoSProvider` para trabajar tanto con `itemLoader` como con `MediaPlayer`. Si la aplicación utiliza Instant On, la aplicación debe mantener dos `QoS` instancias y administrar ambas instancias para la información. Consulte [Activado](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) para obtener más información.

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
   >Cree una instancia de `MediaPlayerItemLoader` para cada recurso. No utilice una `MediaPlayerItemLoader` instancia para cargar varios recursos.

1. Implemente la `ItemLoaderListener` clase para recibir notificaciones de la `MediaPlayerItemLoader` instancia.

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

   En la `onLoadComplete()` llamada de retorno, realice una de las siguientes acciones:

   * Asegúrese de que todo lo que pueda afectar al almacenamiento en búfer, por ejemplo, la selección de WebVTT o pistas de audio, esté completo y llame `prepareBuffer()` para aprovechar la activación instantánea.
   * Adjunte el elemento a la `MediaPlayer` instancia mediante `replaceCurrentItem()`.
   Si llama `prepareBuffer()`, recibirá el evento BUFFER_PREPARED en el `onBufferPrepared` controlador cuando finalice la preparación.
1. Llama `load` a la `MediaPlayerItemLoader` instancia y pasa el recurso que se va a cargar, y opcionalmente el ID de contenido y una `MediaPlayerItemConfig` instancia.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para almacenar en búfer desde un punto que no sea el principio del flujo, llame `prepareBuffer()` con la posición (en milisegundos) en la que se iniciará el almacenamiento en búfer.
1. Utilice los métodos `replaceCurrentItem()` y `play()` de `MediaPlayer` para empezar a reproducirse desde ese punto.
1. Espere el estado de inactividad y llame `replaceCurrentItem`.
1. Reproduzca el elemento.

   * Si el elemento se carga pero no se almacena en el búfer:

      1. Esperar el estado inicializado.
      1. Llama `prepareToPlay()`.
      1. Espere el estado PREPARADO.
      1. Llama `play()`.
   * Si el elemento está en el búfer:

      1. Espere el evento preparado por el búfer.
      1. Llama `play()`.