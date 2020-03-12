---
description: TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo a petición (VOD) como en flujos en directo.
seo-description: TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo a petición (VOD) como en flujos en directo.
seo-title: Mostrar una barra de búsqueda con la posición de reproducción actual
title: Mostrar una barra de búsqueda con la posición de reproducción actual
uuid: a9f4dd6c-78cf-455c-8c31-b2f7b740d84a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Mostrar una barra de búsqueda con la posición de reproducción actual {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, tanto en vídeo a petición (VOD) como en flujos en directo.

>[!IMPORTANT]
>
>La búsqueda en un flujo en directo solo está permitida para DVR.

1. Configure las rellamadas para la búsqueda.

       La búsqueda es asincrónica, por lo que TVSDK distribuye los siguientes eventos relacionados con la búsqueda:
   
   * `QOSEventListener.onSeekStart` - Buscar inicio.
   * `QOSEventListener.onSeekComplete` - Busque con éxito.
   * `QOSEventListener.onOperationFailed` - Error en la búsqueda.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos están PREPARADOS, COMPLETADOS, PAUSADOS y REPRODUCIDOS.

1. Utilice la SeekBar nativa para establecer `OnSeekBarChangeListener` cuándo el usuario está borrando.
1. Escuche `QOSEventListener.onOperationFailed` y tome las medidas apropiadas.

   Este evento pasa la advertencia adecuada. La aplicación determina cómo continuar, por ejemplo, probando la búsqueda de nuevo o continuando la reproducción desde la posición anterior.

1. Espere a que TVSDK llame a la `QOSEventListener.onSeekComplete` llamada de retorno.
1. Recupere la posición de reproducción ajustada final utilizando el parámetro de posición de la llamada de retorno.

   Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. El comportamiento de reproducción puede verse afectado si una búsqueda u otro cambio de posición termina en medio de una pausa publicitaria o omite los saltos publicitarios.

1. Utilice la información de posición al mostrar una barra de búsqueda.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Ejemplo de búsqueda**

En este ejemplo, el usuario elimina la barra de búsqueda para buscar la posición deseada.

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

