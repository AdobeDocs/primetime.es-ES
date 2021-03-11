---
description: TVSDK admite la búsqueda en una posición específica (hora) en la que el flujo es una lista de reproducción de ventana deslizante, en vídeo bajo demanda (VOD) y emisiones en directo.
title: Mostrar una barra de desplazamiento con la posición de reproducción actual
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Mostrar una barra de depuración con la posición de reproducción actual {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición específica (hora) en la que el flujo es una lista de reproducción de ventana deslizante, en vídeo bajo demanda (VOD) y emisiones en directo.

>[!TIP]
>
>La llamada a otro sitio en directo solo está permitida para DVR.

1. Configure las llamadas de retorno para la búsqueda.

   La llamada a otro punto del contenido es asíncrona, por lo que TVSDK envía los siguientes eventos relacionados con la búsqueda:

   * `MediaPlayerEvent.SEEK_BEGIN`, donde comienza la búsqueda.
   * `MediaPlayerEvent.SEEK_END`, donde la búsqueda se realiza correctamente.
   * `MediaPlayerEvent.OPERATION_FAILED`, donde la búsqueda ha fallado.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARADO, COMPLETO, PAUSADO y REPRODUCIENDO.
1. Utilice el `SeekBar` nativo para establecer `OnSeekBarChangeListener`, que determina cuándo se está borrando el usuario.
1. Pase la posición de búsqueda solicitada (milisegundos) al método `MediaPlayer.seek` .

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Solo puede buscar en la duración en la que puede buscar el recurso. Para vídeo bajo demanda, es decir, de 0 a la duración del recurso.

   >[!TIP]
   >
   >Este paso mueve el cabezal de reproducción a una nueva posición en el flujo, pero la posición calculada final puede diferir de la posición de búsqueda especificada.

1. Escuche `MediaPlayerEvent.OPERATION_FAILED` y realice las acciones adecuadas.

   Este evento pasa la advertencia adecuada. La aplicación determina cómo continuar y las opciones incluyen volver a intentar la llamada a otro punto del contenido o continuar la reproducción desde la posición anterior.

1. Espere a que TVSDK llame a la rellamada `MediaPlayerEvent.SEEK_END` .
1. Recupere la posición de reproducción ajustada final utilizando el parámetro de posición de la rellamada.

   Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. Las reglas, incluido el comportamiento de reproducción, se ven afectadas si una búsqueda u otro cambio de posición termina en mitad de una pausa publicitaria o omite las pausas publicitarias, pueden aplicarse.

1. Utilice la información de posición para mostrar una barra de desplazamiento.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Ejemplo de llamada a otro punto del contenido**

En este ejemplo, el usuario elimina la barra de búsqueda para buscar la posición deseada.

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
