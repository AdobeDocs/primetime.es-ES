---
description: TVSDK del explorador envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y los eventos de búsqueda.
title: Eventos de QoS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Eventos de QoS{#qos-events}

TVSDK del explorador envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y los eventos de búsqueda.

Para recibir notificaciones acerca de todos los eventos relacionados con QoS, cree una instancia de `AdobePSDK.QOSProvider` y adjunte la instancia de MediaPlayer a esta `QOSProvider` instancia:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configure un temporizador en la aplicación para comprobar periódicamente la `playbackInformation` propiedad del `qosProvider` ejemplo. El `playbackInformation` proporciona una instantánea de las estadísticas de reproducción actuales. Por ejemplo:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
