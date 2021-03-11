---
description: Cuando los usuarios avancen o rebobinen rápidamente a través de los medios, se encuentran en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción engañosa, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
title: Implemente hacia adelante y rebobine rápidamente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# Implemente hacia adelante y rebobine rápidamente {#implement-fast-forward-and-rewind}

Cuando los usuarios avancen o rebobinen rápidamente a través de los medios, se encuentran en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción engañosa, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

Para cambiar la velocidad, debe establecer un valor.

1. Para pasar del modo de reproducción normal (1x) al modo de reproducción de trucos, establezca la propiedad `rate` en `MediaPlayer` en un valor permitido.

   * La clase `MediaPlayerItem` define las tasas de reproducción permitidas.
   * TVSDK selecciona la tasa permitida más cercana si no se permite la velocidad especificada.

      Cuando la velocidad de reproducción de trucos cambia de 0 (pausa) o 1 (reproducción normal) a una velocidad buena a 1 o menor que -1, se eliminan todos los anuncios de la cronología. Solo hay un punto en toda la cronología que facilita una acción de reproducción de trucos para permitir que el contenido se reenvíe y rebobine rápidamente sin detenerse en ninguna posición del anuncio. Esta acción está habilitada por una acción de desconexión de línea de tiempo en TVSDK para eliminar todos los adBreaks resueltos. Cuando la reproducción de trucos se reanuda en 0 o 1, las pausas publicitarias se restauran primero mediante la acción de adjunto de la cronología.

      Recuerde la siguiente información:

   * Si la acción de reproducción de trucos consiste en rebobinar el contenido, la reproducción se reanuda cuando la velocidad se cambia a 1.
   * Si la acción de reproducción de trucos es acelerar el avance del contenido, el último adBreak omitido se reproduce en la posición de reanudación.

   En este ejemplo se establece la velocidad de reproducción interna del reproductor en la velocidad solicitada.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Si lo desea, puede escuchar eventos de cambio de tasa, que le permiten saber cuándo solicitó un cambio de tasa y cuándo se produjo realmente un cambio de tasa.

   TVSDK distribuye los siguientes eventos relacionados con la reproducción trucada:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` cuando el  `rate` valor cambia a otro valor.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

   TVSDK envía ambos eventos cuando el reproductor vuelve del modo de reproducción trucada al modo de reproducción normal.

## Elementos de API de cambio de tasa {#rate-change-api}

TVSDK incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con la redirección y el avance rápidos.

Utilice los siguientes elementos de API para cambiar las tasas de reproducción:

* `MediaPlayer.rate` propiedad con funciones setter y getter
* `MediaPlayer.localTime property` con la función getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` propiedad con función getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` propiedad con función getter : especifica tasas válidas.

| Valor de tasa | Efectos en la reproducción |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2,0, -4,0, -8,0, -16,0, -32,0, -64,0 y -128,0 | Cambia al modo de rebobinado rápido |
| 1,0 | Cambia al modo de reproducción normal (llamar a `play` es lo mismo que establecer la propiedad rate en 1.0) |
| 0,0 | Pausas (llamar a `pause` es lo mismo que establecer la propiedad rate en 0,0) |

## Limitaciones y comportamiento para la reproducción de trucos {#limitations-behavior-trick-play}

Estas son las limitaciones del modo de reproducción de trucos:

* La lista de reproducción maestra debe contener segmentos solo de marco I. En la pantalla solo se muestran los fotogramas clave de la pista de I-frame.
* La pista de audio y los subtítulos están desactivados.
* La lógica de velocidad de bits adaptable (ABR) está desactivada. TVSDK selecciona una velocidad de bits entre la velocidad más baja proporcionada y 800 kbps y la utiliza durante toda la sesión de reproducción asistida.
* La reproducción y la pausa están activadas.
* No se permite la llamada a otro punto del contenido. Para buscar, llame a `pause` para salir del modo de reproducción de trucos y luego llame a `seek`.

* Puede salir del modo de reproducción mediante trucos a cualquier velocidad de reproducción permitida (reproducción o pausa).
* Cuando los anuncios se incorporan al flujo:

   * Puede ir a la reproducción trucada solo mientras reproduce el contenido principal. Se envía un error si intenta cambiar para engañar la reproducción durante una pausa publicitaria.
   * Después de iniciar el modo de reproducción de truco, se omiten las pausas publicitarias y no se activan eventos publicitarios.
   * La línea de tiempo expuesta por TVSDK a la aplicación del reproductor no se modifica aunque se omitan las pausas publicitarias.
   * La propiedad `MediaPlayer.currentTime` salta hacia adelante (en avance rápido) o hacia atrás (en rebobinado rápido) con la duración de la pausa publicitaria omitida. Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante la reproducción de trucos. La aplicación del reproductor puede utilizar la propiedad `localTime` para rastrear el tiempo relativo solo al contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir un anuncio.

   * El evento `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` se envía inmediatamente antes de que se omita una pausa publicitaria. El reproductor puede utilizar este evento para implementar lógica personalizada relacionada con las pausas publicitarias omitidas.
   * Salir de la reproducción de trucos invoca la misma política de reproducción de anuncios que al salir de la llamada a otro punto del contenido.

      Por lo tanto, como en la búsqueda, el comportamiento depende de si la política de reproducción de la aplicación es diferente de la predeterminada. El valor predeterminado es que la última pausa publicitaria omitida se reproduce en el punto en el que sale de la reproducción engañosa.