---
description: Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que finaliza, esta instancia pasa de un estado al siguiente.
title: Ciclo de vida y estados del objeto MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Ciclo de vida y estados del objeto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que finaliza, esta instancia pasa de un estado al siguiente.

Estos son los estados posibles:

* **INACTIVO**: `MediaPlayerStatus.IDLE`

* **INICIALIZACIÓN**: `MediaPlayerStatus.INITIALIZING`

* **INICIALIZADO**: `MediaPlayerStatus.INITIALIZED`

* **PREPARANDO**: `MediaPlayerStatus.PREPARING`

* **PREPARADO**: `MediaPlayerStatus.PREPARED`

* **JUGANDO**: `MediaPlayerStatus.PLAYING`

* **PAUSADO**: `MediaPlayerStatus.PAUSED`

* **BUSCANDO**: `MediaPlayerStatus.SEEKING`

* **COMPLETADO**: `MediaPlayerStatus.COMPLETE`

* **ERROR**: `MediaPlayerStatus.ERROR`

* **PUBLICADO**: `MediaPlayerStatus.RELEASED`

La lista completa de estados se define en `MediaPlayerStatus`.

Conocer el estado del reproductor es útil porque algunas operaciones solo se permiten mientras el reproductor está en un estado particular. Por ejemplo, `play` no se puede llamar mientras se esté en estado IDLE. Debe llamarse después de alcanzar el estado PREPARADO. El estado ERROR también cambia lo que puede suceder a continuación.

Cuando se carga y reproduce un recurso multimedia, el reproductor realiza la transición de la siguiente manera:

1. El estado inicial es IDLE.
1. La aplicación llama a `MediaPlayer.replaceCurrentResource`, que mueve el reproductor al estado INICIALIZANDO.
1. Si el TVSDK del explorador carga correctamente el recurso, el estado cambia a INITIALIZED.
1. La aplicación llama a `MediaPlayer.prepareToPlay`y el estado cambia a PREPARING.
1. TVSDK del explorador prepara el flujo de medios e inicia la resolución de anuncios y la inserción de anuncios (si está activada).

   Cuando se completa este paso, los anuncios se insertan en la cronología o el procedimiento de publicidad ha fallado y el estado del reproductor cambia a PREPARADO.
1. A medida que la aplicación reproduce y pausa el contenido, el estado cambia entre REPRODUCIR y PAUSADO.

   >[!TIP]
   >
   >Mientras se reproduce o está en pausa, cuando sale de la reproducción, apaga el dispositivo o cambia de aplicación, el estado cambia a SUSPENDIDO y los recursos se liberan. Para continuar, restaure el reproductor de contenidos.

1. Cuando el reproductor llega al final del flujo, el estado se vuelve COMPLETO.
1. Cuando la aplicación libera el reproductor de contenido, el estado cambia a RELEASED.
1. Si se produce un error durante el proceso, el estado cambia a ERROR.

Esta es una ilustración del ciclo de vida de una instancia de MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Puede utilizar el estado para proporcionar comentarios al usuario sobre el proceso (por ejemplo, un control de número mientras espera el siguiente cambio de estado) o para dar los siguientes pasos durante la reproducción del contenido, como esperar al estado adecuado antes de llamar al siguiente método.

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
