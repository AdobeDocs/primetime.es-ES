---
description: Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.
title: Guardar la posición del vídeo y reanudarlo más tarde
exl-id: 6b1eeeeb-ae13-437f-80cc-1ceb7bf8ac19
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Guardar la posición del vídeo y reanudarlo más tarde {#save-the-video-position-and-resume-later}

Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.

Los anuncios insertados dinámicamente difieren entre las sesiones de usuario, por lo que se guarda la posición **con** los anuncios empalmados hacen referencia a una posición diferente en una sesión futura. TVSDK proporciona métodos para recuperar la posición de reproducción al ignorar los anuncios empalmados.

1. Cuando el usuario sale de un vídeo, la aplicación recupera y guarda la posición en el vídeo.

   >[!TIP]
   >
   >No se incluyen las duraciones de los anuncios.

   Las pausas publicitarias pueden variar en cada sesión debido a patrones de anuncios, restricción de frecuencia, etc. La hora actual del vídeo en una sesión puede ser diferente en una sesión futura. Al guardar una posición en el vídeo, la aplicación recupera la hora local, que puede guardar en el dispositivo o en una base de datos en el servidor.

   Por ejemplo, si el usuario se encuentra en el minuto 20 del vídeo y esta posición incluye cinco minutos de anuncios, `getCurrentTime` devolverá 1200 segundos, mientras que `getLocalTime` en esta posición volverá 900 segundos.

   >[!IMPORTANT]
   >
   >La hora local y la hora actual son las mismas para los flujos en directo/lineales. En este caso, `convertToLocalTime` no tiene ningún efecto. En VOD, la hora local permanece sin cambios mientras se reproducen los anuncios.

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

1. Restaura la sesión del usuario cuando se reanuda la actividad del reproductor.

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
      >Solo se llama a este método con valores de hora local. Si se llama al método con los resultados de la hora actual, se produce un comportamiento incorrecto.

   * Para buscar la hora actual, utilice `seek`.

1. Cuando su aplicación reciba la `onStatusChanged` evento de cambio de estado, busque la hora local guardada.

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

1. Proporcione los saltos de anuncio según se especifican en la interfaz de la política de anuncios.
1. Implemente un selector de políticas de publicidad personalizado ampliando el selector de políticas de publicidad predeterminado.
1. Proporcione las pausas publicitarias que deben presentarse al usuario implementando `selectAdBreaksToPlay`.

   Este método incluye una pausa publicitaria pre-roll y las pausas publicitarias mid-roll antes de la posición horaria local. La aplicación puede decidir reproducir una pausa publicitaria pre-roll y reanudarla a la hora local especificada, reproducir una pausa publicitaria mid-roll y reanudarla a la hora local especificada o reproducir ninguna pausa publicitaria.
