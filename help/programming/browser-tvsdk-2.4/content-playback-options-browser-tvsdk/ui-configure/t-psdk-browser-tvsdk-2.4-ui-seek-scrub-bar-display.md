---
description: En el TVSDK del explorador, puede buscar una posición específica (tiempo) en un flujo. Un flujo puede ser una lista de reproducción de ventana deslizante o contenido de vídeo a petición (VOD).
seo-description: En el TVSDK del explorador, puede buscar una posición específica (tiempo) en un flujo. Un flujo puede ser una lista de reproducción de ventana deslizante o contenido de vídeo a petición (VOD).
seo-title: Administrar la búsqueda al utilizar la barra de búsqueda
title: Administrar la búsqueda al utilizar la barra de búsqueda
uuid: a7c74141-581f-40a3-9d28-ce56ba56773c
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Administrar la búsqueda al usar la barra de búsqueda{#handle-seek-when-using-the-seek-bar}

En el TVSDK del explorador, puede buscar una posición específica (tiempo) en un flujo. Un flujo puede ser una lista de reproducción de ventana deslizante o contenido de vídeo a petición (VOD).

>[!IMPORTANT]
>
>La búsqueda en un flujo en directo solo está permitida para DVR.

1. Espere a que el TVSDK del explorador esté en un estado válido para la búsqueda.

   Los estados válidos están PREPARADOS, COMPLETADOS, PAUSADOS y REPRODUCIDOS. Estar en un estado válido garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en un estado de búsqueda válido, al intentar llamar a los siguientes métodos se genera un `IllegalStateException`.

   Por ejemplo, puede esperar a que el TVSDK del explorador active `AdobePSDK.MediaPlayerStatusChangeEvent` con un `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Pase la posición de búsqueda solicitada al método `MediaPlayer.seek` como parámetro en milisegundos.

   Esto mueve el cursor de reproducción a una posición diferente en el flujo.

   >[!TIP]
   >
   >La posición de búsqueda solicitada podría no coincidir con la posición real calculada.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Espere a que TVSDK del explorador active el evento `AdobePSDK.PSDKEventType.SEEK_END`, que devuelve la posición ajustada en el atributo `actualPosition` del evento:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Esto es importante porque la posición de inicio real después de la búsqueda podría ser diferente de la posición solicitada. Pueden aplicarse algunas de las siguientes reglas:

   * El comportamiento de reproducción se ve afectado si una búsqueda, u otro cambio de posición, termina en medio de una pausa publicitaria o omite los saltos publicitarios.
   * Solo puede buscar en la duración de búsqueda del recurso. Para VOD, es decir, desde 0 hasta la duración del recurso.

1. Para la barra de búsqueda que se creó en el ejemplo anterior, escuche `setPositionChangeListener()` para ver cuándo el usuario está borrando:

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
   
                       console.log("seek to " + time + " / " + duration); 
                   } 
   
               }); 
   ```

1. Configure las llamadas de retorno de oyentes de evento para los cambios en la actividad de búsqueda del usuario.

       La operación de búsqueda es asincrónica, por lo que el SDK de TVSDK del explorador distribuye estos eventos relacionados con la búsqueda:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` para indicar que la búsqueda está empezando.
   * `AdobePSDK.PSDKEventType.SEEK_END` para indicar que la búsqueda se realizó correctamente.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` para indicar que el reproductor de medios ha reajustado la posición de búsqueda proporcionada por el usuario.

