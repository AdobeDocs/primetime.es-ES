---
description: Puede leer estadísticas de reproducción, almacenamiento en búfer y dispositivos desde la clase QOSProvider.
seo-description: Puede leer estadísticas de reproducción, almacenamiento en búfer y dispositivos desde la clase QOSProvider.
seo-title: Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS
title: Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS
uuid: 5ee631fc-cd6f-4f35-8621-2ffdc51a57c7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS{#read-qos-playback-buffering-and-device-statistics}

Puede leer estadísticas de reproducción, almacenamiento en búfer y dispositivos desde la clase QOSProvider.

La `QOSProvider` clase proporciona varias estadísticas, incluida información sobre almacenamiento en búfer, velocidades de bits, velocidades de fotogramas, datos de tiempo, etc.

También proporciona información sobre el dispositivo, como el fabricante, el modelo, el sistema operativo, la versión del SDK y el tamaño y la densidad de la pantalla.

1. Cree una instancia de un reproductor multimedia.
1. Cree un `QOSProvider` objeto y adjúntelo al reproductor de medios.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador que recopile periódicamente los nuevos valores de QoS del `QOSProvider`. Por ejemplo:

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

