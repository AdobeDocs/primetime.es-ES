---
description: Calidad de servicio (QoS) proporciona una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Estadísticas de calidad del servicio
exl-id: 62b2b65e-7383-4694-bdec-aacc4c2ae372
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Estadísticas de calidad del servicio {#quality-of-service-statistics}

Calidad de servicio (QoS) proporciona una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

TVSDK también proporciona información sobre los siguientes recursos descargados:

* Archivos de lista de reproducción/manifiesto
* Fragmentos de archivo
* Información de seguimiento para archivos

## Seguimiento en el nivel de fragmento mediante información de carga {#section_4439D91E8EDC45588EF1D7BE25697350}

Puede leer la información de calidad de servicio (QoS) sobre los recursos descargados, como fragmentos y pistas, desde el `LoadInformation` clase.

1. Implementación y registro de `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` detector de eventos.
1. Llamada `event.getLoadInformation()` para leer los datos pertinentes de la `event` parámetro que se pasa a la llamada de retorno.

   >[!NOTE]
   >
   >Para obtener más información sobre `LoadInformation`, consulte [3.0 para Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.0/index.html) Documentos de API.

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo de QOS {#section_D21722600F324E67A9F06234D338B243}

Puede leer las estadísticas de reproducción, almacenamiento en búfer y dispositivo desde el `QOSProvider` clase.

El `QOSProvider` proporciona varias estadísticas, incluida información sobre el almacenamiento en búfer, las velocidades de bits, las velocidades de fotogramas, los datos de tiempo, etc. También proporciona información sobre el dispositivo, como el fabricante, el modelo, el sistema operativo, la versión del SDK, el ID de dispositivo del fabricante y el tamaño/densidad de la pantalla.

1. Cree una instancia de un reproductor multimedia.
1. Crear un `QOSProvider` y adjuntarlo al reproductor de contenidos.

   El `QOSProvider` toma un contexto del reproductor para poder recuperar información específica del dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador, que recupere periódicamente los nuevos valores de QoS de la `QOSProvider`.

   Por ejemplo:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   ```

1. (Opcional) Lea la información específica del dispositivo.

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   ```
