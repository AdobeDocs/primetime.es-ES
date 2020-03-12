---
description: El SDK de TVSDK del explorador distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.
seo-description: El SDK de TVSDK del explorador distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.
seo-title: Eventos de QoS
title: Eventos de QoS
uuid: 3384bc51-b435-4cd9-a1f8-9abf2605205b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Eventos de QoS{#qos-events}

El SDK de TVSDK del explorador distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.

Para recibir notificaciones sobre todos los eventos relacionados con QoS, cree una instancia de MediaPlayer `AdobePSDK.QOSProvider` y adjunte la instancia de MediaPlayer a esta `QOSProvider` instancia:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configure un temporizador en la aplicación para comprobar periódicamente la `playbackInformation` propiedad de la `qosProvider` instancia. La `playbackInformation` propiedad proporciona una instantánea de las estadísticas de reproducción actuales. Por ejemplo:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

