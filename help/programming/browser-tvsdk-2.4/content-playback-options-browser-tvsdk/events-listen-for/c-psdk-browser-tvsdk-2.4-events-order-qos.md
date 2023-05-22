---
description: TVSDK del explorador envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y los eventos de búsqueda.
title: Eventos de QoS
exl-id: b0fab68e-ef0f-4812-b4ad-3f69dcdf2d9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
