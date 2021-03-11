---
description: El TVSDK del explorador envía eventos de calidad de servicio (QoS) para notificar a la aplicación de los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.
title: Eventos de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Eventos de QoS{#qos-events}

El TVSDK del explorador envía eventos de calidad de servicio (QoS) para notificar a la aplicación de los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.

Para recibir notificaciones sobre todos los eventos relacionados con QoS, cree una instancia de `AdobePSDK.QOSProvider` y adjunte la instancia de MediaPlayer a esta instancia de `QOSProvider`:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configure un temporizador en la aplicación para comprobar periódicamente la propiedad `playbackInformation` de la instancia `qosProvider`. La propiedad `playbackInformation` proporciona una instantánea de las estadísticas de reproducción actuales. Por ejemplo:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

