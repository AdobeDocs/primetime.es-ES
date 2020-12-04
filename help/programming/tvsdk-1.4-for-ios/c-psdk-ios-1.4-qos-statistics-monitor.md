---
description: Calidad de servicio (QoS) oferta una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-description: Calidad de servicio (QoS) oferta una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-title: Estadísticas de calidad del servicio
title: Estadísticas de calidad del servicio
uuid: b74cbc94-1d69-4b4b-b969-d0e985b4762b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Estadísticas de calidad del servicio{#quality-of-service-statistics}

Calidad de servicio (QoS) oferta una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS {#section_9996406E2D814FA382B77E3041CB02BC}

Puede leer estadísticas de reproducción, almacenamiento en búfer y dispositivos de la clase `PTQOSProvider`.

La clase `PTQOSProvider` proporciona varias estadísticas, incluida información sobre almacenamiento en búfer, velocidades de bits, velocidades de fotogramas, datos de tiempo, etc.

También proporciona información sobre el dispositivo, como el modelo, el sistema operativo y el ID del dispositivo del fabricante.

>[!TIP]
>
>No se puede cambiar el tamaño del búfer de reproducción, pero se puede supervisar el estado del tamaño del búfer para la depuración o la análisis. `PTPlaybackInformation` incluye propiedades como  `playbackBufferFull` y  `playbackLikelyToKeepUp`.

1. Cree una instancia de un reproductor multimedia.
1. Cree un objeto `PTQOSProvider` y adjúntelo al reproductor de medios.

   El constructor `PTQOSProvider` toma un contexto de reproductor para poder recuperar información específica del dispositivo.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador, como `NSTimer`, que recopila periódicamente los nuevos valores de QoS de `PTQOSProvider`. Por ejemplo:

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

