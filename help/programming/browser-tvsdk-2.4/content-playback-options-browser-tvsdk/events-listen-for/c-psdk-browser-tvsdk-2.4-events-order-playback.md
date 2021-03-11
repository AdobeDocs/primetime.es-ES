---
description: El SDK de TVSDK de explorador envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.
title: Orden de los eventos de reproducción
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Orden de los eventos de reproducción{#order-of-playback-events}

El SDK de TVSDK de explorador envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

Los siguientes ejemplos muestran el orden de algunos eventos que incluyen eventos de reproducción.

* Cuando se carga correctamente un recurso de medios a través de `replaceCurrentResource`, el orden de los eventos es:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` con  `event.status =`

      * `MediaPlayerStatus.INITIALIZING`
      * `MediaPlayerStatus.INITIALIZED`

* Al prepararse para la reproducción mediante `MediaPlayer.prepareToPlay`, el orden de los eventos es:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` con  `event.status =`

      * `MediaPlayerStatus.PREPARING`
      * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

El siguiente ejemplo muestra una progresión típica de eventos:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                 onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
            console.log("Player Status: INITIALIZING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            console.log("Player Status: INITIALIZED"); 
            player.prepareToPlay(); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARING: 
            console.log("Player Status: PREPARING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
            console.log("Player Status: PREPARED"); 
            if (autoPlay) { 
                player.play(); 
            } 
            else { 
                dispatchEvent(ReferencePlayer.Events.PreparedEvent,  
                              {target: this}); 
            } 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PLAYING: 
            console.log("Player Status: PLAYING"); 
            //update UI play/pause to show pause icon 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PAUSED: 
            console.log("Player Status: PAUSED"); 
            //update UI play/pause to show play icon &  
            //display pause icon over video 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.SEEKING: 
            console.log("Player Status: SEEKING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.COMPLETE: 
            console.log("Player Status: COMPLETE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.RELEASED: 
            console.log("Player Status: RELEASED"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            console.log("Player Status: ERROR"); 
            break; 
    } 
};
```

