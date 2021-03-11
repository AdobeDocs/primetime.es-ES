---
description: Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Estadísticas de calidad del servicio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Estadísticas de calidad de servicio {#quality-of-service-statistics}

Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

TVSDK también proporciona información sobre los siguientes recursos descargados:

* Archivos de lista de reproducción/manifiesto
* Fragmentos de archivo
* Información de seguimiento de archivos

## Rastrear en el nivel de fragmento utilizando información de carga {#track-at-the-fragment-level-using-load-information}

Puede leer información sobre la calidad del servicio (QoS) acerca de los recursos descargados, como fragmentos y pistas, desde la clase LoadInformation .

1. Implemente el detector de eventos de llamada de retorno `onLoadInformationAvailable`.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registre el detector de eventos, al que llama TVSDK cada vez que se descarga un fragmento.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Lea los datos de interés de `LoadInformation` que se pasan a la rellamada.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> Propiedad </th> 
      <th colname="col1" class="entry"> Tipo </th> 
      <th colname="col2" class="entry"> Descripción </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> <p>Duración de la descarga en milisegundos. </p> <p>TVSDK no diferencia entre el tiempo que tardó el cliente en conectarse al servidor y el tiempo que tardó en descargar el fragmento completo. Por ejemplo, si la descarga de un segmento de 10 MB tarda 8 segundos, TVSDK proporciona esa información, pero no le indica que se tardaron 4 segundos hasta el primer byte y otros 4 segundos en descargar el fragmento completo. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> Duración del contenido de los fragmentos descargados en milisegundos. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> El tamaño del recurso descargado en bytes. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> Índice de la pista correspondiente, si se conoce; de lo contrario, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> el nombre de la pista correspondiente, si se conoce; de lo contrario, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> el tipo de pista correspondiente, si se conoce; de lo contrario, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> Qué ha descargado TVSDK. Uno de los siguientes: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFIESTO: lista de reproducción/manifiesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENTO: Un fragmento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK: fragmento asociado a una pista específica </li> 
      </ul> A veces, es posible que no sea posible detectar el tipo de recurso. Si esto ocurre, se devuelve FILE. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> Dirección URL que señala al recurso descargado. </td> 
   </tr> 
   </tbody> 
   </table>

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS {#read-qos-playback-buffering-and-device-statistics}

Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos desde la clase QOSProvider.

La clase `QOSProvider` proporciona varias estadísticas, incluida información sobre el almacenamiento en búfer, las tasas de bits, las tasas de fotogramas, los datos de tiempo, etc.

También proporciona información sobre el dispositivo, como el fabricante, el modelo, el sistema operativo, la versión del SDK y el tamaño/densidad de la pantalla.

1. Cree una instancia de un reproductor de medios.
1. Cree un objeto `QOSProvider` y adjúntelo al reproductor de medios.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador que obtenga periódicamente los nuevos valores de QoS de `QOSProvider`. Por ejemplo:

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
