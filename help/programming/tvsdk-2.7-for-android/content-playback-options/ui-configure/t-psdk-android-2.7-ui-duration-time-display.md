---
description: Puede utilizar TVSDK para recuperar información sobre la posición del reproductor en el contenido y mostrarla en la barra de búsqueda.
title: Mostrar la duración, el tiempo actual y el tiempo restante del vídeo
exl-id: d9832f19-c2d1-413a-b094-091052912c96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Mostrar la duración, el tiempo actual y el tiempo restante del vídeo {#display-the-duration-current-time-and-remaining-time-of-the-video}

Puede utilizar TVSDK para recuperar información sobre la posición del reproductor en el contenido y mostrarla en la barra de búsqueda.

1. Espere a que el reproductor esté al menos en estado PREPARADO.
1. Recupere el tiempo del cabezal de reproducción actual utilizando `MediaPlayer.getCurrentTime` método.

   Devuelve la posición actual del cabezal de reproducción en la cronología virtual en milisegundos. El tiempo se calcula en relación con el flujo resuelto que puede contener varias instancias de contenido alternativo, como varios anuncios o pausas publicitarias empalmadas en el flujo principal. Para los flujos en directo/lineales, el tiempo devuelto siempre está en el intervalo de la ventana de reproducción.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. Recupere el rango de reproducción de la emisión y determine la duración.
   1. Utilice el `MediaPlayer.getPlaybackRange` método para obtener el intervalo de tiempo de la escala de tiempo virtual.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. Utilice el `MediaPlayer.getPlaybackRange` método para obtener el intervalo de tiempo de la escala de tiempo virtual.

      * Para VOD, el intervalo siempre comienza con cero y el valor final es igual a la suma de la duración del contenido principal y las duraciones del contenido adicional en el flujo (anuncios).
      * Para un recurso lineal/activo, el rango representa el rango de la ventana de reproducción. Este rango cambia durante la reproducción.

         TVSDK llama a `ITEM_Updated` llamada de retorno para indicar que el elemento de medios se actualizó y que sus atributos, incluido el intervalo de reproducción, se actualizaron.

1. Utilice los métodos disponibles en `MediaPlayer` y en el `SeekBar` en el SDK para Android para configurar los parámetros de la barra de búsqueda.

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

   El ejemplo siguiente utiliza el `Clock.java` clase de ayuda, que está disponible en `ReferencePlayer`, como temporizador. Esta clase establece un detector de eventos y déclencheur un `onTick` evento cada segundo u otro valor de tiempo de espera que pueda especificar.

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

   En cada marca de reloj, este ejemplo recupera la posición actual del reproductor de contenido y actualiza la barra de búsqueda. Utiliza los dos `TextView` elementos para marcar el tiempo actual y la posición final del intervalo de reproducción como valores numéricos.

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
