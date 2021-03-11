---
description: Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. El SDK de explorador proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Estadísticas de calidad del servicio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---


# Estadísticas de calidad de servicio{#quality-of-service-statistics}

Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. El SDK de explorador proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS {#read-qos-playback-buffering-and-device-statistics}

Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos desde la clase QOSProvider.

La clase `QOSProvider` proporciona varias estadísticas, incluida información sobre el almacenamiento en búfer, las tasas de bits, las tasas de fotogramas, los datos de tiempo, etc.

1. Cree una instancia de un reproductor de medios.
1. Cree un objeto `QOSProvider` y adjúntelo al reproductor de medios.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador que obtenga periódicamente los nuevos valores de QoS de `QOSProvider`. Por ejemplo:

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
