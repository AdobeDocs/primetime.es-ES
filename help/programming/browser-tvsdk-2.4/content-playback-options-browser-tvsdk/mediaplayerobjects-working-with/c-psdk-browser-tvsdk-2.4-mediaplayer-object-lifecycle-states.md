---
description: Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que finaliza, esta instancia pasa de un estado a otro.
seo-description: Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que finaliza, esta instancia pasa de un estado a otro.
seo-title: Ciclo de vida y estados del objeto MediaPlayer
title: Ciclo de vida y estados del objeto MediaPlayer
uuid: fe76ea80-aaa8-43bc-9b81-85e0551f70dd
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Ciclo de vida y estados del objeto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que finaliza, esta instancia pasa de un estado a otro.

Estos son los posibles estados:

* **IDLE**: `MediaPlayerStatus.IDLE`

* **INICIALIZACIÓN**: `MediaPlayerStatus.INITIALIZING`

* **INICIALIZADO**: `MediaPlayerStatus.INITIALIZED`

* **PREPARACIÓN**: `MediaPlayerStatus.PREPARING`

* **PREPARADO**: `MediaPlayerStatus.PREPARED`

* **REPRODUCCIÓN**: `MediaPlayerStatus.PLAYING`

* **EN PAUSA**: `MediaPlayerStatus.PAUSED`

* **BUSCANDO**: `MediaPlayerStatus.SEEKING`

* **COMPLETAR**: `MediaPlayerStatus.COMPLETE`

* **ERROR**: `MediaPlayerStatus.ERROR`

* **LANZADO**: `MediaPlayerStatus.RELEASED`

La lista completa de estados se define en `MediaPlayerStatus`.

Conocer el estado del reproductor es útil porque algunas operaciones solo se permiten mientras el reproductor se encuentra en un estado concreto. Por ejemplo, `play` no se puede llamar mientras esté en el estado IDLE. Debe llamarse después de alcanzar el estado PREPARADO. El estado ERROR también cambia lo que puede suceder a continuación.

A medida que se carga y reproduce un recurso multimedia, el reproductor realiza la siguiente transición:

1. El estado inicial es IDLE.
1. La aplicación llama `MediaPlayer.replaceCurrentResource`, que mueve el reproductor al estado INICIALIZANDO.
1. Si TVSDK del explorador carga correctamente el recurso, el estado cambia a INITIALIZED.
1. La aplicación llama `MediaPlayer.prepareToPlay`y el estado cambia a PREPARING.
1. El SDK del explorador prepara el flujo de medios e inicia la resolución de publicidad y la inserción de anuncios (si está activada).

   Cuando se completa este paso, las publicidades se insertan en la línea de tiempo o el procedimiento de publicidad ha fallado y el estado del reproductor cambia a PREPARADO.
1. A medida que la aplicación se reproduce y pausa los medios, el estado se mueve entre REPRODUCIR y PAUSAR.

   >[!TIP]
   >
   >Durante la reproducción o pausa, cuando se sale de la reproducción, se apaga el dispositivo o se cambia de aplicación, el estado cambia a SUSPENDIDO y se liberan los recursos. Para continuar, restaure el reproductor multimedia.

1. Cuando el reproductor llega al final del flujo, el estado se convierte en COMPLETO.
1. Cuando la aplicación libera el reproductor de medios, el estado cambia a LANZADO.
1. Si se produce un error durante el proceso, el estado cambia a ERROR.

Esta es una ilustración del ciclo de vida de una instancia de MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Puede utilizar el estado para proporcionar comentarios al usuario sobre el proceso (por ejemplo, un control giratorio mientras espera el siguiente cambio de estado) o para realizar los siguientes pasos en la reproducción de medios, como esperar al estado adecuado antes de llamar al siguiente método.

Por ejemplo:

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 
```

