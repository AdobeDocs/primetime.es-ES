---
description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
seo-description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
seo-title: Mostrar la duración, el tiempo actual y el tiempo restante del vídeo
title: Mostrar la duración, el tiempo actual y el tiempo restante del vídeo
uuid: afb43169-2d82-4137-ba38-27caef3d8c21
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Mostrar la duración, el tiempo actual y el tiempo restante del vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.

1. Espere a que el reproductor esté en el estado PREPARADO.
1. Recupere el tiempo actual del cursor de reproducción mediante el `MediaPlayer.getCurrentTime` método .

   Esto devuelve la posición actual del cursor de reproducción en la línea de tiempo virtual en milisegundos. El tiempo se calcula en relación con el flujo resuelto que puede contener varias instancias de contenido alternativo, como anuncios múltiples o pausas publicitarias que se dividen en el flujo principal. Para flujos en directo/lineal, el tiempo devuelto siempre está en el rango de la ventana de reproducción.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recupere el rango de reproducción del flujo y determine la duración.
   1. Utilice el `mediaPlayer.getPlaybackRange` método para obtener el intervalo de tiempo de la línea de tiempo virtual.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analice el intervalo de tiempo usando `mediacore.utils.TimeRange`.
   1. Para determinar la duración, reste el inicio desde el final del rango.

      Esto incluye la duración del contenido adicional que se inserta en el flujo (anuncios).

      Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y la duración del contenido adicional que se inserta en el flujo (anuncios).

      Para un recurso lineal/activo, el rango representa el rango de la ventana de reproducción y este rango cambia durante la reproducción.

      TVSDK llama a la `onUpdated` llamada de retorno para indicar que se actualizó el elemento de medios y que se actualizaron sus atributos (incluido el intervalo de reproducción).

1. Utilice los métodos disponibles en la `MediaPlayer` clase y la `SeekBar` clase que están públicamente disponibles en el SDK para Android para configurar los parámetros de la barra de búsqueda.

   Por ejemplo, aquí se muestra un diseño posible que contiene los `SeekBar` y dos `TextView` elementos.

   ```xml
   <LinearLayout 
    android:id="@+id/controlBarLayout" 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:layout_alignParentBottom="true" 
    android:background="@android:color/black" 
    android:orientation="horizontal" > 
    <TextView 
       android:id="@+id/playerCurrentTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
    <SeekBar 
       android:id="@+id/playerSeekBar" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_weight="1" /> 
    <TextView 
       android:id="@+id/playerTotalTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
   </LinearLayout>
   ```

1. Utilice un temporizador para recuperar periódicamente la hora actual y actualizar SeekBar.

   El ejemplo siguiente utiliza la clase `Clock.java` auxiliar como temporizador, que está disponible en el reproductor de referencia PrimetimeReference. Esta clase establece un detector de eventos y activa un `onTick` evento cada segundo, o bien, otro valor de tiempo de espera que se pueda especificar.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
   @Override 
   public void onTick(String name) { 
       // Timer event is received. Update the SeekBar here. 
   } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   En cada marca de reloj, este ejemplo recupera la posición actual del reproductor de medios y actualiza SeekBar. Utiliza los dos elementos TextView para marcar el tiempo actual y la posición final del intervalo de reproducción como valores numéricos.

   ```java
   @Override 
   public void onTick(String name) { 
   if (mediaPlayer != null && mediaPlayer.getStatus() == PlayerState.PLAYING) { 
       handler.post(new Runnable() { 
           @Override 
           public void run() { 
               seekBar.setProgress((int)  
                    mediaPlayer.getCurrentTime()); 
               currentTimeText.setText(timeStampToText( 
                  mediaPlayer.getCurrentTime())); 
               totalTimeText.setText(timeStampToText( 
                   mediaPlayer.getPlaybackRange().getEnd())); 
           } 
       }); 
   } 
   }
   ```

