---
description: Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.
seo-description: Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.
seo-title: Guardar la posición del vídeo y reanudarlo más tarde
title: Guardar la posición del vídeo y reanudarlo más tarde
uuid: cff1715e-c7a9-4eda-ad71-31892c3c1e78
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Guarde la posición del vídeo y reanude más tarde {#save-the-video-position-and-resume-later}

Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.

Las publicidades insertadas dinámicamente difieren entre las sesiones de usuario, por lo que al guardar la posición **con** publicidades duplicadas se hace referencia a una posición diferente en una sesión futura. TVSDK proporciona métodos para recuperar la posición de reproducción e ignorar las publicidades duplicadas.

1. Cuando el usuario cierra un vídeo, la aplicación recupera y guarda la posición en el vídeo.

   >[!TIP]
   >
   >No se incluyen las duraciones de los anuncios.

   Los saltos de publicidad pueden variar en cada sesión debido a patrones de publicidad, límites de frecuencia, etc. La hora actual del vídeo en una sesión puede ser diferente en una sesión futura. Al guardar una posición en el vídeo, la aplicación recupera la hora local, que puede guardar en el dispositivo o en una base de datos del servidor.

   Por ejemplo: si el usuario se encuentra en el minuto 20 del vídeo y esta posición incluye cinco minutos de anuncios, `getCurrentTime` devolverá 1200 segundos, mientras que `getLocalTime` en esta posición devolverá 900 segundos.

   >[!IMPORTANT]
   >
   >La hora local y la hora actual son las mismas para flujos en directo/lineales. En este caso, `convertToLocalTime` no tiene ningún efecto. Para VOD, el tiempo local permanece sin cambios mientras se reproducen los anuncios.

   ```java
   // Save the user session when player activity stops 
       @Override 
       public void onStop(){ 
           super.onStop(); 
           ... 
           prefs = PreferenceManager.getDefaultSharedPreferences( 
                                     getActivity().getApplicationContext()); 
           SharedPreferences.Editor editor = prefs.edit(); 
           // get the local time where stream stopped playing and  
           // save it in System preferences 
           editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
           editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
           editor.commit(); 
           ... 
       }
   ```

1. Restaure la sesión de usuario cuando se reanude la actividad del reproductor.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs =  
         PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil"). 
         equals(_contentInfo.toMediaResource().getUrl())) { 
           _lastKnownLocalTime =  
             prefs.getLong(LAST_LOCAL_TIME, 0); // get the last local time  
                                                // saved in system preferences 
           if(_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. Para reanudar el vídeo en la misma posición:

   * Para reanudar la reproducción del vídeo desde la posición guardada en una sesión anterior, utilice `seekToLocalTime`.

      >[!TIP]
      >
      >Este método solo se llama con valores de hora locales. Si se llama al método con los resultados de tiempo actuales, se produce un comportamiento incorrecto.

   * Para buscar la hora actual, utilice `seek`.

1. Cuando la aplicación reciba el evento de cambio de estado `onStatusChanged`, busque la hora local guardada.

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if(_shouldResumePlayback){ 
               if(_lastKnownLocalTime >= 0) { 
                    _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
       ... 
   }
   ```

1. Proporcione los saltos de publicidad como se especifica en la interfaz de directivas de publicidad.
1. Implemente un selector de directivas de publicidad personalizado ampliando el selector de directivas de publicidad predeterminado.
1. Proporcione los pausas publicitarias que deben presentarse al usuario implementando `selectAdBreaksToPlay`.

   Este método incluye una pausa publicitaria previa y las pausas publicitarias intermedias antes de la posición horaria local. La aplicación puede decidir reproducir una pausa publicitaria previa y reanudar a la hora local especificada, reproducir una pausa publicitaria media y reanudar a la hora local especificada o no reproducir ninguna pausa publicitaria.