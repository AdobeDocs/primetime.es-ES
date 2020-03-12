---
description: Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. El SDK TVSDK del explorador proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-description: Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. El SDK TVSDK del explorador proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-title: Estadísticas de calidad del servicio
title: Estadísticas de calidad del servicio
uuid: e4bb2617-d8a7-4da7-b669-d6ffab2864bb
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Estadísticas de calidad del servicio{#quality-of-service-statistics}

Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. El SDK TVSDK del explorador proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS {#read-qos-playback-buffering-and-device-statistics}

Puede leer estadísticas de reproducción, almacenamiento en búfer y dispositivos desde la clase QOSProvider.

La `QOSProvider` clase proporciona varias estadísticas, incluida información sobre almacenamiento en búfer, velocidades de bits, velocidades de fotogramas, datos de tiempo, etc.

1. Cree una instancia de un reproductor multimedia.
1. Cree un `QOSProvider` objeto y adjúntelo al reproductor de medios.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador que recopile periódicamente los nuevos valores de QoS del `QOSProvider`. Por ejemplo:

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
