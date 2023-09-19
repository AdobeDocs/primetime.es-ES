---
description: Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. El TVSDK del explorador proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Estadísticas de calidad del servicio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Estadísticas de calidad del servicio{#quality-of-service-statistics}

Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. El TVSDK del explorador proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de QOS {#read-qos-playback-buffering-and-device-statistics}

Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de la clase QOSProvider.

El `QOSProvider` proporciona varias estadísticas, incluida información sobre el almacenamiento en búfer, las velocidades de bits, las velocidades de fotogramas, los datos de tiempo, etc.

1. Cree una instancia de un reproductor multimedia.
1. Crear un `QOSProvider` y adjuntarlo al reproductor de contenidos.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador, que recupere periódicamente los nuevos valores de QoS de la `QOSProvider`. Por ejemplo:

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
   
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
   
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
   
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
   
   qosTimer.start(); 
   ```

1. (Opcional) Lea la información específica del dispositivo.

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
