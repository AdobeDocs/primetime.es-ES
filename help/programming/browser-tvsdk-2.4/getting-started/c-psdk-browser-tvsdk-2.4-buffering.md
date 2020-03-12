---
description: Puede configurar imágenes para notificar al usuario que el contenido se está almacenando en búfer.
seo-description: Puede configurar imágenes para notificar al usuario que el contenido se está almacenando en búfer.
seo-title: Almacenamiento en búfer
title: Almacenamiento en búfer
uuid: da9498ee-c736-4093-97a2-250d3ad56d49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Almacenamiento en búfer{#buffering}

Puede configurar imágenes para notificar al usuario que el contenido se está almacenando en búfer.

Escucha `AdobePSDK.PSDKEventType.BUFFERING_BEGIN` y `AdobePSDK.PSDKEventType.BUFFERING_END` eventos. Por ejemplo:

```js
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_BEGIN,  
                        function (event) { 
                            buffering = true; 
                            // add buffering layer 
                        }); 
  
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_END,  
                        function (event) { 
                           buffering = false; 
                           // remove buffering layer 
                        });
```

El marco de interfaz de usuario proporciona una implementación de comportamiento de superposición de almacenamiento en búfer predeterminada, que se puede ampliar como se muestra a continuación:

```js
// Using UI Framework 
function myBufferingOverlayBehavior (element, configuration, player, localize, baseLog) { 
    return ptp.bufferingOverlayBehavior(element, configuration, player, localize, baseLog); 
} 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource:'Specify Resource URL', 
        bufferingOverlay: { 
            behavior: myBufferingOverlayBehavior, 
            classNames: 'ptp-buffering-overlay my_buffering_overlay_bar' 
        } 
    } 
 
}); 
```

Así es como se ve el DOM de resultado:

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```

