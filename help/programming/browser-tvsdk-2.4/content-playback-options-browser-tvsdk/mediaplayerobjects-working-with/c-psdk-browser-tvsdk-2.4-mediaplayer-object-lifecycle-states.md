---
description: Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que se termina, esta instancia pasa de un estado a otro.
title: Ciclo de vida y estados del objeto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Ciclo de vida y estados del objeto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

Desde el momento en que se crea la instancia de MediaPlayer hasta el momento en que se termina, esta instancia pasa de un estado a otro.

Estos son los estados posibles:

* **IDLE**:  `MediaPlayerStatus.IDLE`

* **INICIALIZACIÓN**:  `MediaPlayerStatus.INITIALIZING`

* **INICIALIZADO**:  `MediaPlayerStatus.INITIALIZED`

* **PREPARACIÓN**:  `MediaPlayerStatus.PREPARING`

* **PREPARADO**:  `MediaPlayerStatus.PREPARED`

* **REPRODUCIENDO**:  `MediaPlayerStatus.PLAYING`

* **EN PAUSA**:  `MediaPlayerStatus.PAUSED`

* **BUSCANDO**:  `MediaPlayerStatus.SEEKING`

* **COMPLETAR**:  `MediaPlayerStatus.COMPLETE`

* **ERROR**:  `MediaPlayerStatus.ERROR`

* **LANZADO**:  `MediaPlayerStatus.RELEASED`

La lista completa de estados se define en `MediaPlayerStatus`.

Conocer el estado del reproductor es útil porque algunas operaciones solo se permiten mientras el reproductor esté en un estado concreto. Por ejemplo, no se puede llamar a `play` mientras se encuentra en el estado IDLE. Debe llamarse después de alcanzar el estado PREPARADO. El estado ERROR también cambia lo que puede suceder a continuación.

A medida que se carga y reproduce un recurso multimedia, el reproductor realiza la siguiente transición:

1. El estado inicial es IDLE.
1. La aplicación llama a `MediaPlayer.replaceCurrentResource`, que mueve el reproductor al estado INICIALIZAR.
1. Si el TVSDK del explorador carga correctamente el recurso, el estado cambia a INITIALIZADO.
1. La aplicación llama a `MediaPlayer.prepareToPlay` y el estado cambia a PREPARACIÓN.
1. El SDK del explorador prepara el flujo de medios e inicia la resolución de anuncios y la inserción de anuncios (si está habilitada).

   Una vez completado este paso, se insertan anuncios en la cronología o el procedimiento publicitario ha fallado, y el estado del reproductor cambia a PREPARADO.
1. A medida que la aplicación reproduce y pone en pausa el contenido, el estado se mueve entre REPRODUCIR y PAUSADO.

   >[!TIP]
   >
   >Cuando se reproduce o se pone en pausa, cuando se sale de la reproducción, se apaga el dispositivo o se cambia de aplicación, el estado cambia a SUSPENDED y se liberan los recursos. Para continuar, restaure el reproductor multimedia.

1. Cuando el reproductor llega al final de la emisión, el estado se vuelve COMPLETO.
1. Cuando la aplicación libera el reproductor de contenido, el estado cambia a LANZADO.
1. Si se produce un error durante el proceso, el estado cambia a ERROR.

Esta es una ilustración del ciclo de vida de una instancia de MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Puede utilizar el estado para proporcionar comentarios al usuario sobre el proceso (por ejemplo, un control de número mientras espera el siguiente cambio de estado) o para realizar los siguientes pasos en la reproducción del contenido, como esperar al estado adecuado antes de llamar al siguiente método.

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

