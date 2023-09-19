---
description: En el TVSDK del explorador, puede buscar una posición específica (tiempo) en un flujo. Un flujo puede ser una lista de reproducción de ventana deslizante o contenido de vídeo bajo demanda (VOD).
title: Controlar la búsqueda al utilizar la barra de búsqueda
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Controlar la búsqueda al utilizar la barra de búsqueda{#handle-seek-when-using-the-seek-bar}

En el TVSDK del explorador, puede buscar una posición específica (tiempo) en un flujo. Un flujo puede ser una lista de reproducción de ventana deslizante o contenido de vídeo bajo demanda (VOD).

>[!IMPORTANT]
>
>La búsqueda en un flujo en vivo solo está permitida para DVR.

1. Espere a que el TVSDK del explorador esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARED, COMPLETE, PAUSED y PLAYING. Tener un estado válido garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en un estado de búsqueda válido, al intentar llamar a los siguientes métodos se genera un `IllegalStateException`.

   Por ejemplo, puede esperar a que el TVSDK del explorador entre en déclencheur  `AdobePSDK.MediaPlayerStatusChangeEvent`  con un `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Pase la posición de búsqueda solicitada a `MediaPlayer.seek` como parámetro en milisegundos.

   Esto mueve el cabezal de reproducción a una posición diferente en el flujo.

   >[!TIP]
   >
   >La posición de búsqueda solicitada puede no coincidir con la posición calculada real.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Espere a que el TVSDK del explorador almacene en déclencheur el  `AdobePSDK.PSDKEventType.SEEK_END`  evento, que devuelve la posición ajustada en el `actualPosition` atributo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Esto es importante porque la posición de inicio real después de la búsqueda podría ser diferente de la posición solicitada. Algunas de las siguientes reglas pueden aplicarse:

   * El comportamiento de reproducción se ve afectado si una búsqueda, u otro cambio de posición, termina en mitad de una pausa publicitaria o omite las pausas publicitarias.
   * Solo puede buscar en la duración buscada del recurso. Para VOD, es decir, desde 0 hasta la duración del recurso.

1. Para la barra de búsqueda creada en el ejemplo anterior, escuche `setPositionChangeListener()` para ver cuándo está borrando el usuario:

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

1. Configure las llamadas de retorno del oyente de eventos para los cambios en la actividad de búsqueda del usuario.

       La operación de búsqueda es asíncrona, por lo que el TVSDK del explorador envía estos eventos relacionados con la búsqueda:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` para indicar que la llamada a otro punto del contenido comienza.
   * `AdobePSDK.PSDKEventType.SEEK_END` para indicar que la búsqueda se ha realizado correctamente.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` para indicar que el reproductor de contenido ha reajustado la posición de búsqueda proporcionada por el usuario.
