---
description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
title: Mostrar la duración, el tiempo actual y el tiempo restante del vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Mostrar la duración, el tiempo actual y el tiempo restante del vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.

1. Espere a que su reproductor esté en estado PREPARADO.
1. Recupere el tiempo del cabezal de reproducción actual utilizando `MediaPlayer.getCurrentTime` método.

   Devuelve la posición actual del cabezal de reproducción en la cronología virtual en milisegundos. El tiempo se calcula en relación con el flujo resuelto que puede contener varias instancias de contenido alternativo, como varios anuncios o pausas publicitarias empalmadas en el flujo principal. Para los flujos en directo/lineales, el tiempo devuelto siempre está en el intervalo de la ventana de reproducción.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recupere el rango de reproducción de la emisión y determine la duración.
   1. Utilice el `mediaPlayer.getPlaybackRange` método para obtener el intervalo de tiempo de la escala de tiempo virtual.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analice el intervalo de tiempo mediante `mediacore.utils.TimeRange`.
   1. Para determinar la duración, reste el inicio desde el final del intervalo.

      Esto incluye la duración del contenido adicional que se inserta en el flujo (anuncios).

      Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y las duraciones del contenido adicional que se inserta en el flujo (anuncios).

      Para un recurso lineal/activo, el rango representa el intervalo de la ventana de reproducción y este intervalo cambia durante la reproducción.

      TVSDK llama a su `onUpdated` llamada de retorno para indicar que el elemento de medios se actualizó y que sus atributos (incluido el intervalo de reproducción) se actualizaron.

1. Utilice los métodos disponibles en la `MediaPlayer` y el `SeekBar` que está disponible públicamente en el SDK de Android para configurar los parámetros de la barra de búsqueda.

   Por ejemplo, este es un posible diseño que contiene la variable `SeekBar` y dos `TextView` elementos.

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

   El ejemplo siguiente utiliza el `Clock.java` como temporizador, que está disponible en el reproductor de referencia PrimetimeReference. Esta clase establece un detector de eventos y déclencheur un `onTick` evento cada segundo u otro valor de tiempo de espera que pueda especificar.

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

   En cada marca de reloj, este ejemplo recupera la posición actual del reproductor de contenido y actualiza SeekBar. Utiliza los dos elementos TextView para marcar el tiempo actual y la posición final del intervalo de reproducción como valores numéricos.

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
