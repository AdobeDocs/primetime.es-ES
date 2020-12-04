---
description: El término instantáneo en hace referencia a la precarga de uno o varios canales para que un usuario que selecciona un canal o cambia de canal vea que el contenido se reproduce inmediatamente. El almacenamiento en búfer ya se realiza cuando el usuario inicio de verlo.
seo-description: El término instantáneo en hace referencia a la precarga de uno o varios canales para que un usuario que selecciona un canal o cambia de canal vea que el contenido se reproduce inmediatamente. El almacenamiento en búfer ya se realiza cuando el usuario inicio de verlo.
seo-title: Instantáneo en
title: Instantáneo en
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Instantáneo en {#instant-on}

El término instantáneo en hace referencia a la precarga de uno o varios canales para que un usuario que selecciona un canal o cambia de canal vea que el contenido se reproduce inmediatamente. El almacenamiento en búfer ya se realiza cuando el usuario inicio de verlo.

Sin activación instantánea, TVSDK inicializa el medio que se va a reproducir, pero no almacena en inicio el almacenamiento en búfer del flujo hasta que la aplicación llama a `play`. El usuario no ve ningún contenido hasta que se completa el almacenamiento en búfer. Con la activación instantánea, puede iniciar varias instancias de reproductor de medios (o cargador de elementos de reproductor de medios) y inicios TVSDK almacenando en búfer los flujos inmediatamente.

Cuando un usuario cambia el canal y el flujo se almacena en el búfer correctamente, llamando `play` en el nuevo inicio de canal se reproduce inmediatamente.

Aunque no hay límites en el número de instancias `MediaPlayer` que TVSDK puede ejecutar, la ejecución de más instancias consume más recursos. El rendimiento de la aplicación puede verse afectado por el número de instancias que se ejecutan. Para obtener más información sobre estas instancias, consulte [Carga de un recurso de medios mediante MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurar el almacenamiento en búfer para la reproducción instantánea {#configure-buffering-for-instant-on-playback}

Con la activación instantánea, los usuarios pueden cambiar los canales y los inicios de reproducción inmediatamente sin tener que esperar. Cuando se activa instantáneamente, TVSDK almacena en el búfer uno o varios canales antes de que comience la reproducción.

1. Confirme que el recurso se ha cargado y está listo para reproducirse comprobando que el estado está PREPARADO.
1. Antes de llamar a `play`, llame a `prepareBuffer` para cada instancia `MediaPlayer`.

   Esto habilita la activación instantánea, lo que significa que TVSDK inicio el almacenamiento en búfer sin reproducir realmente el recurso de medios. TVSDK distribuye el evento `BUFFERING_COMPLETED` cuando el búfer está lleno.

   >[!NOTE]
   >
   >De forma predeterminada, `prepareBuffer` y `prepareToPlay` configuran el flujo de medios para que se reproduzca en inicio desde el principio. Para inicio en otra posición, pase la posición (en milisegundos) a `prepareToPlay`.

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

1. Cuando recibe el evento `BUFFERING_COMPLETE`, inicio al reproducir el elemento o muestre información visual para indicar que el contenido se almacena completamente en el búfer.

   Si llama a `play`, la reproducción debe comenzar inmediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
