---
description: Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Estadísticas de calidad del servicio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Estadísticas de calidad de servicio{#quality-of-service-statistics}

Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS {#section_9996406E2D814FA382B77E3041CB02BC}

Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos desde la clase `PTQOSProvider` .

La clase `PTQOSProvider` proporciona varias estadísticas, incluida información sobre el almacenamiento en búfer, las tasas de bits, las tasas de fotogramas, los datos de tiempo, etc.

También proporciona información sobre el dispositivo, como el modelo, el sistema operativo y el ID del dispositivo del fabricante.

>[!TIP]
>
>No se puede cambiar el tamaño del búfer de reproducción, pero se puede supervisar el estado del tamaño del búfer para su depuración o análisis. `PTPlaybackInformation` incluye propiedades como  `playbackBufferFull` y  `playbackLikelyToKeepUp`.

1. Cree una instancia de un reproductor de medios.
1. Cree un objeto `PTQOSProvider` y adjúntelo al reproductor de medios.

   El constructor `PTQOSProvider` toma un contexto de reproductor para que pueda recuperar información específica del dispositivo.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador, como `NSTimer`, que obtenga periódicamente los nuevos valores de QoS de `PTQOSProvider`. Por ejemplo:

   ```
   - (void)printPlaybackInfoLog { 
       PTPlaybackInformation *playbackInfo = qosProvider.playbackInformation;  
       if (playbackInfo) { 
           // For example: 
           NSString *infoLog = [NSString stringWithFormat:@"observedBitrate :  
                                  %f\n",playbackInfo.observedBitrate]; 
           [consoleView logMessage:@"====%@\n\n",infoLog]; 
       } 
   }
   ```

1. (Opcional) Lea la información específica del dispositivo.

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```

