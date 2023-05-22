---
description: TVSDK admite la búsqueda en una posición específica (tiempo) en la que el flujo es una lista de reproducción de ventana deslizante, en vídeo bajo demanda (VOD) y flujos en directo.
title: Mostrar una barra de desplazamiento de búsqueda con la posición de reproducción actual
exl-id: d5bc3a54-7dfd-435e-abb4-323639732e0a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Mostrar una barra de desplazamiento de búsqueda con la posición de reproducción actual {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición específica (tiempo) en la que el flujo es una lista de reproducción de ventana deslizante, en vídeo bajo demanda (VOD) y flujos en directo.

>[!TIP]
>
>La búsqueda en un flujo en vivo solo está permitida para DVR.

1. Configure las llamadas de retorno para la búsqueda.

   La búsqueda es asíncrona, por lo que TVSDK envía los siguientes eventos relacionados con la búsqueda:

   * `MediaPlayerEvent.SEEK_BEGIN`, donde comienza la búsqueda.
   * `MediaPlayerEvent.SEEK_END`, donde la búsqueda es exitosa.
   * `MediaPlayerEvent.OPERATION_FAILED`, donde la búsqueda ha fallado.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARED, COMPLETE, PAUSED y PLAYING.
1. Usar el nativo `SeekBar` para establecer `OnSeekBarChangeListener`, que determina cuándo el usuario está borrando.
1. Pase la posición de búsqueda solicitada (milisegundos) a `MediaPlayer.seek` método.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Solo puede buscar en la duración buscada del recurso. Para el vídeo bajo demanda, es decir, desde 0 hasta la duración del recurso.

   >[!TIP]
   >
   >Este paso mueve el cabezal de reproducción a una nueva posición en el flujo, pero la posición calculada final podría diferir de la posición de búsqueda especificada.

1. Escuchar para `MediaPlayerEvent.OPERATION_FAILED` y tome las medidas adecuadas.

   Este evento pasa la advertencia adecuada. La aplicación determina cómo proceder y las opciones incluyen volver a intentar la búsqueda o continuar la reproducción desde la posición anterior.

1. Espere a que TVSDK llame a `MediaPlayerEvent.SEEK_END` devolución de llamada.
1. Recupere la posición de reproducción ajustada final utilizando el parámetro de posición de la llamada de retorno.

   Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. Las reglas, incluido el comportamiento de reproducción, se ven afectadas si una búsqueda u otra reposición termina en mitad de una pausa publicitaria o omite las pausas publicitarias, y es posible que se apliquen.

1. Utilice la información de posición cuando se muestre una barra de desplazamiento de búsqueda.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Ejemplo de llamada**

En este ejemplo, el usuario borra la barra de búsqueda para buscar en la posición deseada.

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()), 
        playbackRange.getDuration()); 
     
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 
```
