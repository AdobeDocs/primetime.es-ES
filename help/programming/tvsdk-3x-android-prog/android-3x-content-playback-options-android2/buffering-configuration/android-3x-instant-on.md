---
description: Habilitar instantáneamente significa que uno o más canales están precargados. Cuando los usuarios seleccionan un canal o cambian de canal, el contenido se reproduce inmediatamente. El almacenamiento en búfer se completa cuando el usuario comienza a ver.
seo-description: Habilitar instantáneamente significa que uno o más canales están precargados. Cuando los usuarios seleccionan un canal o cambian de canal, el contenido se reproduce inmediatamente. El almacenamiento en búfer se completa cuando el usuario comienza a ver.
seo-title: Instantáneo activado
title: Instantáneo activado
uuid: 5b1ceace-cae7-44c7-b4b9-d45078d58cc3
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Instantáneo activado {#instant-on}

Habilitar instantáneamente significa que uno o más canales están precargados. Cuando los usuarios seleccionan un canal o cambian de canal, el contenido se reproduce inmediatamente. El almacenamiento en búfer se completa cuando el usuario comienza a ver.

Sin activación instantánea, TVSDK inicializa el medio que se va a reproducir pero no comienza a almacenar en búfer el flujo hasta que la aplicación llama a `play`. El usuario no ve ningún contenido hasta que se completa el almacenamiento en búfer. Con Instant On, puede iniciar varias instancias de reproductor de medios (o cargador de elementos de reproductor de medios) y TVSDK empezará a almacenar los flujos inmediatamente. Cuando un usuario cambia el canal y el flujo se almacena en el búfer correctamente, al llamar `play` al nuevo canal se inicia la reproducción inmediatamente.

Aunque TVSDK no tiene límites en cuanto al número de instancias `MediaPlayer` y `MediaPlayerItemLoader` instancias que se pueden ejecutar, la ejecución de más instancias consume más recursos. El rendimiento de la aplicación puede verse afectado por el número de instancias que se están ejecutando. Para obtener más información sobre `MediaPlayerItemLoader`, consulte [Carga de un recurso de medios en el reproductor](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)de medios.

>[!IMPORTANT]
>
>TVSDK no admite un solo `QoSProvider` para trabajar tanto con `itemLoader` como con `MediaPlayer`. Si el cliente utiliza Instant On, la aplicación debe mantener dos instancias de QoS y administrar ambas instancias para la información.

Para obtener más información sobre `MediaPlayerItemLoader`, consulte [Carga de un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Agregar una instancia de proveedor de QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Crear y adjuntar un proveedor de QoS a una `mediaPlayerItemLoader` instancia

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Una vez que se inicie la reproducción, utilice el `_qosProvider` para obtener `timeToLoad` y `timeToPrepare` QoSdata. El resto de las métricas de QoS se pueden recuperar mediante el `QoSProvider` vínculo adjunto al `mediaPlayer`.

   Para obtener más información sobre `MediaPlayerItemLoader`, consulte [Carga de un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurar almacenamiento en búfer para activación instantánea {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK proporciona métodos y estados que le permiten usar Instant On con un recurso multimedia.

>[!NOTE]
>
>Adobe recomienda usar `MediaPlayerItemLoader` para InstantOn. Para usar `MediaPlayerItemLoader`, en lugar de `MediaPlayer`, consulte [Carga de un recurso de medios mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Confirme que el recurso se ha cargado y que el reproductor está preparado para reproducirlo.
1. Antes de llamar `play`, llame `prepareBuffer` para cada `MediaPlayer` instancia.

   `prepareBuffer` activa Instant On y TVSDK comienza a almacenar en búfer inmediatamente y distribuye el `BUFFERING_COMPLETED` evento cuando el búfer está lleno.

   >[!TIP]
   >
   >De forma predeterminada, `prepareBuffer` y `prepareToPlay` configure el flujo de medios para empezar a reproducirse desde el principio. Para comenzar en otra posición, pase la posición (en milisegundos) a `prepareToPlay`.

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. Cuando reciba el `BUFFERING_COMPLETE` evento, comience a reproducir el elemento o muestre información visual para indicar que el contenido se almacena completamente en el búfer.

   >[!NOTE]
   >
   >Si llama `play`, la reproducción debe comenzar inmediatamente.