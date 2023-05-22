---
description: Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de la clase QOSProvider.
title: Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de QOS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de QOS{#read-qos-playback-buffering-and-device-statistics}

Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de la clase QOSProvider.

El `QOSProvider` proporciona varias estadísticas, incluida información sobre el almacenamiento en búfer, las velocidades de bits, las velocidades de fotogramas, los datos de tiempo, etc.

También proporciona información sobre el dispositivo, como el fabricante, el modelo, el sistema operativo, la versión del SDK y el tamaño/densidad de la pantalla.

1. Cree una instancia de un reproductor multimedia.
1. Crear un `QOSProvider` y adjuntarlo al reproductor de contenidos.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador, que recupere periódicamente los nuevos valores de QoS de la `QOSProvider`. Por ejemplo:

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. (Opcional) Lea la información específica del dispositivo.

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```

