---
description: TVSDK admite la búsqueda en una posición específica (tiempo) en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo bajo demanda (VOD) como en flujos en directo.
title: Mostrar una barra de desplazamiento de búsqueda con la posición de reproducción actual
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Mostrar una barra de desplazamiento de búsqueda con la posición de reproducción actual {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición específica (tiempo) en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo bajo demanda (VOD) como en flujos en directo.

>[!IMPORTANT]
>
>La búsqueda en un flujo en vivo solo está permitida para DVR.

1. Configure las llamadas de retorno para la búsqueda.

       La búsqueda es asíncrona, por lo que TVSDK envía los siguientes eventos relacionados con la búsqueda:
   
   * `QOSEventListener.onSeekStart` - Busca empezar.
   * `QOSEventListener.onSeekComplete` - Búsqueda correcta.
   * `QOSEventListener.onOperationFailed` - Error de búsqueda.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARED, COMPLETE, PAUSED y PLAYING.

1. Utilice el SeekBar nativo para establecer `OnSeekBarChangeListener` para ver cuándo está borrando el usuario.
1. Escuchar para `QOSEventListener.onOperationFailed` y tome las medidas adecuadas.

   Este evento pasa la advertencia adecuada. La aplicación determina cómo proceder, por ejemplo, intentando la búsqueda de nuevo o continuando la reproducción desde la posición anterior.

1. Espere a que TVSDK llame a `QOSEventListener.onSeekComplete` devolución de llamada.
1. Recupere la posición de reproducción ajustada final utilizando el parámetro de posición de la llamada de retorno.

   Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. El comportamiento de reproducción puede verse afectado si una búsqueda u otra reposición termina en mitad de una pausa publicitaria o omite las pausas publicitarias.

1. Utilice la información de posición cuando se muestre una barra de desplazamiento de búsqueda.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Ejemplo de llamada**

En este ejemplo, el usuario borra la barra de búsqueda para buscar en la posición deseada.

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
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
