---
description: El término instantáneo hace referencia a la precarga de uno o más canales para que un usuario que selecciona uno o cambia de canal vea que el contenido se reproduce inmediatamente. El almacenamiento en búfer ya está hecho para cuando el usuario empieza a ver.
title: Instantáneo en
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Instantáneo en {#instant-on}

El término instantáneo hace referencia a la precarga de uno o más canales para que un usuario que selecciona uno o cambia de canal vea que el contenido se reproduce inmediatamente. El almacenamiento en búfer ya está hecho para cuando el usuario empieza a ver.

Sin la activación instantánea, TVSDK inicializa el medio que se va a reproducir, pero no comienza a almacenar en búfer el flujo hasta que la aplicación llama a `play`. El usuario no ve ningún contenido hasta que se completa el almacenamiento en búfer. Con la función instantánea activada, puede iniciar varias instancias del reproductor de contenidos (o del cargador de elementos del reproductor de contenidos) y TVSDK comienza a almacenar en búfer los flujos inmediatamente.

Cuando un usuario cambia el canal y el flujo se ha almacenado en búfer correctamente, llamando a `play` en el nuevo canal, la reproducción se inicia inmediatamente.

Aunque no hay límites en la cantidad de `MediaPlayer` Las instancias que TVSDK puede ejecutar, al ejecutar más instancias, consumen más recursos. El rendimiento de la aplicación puede verse afectado por el número de instancias que se ejecutan. Para obtener más información sobre estas instancias, consulte [Cargar un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configuración del almacenamiento en búfer para la reproducción instantánea {#configure-buffering-for-instant-on-playback}

Con la activación instantánea, los usuarios pueden cambiar de canal y la reproducción se inicia inmediatamente sin tener que esperar. Cuando se activa el inicio instantáneo, TVSDK almacena en búfer uno o más canales antes de que comience la reproducción.

1. Confirme que el recurso se ha cargado y está listo para reproducirse comprobando que el estado es PREPARADO.
1. Antes de llamar `play`, llame a `prepareBuffer` para cada `MediaPlayer` ejemplo.

   Esto habilita el inicio instantáneo, lo que significa que TVSDK inicia el almacenamiento en búfer sin reproducir realmente el recurso de medios. TVSDK distribuye el `BUFFERING_COMPLETED` cuando el búfer está lleno.

   >[!NOTE]
   >
   >De forma predeterminada, `prepareBuffer` y `prepareToPlay` configure el flujo de medios para que comience a reproducirse desde el principio. Para empezar en otra posición, pase la posición (en milisegundos) a `prepareToPlay`.

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

1. Cuando reciba la `BUFFERING_COMPLETE` , empiece a reproducir el elemento o muestre comentarios visuales para indicar que el contenido está completamente almacenado en búfer.

   Si llama a `play`, la reproducción debe comenzar inmediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
