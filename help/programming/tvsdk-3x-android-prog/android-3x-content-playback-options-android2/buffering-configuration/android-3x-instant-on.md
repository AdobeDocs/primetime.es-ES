---
description: Activar la activación instantánea significa que uno o más canales están precargados. Cuando los usuarios seleccionan un canal o cambian de canal, el contenido se reproduce inmediatamente. El almacenamiento en búfer se completa para el momento en que el usuario empieza a ver.
title: Instant On
exl-id: 59293e07-160a-41a2-8ffe-7ca9323048f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Instant On {#instant-on}

Activar la activación instantánea significa que uno o más canales están precargados. Cuando los usuarios seleccionan un canal o cambian de canal, el contenido se reproduce inmediatamente. El almacenamiento en búfer se completa para el momento en que el usuario empieza a ver.

Sin Encendido instantáneo, TVSDK inicializa los medios que se van a reproducir, pero no comienza a almacenar en búfer el flujo hasta que la aplicación llama a `play`. El usuario no ve ningún contenido hasta que se completa el almacenamiento en búfer. Con Instant On, puede iniciar varias instancias del reproductor de contenidos (o del cargador de elementos del reproductor de contenidos) y TVSDK comienza a almacenar en búfer los flujos inmediatamente. Cuando un usuario cambia el canal y el flujo se ha almacenado en búfer correctamente, llamando a `play` en el nuevo canal, la reproducción se inicia inmediatamente.

Aunque no hay límites en la cantidad de `MediaPlayer` y `MediaPlayerItemLoader` Las instancias que TVSDK puede ejecutar, al ejecutar más instancias, consumen más recursos. El rendimiento de la aplicación puede verse afectado por el número de instancias que se están ejecutando. Para obtener más información acerca de `MediaPlayerItemLoader`, consulte [Carga de un recurso multimedia en el reproductor de contenidos](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK no admite un único `QoSProvider` para trabajar con ambos `itemLoader` y `MediaPlayer`. Si el cliente utiliza Instant On, la aplicación debe mantener dos instancias de QoS y administrar ambas para la información.

Para obtener más información acerca de `MediaPlayerItemLoader`, consulte [Cargar un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Agregar una instancia de proveedor de QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Crear y adjuntar un proveedor de QoS a un `mediaPlayerItemLoader` instancia

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Una vez que comience la reproducción, utilice el `_qosProvider` para obtener `timeToLoad` y `timeToPrepare` QoSdata. Las métricas de QoS restantes se pueden recuperar mediante la variable `QoSProvider` adjunto al `mediaPlayer`.

   Para obtener más información acerca de `MediaPlayerItemLoader`, consulte [Cargar un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurar el almacenamiento en búfer para Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK proporciona métodos y estados que permiten utilizar Instant On con un recurso multimedia.

>[!NOTE]
>
>Adobe recomienda utilizar `MediaPlayerItemLoader` para InstantOn. Para usar `MediaPlayerItemLoader`, en lugar de `MediaPlayer`, consulte [Cargar un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Confirme que el recurso se ha cargado y que el reproductor está preparado para reproducirlo.
1. Antes de llamar `play`, llame a `prepareBuffer` para cada `MediaPlayer` ejemplo.

   `prepareBuffer` activa Instant On y TVSDK inicia el almacenamiento en búfer inmediatamente y envía el `BUFFERING_COMPLETED` cuando el búfer está lleno.

   >[!TIP]
   >
   >De forma predeterminada, `prepareBuffer` y `prepareToPlay` configure el flujo de medios para que comience a reproducirse desde el principio. Para empezar en otra posición, pase la posición (en milisegundos) a `prepareToPlay`.

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

1. Cuando reciba la `BUFFERING_COMPLETE` , empiece a reproducir el elemento o muestre comentarios visuales para indicar que el contenido está completamente almacenado en búfer.

   >[!NOTE]
   >
   >Si llama a `play`, la reproducción debe comenzar inmediatamente.
