---
description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-title: Implemente un avance rápido y rebobine
title: Implemente un avance rápido y rebobine
uuid: bd190534-c871-4673-b79d-1413277f480f
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96

---


# Implemente un avance rápido y rebobine {#implement-fast-forward-and-rewind}

Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

Para cambiar la velocidad, debe establecer un valor.

1. Pasar del modo de reproducción normal (1x) al modo de reproducción de trucos estableciendo la `rate` propiedad en el `MediaPlayer` a un valor permitido.

   * La `MediaPlayerItem` clase define las tasas de reproducción permitidas.
   * TVSDK selecciona la velocidad permitida más cercana si no se permite la velocidad especificada.

      Cuando se cambia la velocidad de reproducción de entradas de 0 (pausa) o 1 (reproducción normal) a una velocidad buena de 1 o menor que -1, se eliminan todas las publicidades de la línea de tiempo. Solo hay un período en toda la línea de tiempo que facilita una acción de reproducción de trucos para permitir que el contenido se reenvíe y rebobine rápidamente sin detenerse en ninguna posición del anuncio. Esta acción está habilitada por una acción de desprendimiento de línea de tiempo en TVSDK para eliminar todos los adBreaks resueltos. Cuando la reproducción de trucos se reanuda en 0 o 1, los adBreaks se restauran primero mediante la acción de datos adjuntos de la línea de tiempo.

      Recuerde la siguiente información:

   * Si la acción trickplay es rebobinar el contenido, la reproducción se reanuda cuando la velocidad se cambia a 1.
   * Si la acción de trickplay es acelerar el avance del contenido, el último adBreak omitido se reproduce en la posición de reanudación.
   Este ejemplo establece la velocidad de reproducción interna del reproductor en la velocidad solicitada.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. De forma opcional, puede escuchar los eventos de cambio de tasa, que le informan cuándo solicitó un cambio de tasa y cuándo se produce realmente un cambio de tasa.

   TVSDK distribuye los siguientes eventos relacionados con la reproducción mediante trucos:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` cuando el `rate` valor cambia a otro valor.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.
   TVSDK distribuye ambos eventos cuando el reproductor regresa del modo de reproducción mediante trucos al modo de reproducción normal.

## Elementos de API de cambio de tasa {#rate-change-api}

TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.

Utilice los siguientes elementos de API para cambiar las tasas de reproducción:

* `MediaPlayer.rate` propiedad con funciones setter y getter
* `MediaPlayer.localTime property` con función getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` propiedad con función getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` propiedad con función getter: especifica tasas válidas.

| Valor de tasa | Efecto en la reproducción |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | Cambia al modo de rebobinado rápido |
| 1.0 | Cambia al modo de reproducción normal (llamar `play` es lo mismo que establecer la propiedad rate en 1.0) |
| 0.0 | Pausas (llamar `pause` es lo mismo que establecer la propiedad rate en 0,0) |

## Limitaciones y comportamiento del juego de trucos {#limitations-behavior-trick-play}

Estas son las limitaciones para el modo de reproducción mediante trucos:

* La lista de reproducción maestra debe contener segmentos solo de marco I. En la pantalla solo se muestran los fotogramas clave de la pista I-frame.
* La pista de audio y los subtítulos cerrados están desactivados.
* La lógica de velocidad de bits adaptable (ABR) está deshabilitada. TVSDK selecciona una velocidad de bits entre la velocidad más baja proporcionada y 800 kbps y la utiliza durante toda la sesión de reproducción mediante trucos.
* La reproducción y la pausa están activadas.
* No se permite la búsqueda. Para buscar, llame `pause` a salir del modo de reproducción de trucos y luego llame a `seek`.

* Puede salir del modo de reproducción mediante trucos a cualquier velocidad de reproducción permitida (reproducir o pausar).
* Cuando se incorporan publicidades en el flujo:

   * Puede ir a jugar con trucos solo mientras reproduce el contenido principal. Se envía un error si intenta cambiar a la reproducción incorrecta durante una pausa publicitaria.
   * Después de comenzar el modo de reproducción de trucos, se omiten los saltos de publicidad y no se activa ningún evento de publicidad.
   * La línea de tiempo expuesta por TVSDK a la aplicación del reproductor no se modifica aunque se omitan los saltos de publicidad.
   * La `MediaPlayer.currentTime` propiedad salta hacia adelante (hacia adelante) o hacia atrás (en rebobinado rápido) con la duración de la pausa publicitaria omitida. Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante la reproducción mediante trucos. La aplicación del reproductor puede utilizar la `localTime` propiedad para rastrear el tiempo en relación únicamente con el contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir una publicidad.

   * El `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` evento se envía inmediatamente antes de que se omita una pausa publicitaria. El reproductor puede utilizar este evento para implementar la lógica personalizada relacionada con los saltos de publicidad omitidos.
   * Salir de la reproducción de trucos invoca la misma política de reproducción de anuncios que al salir de la búsqueda.

      Por lo tanto, al igual que en la búsqueda, el comportamiento depende de si la política de reproducción de la aplicación es diferente de la predeterminada. El valor predeterminado es que la última pausa publicitaria omitida se reproduce en el punto en el que se sale del juego sucio.