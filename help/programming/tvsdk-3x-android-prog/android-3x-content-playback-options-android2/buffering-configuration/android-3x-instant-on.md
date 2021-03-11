---
description: Habilitar instantáneamente significa que uno o más canales están precargados. Cuando los usuarios seleccionan un canal o cambian de canal, el contenido se reproduce inmediatamente. El almacenamiento en búfer se completa cuando el usuario empieza a ver.
title: Instantáneo activado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Instantáneo en {#instant-on}

Habilitar instantáneamente significa que uno o más canales están precargados. Cuando los usuarios seleccionan un canal o cambian de canal, el contenido se reproduce inmediatamente. El almacenamiento en búfer se completa cuando el usuario empieza a ver.

Sin Instant On, TVSDK inicializa el contenido que se va a reproducir, pero no comienza a almacenar en búfer el flujo hasta que la aplicación llama a `play`. El usuario no ve ningún contenido hasta que se completa el almacenamiento en búfer. Con Instant On, puede iniciar varias instancias del reproductor de contenidos (o del cargador de elementos del reproductor de contenidos) y TVSDK empezará a almacenar en búfer las emisiones inmediatamente. Cuando un usuario cambia el canal y el flujo se almacena en búfer correctamente, la llamada `play` en el nuevo canal inicia la reproducción inmediatamente.

Aunque no hay límites en el número de instancias `MediaPlayer` y `MediaPlayerItemLoader` que TVSDK puede ejecutar, la ejecución de más instancias consume más recursos. El rendimiento de la aplicación puede verse afectado por el número de instancias que se están ejecutando. Para obtener más información sobre `MediaPlayerItemLoader`, consulte [Cargar un recurso de medios en el reproductor de medios](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK no admite un solo `QoSProvider` para que funcione con `itemLoader` y `MediaPlayer`. Si el cliente utiliza Instant On, la aplicación debe mantener dos instancias de QoS y administrar ambas instancias para la información.

Para obtener más información sobre `MediaPlayerItemLoader`, consulte [Carga de un recurso de medios mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Agregar una instancia de proveedor de QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Crear y adjuntar un proveedor de QoS a una instancia `mediaPlayerItemLoader`

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Una vez que se inicie la reproducción, utilice `_qosProvider` para obtener `timeToLoad` y `timeToPrepare` QoSdata. Las métricas de QoS restantes se pueden recuperar utilizando el `QoSProvider` adjunto al `mediaPlayer`.

   Para obtener más información sobre `MediaPlayerItemLoader`, consulte [Carga de un recurso de medios mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurar el almacenamiento en búfer para Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK proporciona métodos y estados para permitirle utilizar Instant On con un recurso de medios.

>[!NOTE]
>
>Adobe recomienda usar `MediaPlayerItemLoader` para InstantOn. Para utilizar `MediaPlayerItemLoader`, en lugar de `MediaPlayer`, consulte [Carga de un recurso de medios mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Confirme que el recurso se ha cargado y que el reproductor está preparado para reproducir el recurso.
1. Antes de llamar a `play`, llame a `prepareBuffer` para cada instancia `MediaPlayer`.

   `prepareBuffer` activa Instant On y TVSDK comienza a almacenar en búfer inmediatamente y envía el  `BUFFERING_COMPLETED` evento cuando el búfer está lleno.

   >[!TIP]
   >
   >De forma predeterminada, `prepareBuffer` y `prepareToPlay` configuran el flujo de medios para que se inicie la reproducción desde el principio. Para comenzar en otra posición, pase la posición (en milisegundos) a `prepareToPlay`.

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

1. Cuando reciba el evento `BUFFERING_COMPLETE`, empiece a reproducir el elemento o muestre comentarios visuales para indicar que el contenido está completamente almacenado en búfer.

   >[!NOTE]
   >
   >Si llama a `play`, la reproducción debe comenzar inmediatamente.