---
description: Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.
title: Mostrar la duración, la hora actual y el tiempo restante del vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Mostrar la duración, la hora actual y el tiempo restante del vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre los medios que puede mostrar en la barra de búsqueda.

1. Espere a que el reproductor esté en el estado PREPARADO.
1. Recupere el tiempo actual del cabezal de reproducción mediante el método `MediaPlayer.getCurrentTime`.

   Esto devuelve la posición actual del cabezal de reproducción en la cronología virtual en milisegundos. El tiempo se calcula en función del flujo resuelto que puede contener varias instancias de contenido alternativo, como varios anuncios o pausas publicitarias duplicados en el flujo principal. Para los flujos en directo/lineales, el tiempo devuelto siempre está en el intervalo de la ventana de reproducción.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recupere el intervalo de reproducción de la emisión y determine la duración.
   1. Utilice el método `mediaPlayer.getPlaybackRange` para obtener el intervalo de tiempo de la cronología virtual.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analice el intervalo de tiempo con `mediacore.utils.TimeRange`.
   1. Para determinar la duración, reste el inicio desde el final del intervalo.

      Esto incluye la duración del contenido adicional que se inserta en la emisión (anuncios).

      Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y las duraciones del contenido adicional que se inserta en la emisión (anuncios).

      Para un recurso lineal/activo, el rango representa el intervalo de la ventana de reproducción y este intervalo cambia durante la reproducción.

      TVSDK llama a su llamada de retorno `onUpdated` para indicar que el elemento multimedia se ha actualizado y que sus atributos (incluido el intervalo de reproducción) se han actualizado.

1. Utilice los métodos disponibles en las clases `MediaPlayer` y `SeekBar` que están disponibles públicamente en el SDK para Android para configurar los parámetros de la barra de búsqueda.

   Por ejemplo, este es un posible diseño que contiene los elementos `SeekBar` y dos `TextView`.

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

   El siguiente ejemplo utiliza la clase de ayuda `Clock.java` como temporizador, que está disponible en el reproductor de referencia PrimetimeReference. Esta clase establece un detector de eventos y déclencheur un evento `onTick` cada segundo u otro valor de tiempo de espera que pueda especificar.

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

   En cada visto del reloj, este ejemplo recupera la posición actual del reproductor de medios y actualiza SeekBar. Utiliza los dos elementos TextView para marcar la hora actual y la posición final del intervalo de reproducción como valores numéricos.

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

