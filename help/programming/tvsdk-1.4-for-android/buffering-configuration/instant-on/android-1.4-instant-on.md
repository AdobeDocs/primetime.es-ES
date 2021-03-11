---
description: El término instantáneo en hace referencia a la precarga de uno o más canales, de modo que un usuario que selecciona un canal o cambia de canal ve que el contenido se reproduce inmediatamente. El almacenamiento en búfer ya se ha realizado cuando el usuario empieza a ver.
title: Instantáneo activado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Instantáneo en {#instant-on}

El término instantáneo en hace referencia a la precarga de uno o más canales, de modo que un usuario que selecciona un canal o cambia de canal ve que el contenido se reproduce inmediatamente. El almacenamiento en búfer ya se ha realizado cuando el usuario empieza a ver.

Sin conexión instantánea, TVSDK inicializa el contenido que se va a reproducir, pero no comienza a almacenar en búfer el flujo hasta que la aplicación llama a `play`. El usuario no ve ningún contenido hasta que se completa el almacenamiento en búfer. Con la activación instantánea, puede iniciar varias instancias del reproductor de contenidos (o del cargador de elementos del reproductor de contenidos) y TVSDK empezará a almacenar en búfer las emisiones inmediatamente.

Cuando un usuario cambia el canal y el flujo se almacena en búfer correctamente, la llamada `play` en el nuevo canal inicia la reproducción inmediatamente.

Aunque no hay límites al número de instancias `MediaPlayer` que TVSDK puede ejecutar, la ejecución de más instancias consume más recursos. El rendimiento de la aplicación puede verse afectado por el número de instancias que se ejecutan. Para obtener más información sobre estas instancias, consulte [Carga de un recurso de medios mediante MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurar el almacenamiento en búfer para la reproducción instantánea {#configure-buffering-for-instant-on-playback}

Con la activación instantánea, los usuarios pueden cambiar de canal y la reproducción comienza inmediatamente sin esperar tiempo. Cuando activa instantáneamente, TVSDK almacena en búfer uno o varios canales antes de que comience la reproducción.

1. Confirme que el recurso se ha cargado y está listo para reproducirse. Para ello, compruebe que el estado esté PREPARADO.
1. Antes de llamar a `play`, llame a `prepareBuffer` para cada instancia `MediaPlayer`.

   Esto activa instantáneamente, lo que significa que TVSDK comienza a almacenar en búfer sin reproducir realmente el recurso de medios. TVSDK distribuye el evento `BUFFERING_COMPLETED` cuando el búfer está lleno.

   >[!NOTE]
   >
   >De forma predeterminada, `prepareBuffer` y `prepareToPlay` configuran el flujo de medios para que se inicie la reproducción desde el principio. Para comenzar en otra posición, pase la posición (en milisegundos) a `prepareToPlay`.

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. Cuando reciba el evento `BUFFERING_COMPLETE`, empiece a reproducir el elemento o muestre comentarios visuales para indicar que el contenido está completamente almacenado en búfer.

   Si llama a `play`, la reproducción debe comenzar inmediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
