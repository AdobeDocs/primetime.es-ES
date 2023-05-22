---
description: Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Estadísticas de calidad del servicio
exl-id: 7684605f-e049-47bf-8073-155d1ff000e0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Estadísticas de calidad del servicio{#quality-of-service-statistics}

Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de QOS {#section_9996406E2D814FA382B77E3041CB02BC}

Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo desde el `PTQOSProvider` clase.

El `PTQOSProvider` proporciona varias estadísticas, incluida información sobre el almacenamiento en búfer, las velocidades de bits, las velocidades de fotogramas, los datos de tiempo, etc.

También proporciona información sobre el dispositivo, como el modelo, el sistema operativo y el ID de dispositivo del fabricante.

>[!TIP]
>
>No puede cambiar el tamaño del búfer de reproducción, pero puede supervisar el estado del tamaño del búfer para la depuración o el análisis. `PTPlaybackInformation` incluye propiedades como `playbackBufferFull` y `playbackLikelyToKeepUp`.

1. Cree una instancia de un reproductor multimedia.
1. Crear un `PTQOSProvider` y adjuntarlo al reproductor de contenidos.

   El `PTQOSProvider` toma un contexto del reproductor para poder recuperar información específica del dispositivo.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador, como un `NSTimer`, que recupera periódicamente los nuevos valores de QoS de la `PTQOSProvider`. Por ejemplo:

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
