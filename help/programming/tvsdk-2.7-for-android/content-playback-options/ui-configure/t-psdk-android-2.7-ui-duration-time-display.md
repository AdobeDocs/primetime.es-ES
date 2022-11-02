---
description: Puede utilizar TVSDK para recuperar información sobre la posición del reproductor en el contenido y mostrarla en la barra de búsqueda.
title: Mostrar la duración, la hora actual y el tiempo restante del vídeo
exl-id: d9832f19-c2d1-413a-b094-091052912c96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Mostrar la duración, la hora actual y el tiempo restante del vídeo {#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre la posición del reproductor en el contenido y mostrarla en la barra de búsqueda.

1. Espere a que el reproductor esté en al menos el estado PREPARADO.
1. Recupere el tiempo actual del cabezal de reproducción utilizando la variable `MediaPlayer.getCurrentTime` método.

   Esto devuelve la posición actual del cabezal de reproducción en la cronología virtual en milisegundos. El tiempo se calcula en función del flujo resuelto que puede contener varias instancias de contenido alternativo, como varios anuncios o pausas publicitarias duplicados en el flujo principal. Para los flujos en directo/lineales, el tiempo devuelto siempre está en el intervalo de la ventana de reproducción.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. Recupere el intervalo de reproducción de la emisión y determine la duración.
   1. Utilice la variable `MediaPlayer.getPlaybackRange` para obtener el intervalo de tiempo de la cronología virtual.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. Utilice la variable `MediaPlayer.getPlaybackRange` para obtener el intervalo de tiempo de la cronología virtual.

      * Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y las duraciones del contenido adicional en la emisión (anuncios).
      * Para un recurso lineal/activo, el rango representa el intervalo de ventana de reproducción. Este intervalo cambia durante la reproducción.

         TVSDK llama a la función `ITEM_Updated` llamada de retorno para indicar que el elemento multimedia se actualizó y que sus atributos, incluido el intervalo de reproducción, se actualizaron.

1. Utilice los métodos disponibles en `MediaPlayer` y `SeekBar` en el SDK de Android para configurar los parámetros de la barra de búsqueda.

   Por ejemplo, este es un posible diseño que contiene la barra de búsqueda y dos `TextView` elementos.

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

1. Utilice un temporizador para recuperar periódicamente la hora actual y actualizar la barra de búsqueda, como se muestra en la figura:

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   El ejemplo siguiente utiliza la variable `Clock.java` clase helper, que está disponible en `ReferencePlayer`, como temporizador. Esta clase define un detector de eventos y déclencheur de `onTick` cada segundo, u otro valor de tiempo de espera que pueda especificar.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           // Timer event is received. Update the seek bar here. 
       } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   En cada visto del reloj, este ejemplo recupera la posición actual del reproductor de medios y actualiza la barra de búsqueda. Utiliza los dos `TextView` para marcar la hora actual y la posición final del intervalo de reproducción como valores numéricos.

   ```java
   @Override 
   public void onTick(String name) { 
       if (mediaPlayer != null &&  
         mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
           handler.post(new Runnable() { 
               @Override 
               public void run() { 
                   seekBar.setProgress((int) mediaPlayer.getCurrentTime()); 
                   currentTimeText.setText(timeStampToText(mediaPlayer.getCurrentTime())); 
                   totalTimeText.setText(timeStampToText(mediaPlayer.getPlaybackRange().getEnd())); 
               } 
           }); 
       } 
   } 
   ```
