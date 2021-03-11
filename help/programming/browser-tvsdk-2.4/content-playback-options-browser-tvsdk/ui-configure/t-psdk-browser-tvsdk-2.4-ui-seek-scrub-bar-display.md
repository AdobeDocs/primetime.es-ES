---
description: En el SDK del explorador, puede buscar una posición específica (hora) en un flujo. Un flujo puede ser una lista de reproducción de ventana deslizante o contenido de vídeo bajo demanda (VOD).
title: Administrar la búsqueda al utilizar la barra de búsqueda
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Administrar la búsqueda al utilizar la barra de búsqueda{#handle-seek-when-using-the-seek-bar}

En el SDK del explorador, puede buscar una posición específica (hora) en un flujo. Un flujo puede ser una lista de reproducción de ventana deslizante o contenido de vídeo bajo demanda (VOD).

>[!IMPORTANT]
>
>La llamada a otro sitio en directo solo está permitida para DVR.

1. Espere a que el TVSDK del explorador esté en un estado válido para la búsqueda.

   Los estados válidos son PREPARADO, COMPLETO, PAUSADO y REPRODUCIENDO. Estar en un estado válido garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en un estado de búsqueda válido, al intentar llamar a los siguientes métodos se genera un `IllegalStateException`.

   Por ejemplo, puede esperar a que el TVSDK del explorador almacene en déclencheur `AdobePSDK.MediaPlayerStatusChangeEvent` con un `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Pase la posición de búsqueda solicitada al método `MediaPlayer.seek` como parámetro en milisegundos.

   Esto mueve el cabezal de reproducción a una posición diferente en el flujo.

   >[!TIP]
   >
   >Es posible que el puesto solicitado no coincida con el puesto calculado real.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Espere a que el TVSDK del explorador almacene en déclencheur el evento `AdobePSDK.PSDKEventType.SEEK_END` , que devuelve la posición ajustada en el atributo `actualPosition` del evento:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Esto es importante porque la posición de inicio real después de la búsqueda podría ser diferente de la posición solicitada. Pueden aplicarse algunas de las siguientes reglas:

   * El comportamiento de reproducción se ve afectado si una búsqueda, u otro cambio de posición, termina en medio de una pausa publicitaria o omite las pausas publicitarias.
   * Solo puede buscar en la duración en la que puede buscar el recurso. Para VOD, es decir, de 0 a la duración del recurso.

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

1. Configure llamadas de retorno de oyentes de eventos para cambios en la actividad de búsqueda del usuario.

       La operación de búsqueda es asíncrona, por lo que el SDK de TVSDK del explorador distribuye estos eventos relacionados con la búsqueda:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` para indicar que la búsqueda se está iniciando.
   * `AdobePSDK.PSDKEventType.SEEK_END` para indicar que la búsqueda se realizó correctamente.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` para indicar que el reproductor de contenidos ha reajustado la posición de búsqueda proporcionada por el usuario.

