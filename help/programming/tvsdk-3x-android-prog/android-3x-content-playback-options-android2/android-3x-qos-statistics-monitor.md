---
description: La calidad de servicio (QoS) proporciona una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-description: La calidad de servicio (QoS) proporciona una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-title: Estadísticas de calidad del servicio
title: Estadísticas de calidad del servicio
uuid: 3d66ed44-9d4a-4162-962f-e238575ff2dd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---


# Estadísticas de calidad del servicio {#quality-of-service-statistics}

La calidad de servicio (QoS) proporciona una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

TVSDK también proporciona información sobre los siguientes recursos descargados:

* Archivos de lista de reproducción/manifiesto
* Fragmentos de archivo
* Información de seguimiento de archivos

## Rastree en el nivel de fragmento mediante la información de carga {#section_4439D91E8EDC45588EF1D7BE25697350}

Puede leer información de calidad de servicio (QoS) sobre los recursos descargados, como fragmentos y pistas, desde la clase `LoadInformation`.

1. Implemente y registre el detector de evento `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`.
1. Llame a `event.getLoadInformation()` para leer los datos relevantes del parámetro `event` que se pasa a la llamada de retorno.

   >[!NOTE]
   >
   >Para obtener más información sobre `LoadInformation`, consulte [3.0 para documentos de API de Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.0/index.html).

## Leer las estadísticas de reproducción, almacenamiento en búfer y dispositivos de QOS {#section_D21722600F324E67A9F06234D338B243}

Puede leer estadísticas de reproducción, almacenamiento en búfer y dispositivos de la clase `QOSProvider`.

La clase `QOSProvider` proporciona varias estadísticas, incluida información sobre almacenamiento en búfer, velocidades de bits, velocidades de fotogramas, datos de tiempo, etc. También proporciona información sobre el dispositivo, como el fabricante, el modelo, el sistema operativo, la versión del SDK, el ID del dispositivo del fabricante y el tamaño y la densidad de la pantalla.

1. Cree una instancia de un reproductor multimedia.
1. Cree un objeto `QOSProvider` y adjúntelo al reproductor de medios.

   El constructor `QOSProvider` toma un contexto de reproductor para poder recuperar información específica del dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Lea las estadísticas de reproducción.

   Una solución para leer las estadísticas de reproducción es tener un temporizador que recopila periódicamente los nuevos valores de QoS de `QOSProvider`.

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
