---
description: TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, en vídeo a petición (VOD) y en flujos en directo.
seo-description: TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, en vídeo a petición (VOD) y en flujos en directo.
seo-title: Mostrar una barra de búsqueda con la posición de reproducción actual
title: Mostrar una barra de búsqueda con la posición de reproducción actual
uuid: 30a9237c-bbd5-457e-a93c-662570711986
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Mostrar una barra de búsqueda con la posición de reproducción actual {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK admite la búsqueda en una posición (hora) específica en la que el flujo es una lista de reproducción de ventana deslizante, en vídeo a petición (VOD) y en flujos en directo.

>[!TIP]
>
>La búsqueda en un flujo en directo solo está permitida para DVR.

1. Configure las rellamadas para la búsqueda.

   La búsqueda es asincrónica, por lo que TVSDK distribuye los siguientes eventos relacionados con la búsqueda:

   * `MediaPlayerEvent.SEEK_BEGIN`, donde los inicios de búsqueda.
   * `MediaPlayerEvent.SEEK_END`, donde la búsqueda se realiza correctamente.
   * `MediaPlayerEvent.OPERATION_FAILED`, donde la búsqueda ha fallado.

1. Espere a que el reproductor esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARADO, COMPLETO, PAUSADO y REPRODUCIENDO.
1. Utilice el `SeekBar` nativo para establecer `OnSeekBarChangeListener`, que determina cuándo se está depurando el usuario.
1. Pase la posición de búsqueda solicitada (milisegundos) al método `MediaPlayer.seek`.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Solo puede buscar en la duración de búsqueda del recurso. Para vídeo a petición, es decir, desde 0 hasta la duración del recurso.

   >[!TIP]
   >
   >Este paso mueve el cursor de reproducción a una nueva posición en el flujo, pero la posición calculada final puede diferir de la posición de búsqueda especificada.

1. Escuche `MediaPlayerEvent.OPERATION_FAILED` y realice las acciones correspondientes.

   Este evento pasa la advertencia adecuada. La aplicación determina cómo continuar y las opciones incluyen probar la búsqueda de nuevo o continuar la reproducción desde la posición anterior.

1. Espere a que TVSDK llame a la llamada de retorno `MediaPlayerEvent.SEEK_END`.
1. Recupere la posición de reproducción ajustada final utilizando el parámetro de posición de la llamada de retorno.

   Esto es importante porque la posición de inicio real después de la búsqueda puede ser diferente de la posición solicitada. Las reglas, incluido el comportamiento de reproducción, se ven afectadas si una búsqueda u otro cambio de posición termina en medio de una pausa publicitaria o omite los saltos publicitarios, podrían aplicarse.

1. Utilice la información de posición al mostrar una barra de búsqueda.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Ejemplo de búsqueda**

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
