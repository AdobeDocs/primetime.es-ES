---
description: El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento previo en búfer para que la reproducción pueda comenzar sin demora.
seo-description: El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento previo en búfer para que la reproducción pueda comenzar sin demora.
seo-title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
title: Carga de un recurso multimedia mediante MediaPlayerItemLoader
uuid: 504063af-1dd4-4268-88e7-ad5a247fdff7
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Cargar un recurso de medios mediante MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

El uso de MediaPlayerItemLoader ayuda a obtener información sobre un flujo de medios sin crear una instancia de MediaPlayer. Esto resulta especialmente útil en los flujos de almacenamiento previo en búfer para que la reproducción pueda comenzar sin demora.

La clase `MediaPlayerItemLoader` le ayuda a intercambiar un recurso de medios para el `MediaPlayerItem` actual sin adjuntar una vista a una instancia `MediaPlayer`, que asignaría recursos de hardware de descodificación de vídeo. Se necesitan pasos adicionales para el contenido protegido con DRM, pero este manual no los describe.

>[!IMPORTANT]
>
>TVSDK no admite un solo `QoSProvider` para trabajar con `itemLoader` y `MediaPlayer`. Si la aplicación utiliza Instant On, la aplicación debe mantener dos instancias `QoS` y administrar ambas instancias para la información. Consulte [Instant-on](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) para obtener más información.

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

1. Implemente la clase `ItemLoaderListener` para recibir notificaciones de la instancia `MediaPlayerItemLoader`.

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

   * Asegúrese de que todo lo que pueda afectar al almacenamiento en búfer, por ejemplo, seleccionar WebVTT o pistas de audio, esté completo y llame a `prepareBuffer()` para aprovechar el funcionamiento instantáneo.
   * Adjunte el elemento a la instancia `MediaPlayer` mediante `replaceCurrentItem()`.

   Si llama a `prepareBuffer()`, recibirá el evento BUFFER_PREPARED en su controlador `onBufferPrepared` cuando finalice la preparación.
1. Llame a `load` en la instancia `MediaPlayerItemLoader` y pase el recurso que se va a cargar, y opcionalmente la ID de contenido y una instancia `MediaPlayerItemConfig`.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para almacenar en búfer desde un punto que no sea el principio del flujo, llame a `prepareBuffer()` con la posición (en milisegundos) en la que se almacenará en inicio el almacenamiento en búfer.
1. Utilice los métodos `replaceCurrentItem()` y `play()` de `MediaPlayer` para reproducir en inicio a partir de ese punto.
1. Espere el estado de inactividad y llame a `replaceCurrentItem`.
1. Reproduzca el elemento.

   * Si el elemento se carga pero no se almacena en el búfer:

      1. Esperar el estado inicializado.
      1. Llame a `prepareToPlay()`.
      1. Espere el estado PREPARADO.
      1. Llame a `play()`.
   * Si el elemento está en el búfer:

      1. Espere el evento preparado para el búfer.
      1. Llame a `play()`.