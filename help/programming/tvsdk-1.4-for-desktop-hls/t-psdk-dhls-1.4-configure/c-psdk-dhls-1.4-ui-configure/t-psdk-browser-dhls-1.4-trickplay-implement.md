---
description: Cuando los usuarios avanzan o rebobinan rápidamente a través de los medios, se encuentran en el modo de reproducción con trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
title: Implementar avance rápido y rebobinado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Implementar avance rápido y rebobinado {#implement-fast-forward-and-rewind}

Cuando los usuarios avanzan o rebobinan rápidamente a través de los medios, se encuentran en el modo de reproducción con trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

Para cambiar la velocidad, debe establecer un valor.

1. Cambie del modo de reproducción normal (1x) al modo de reproducción con trucos ajustando el `rate` propiedad en el `MediaPlayer` a un valor permitido.

   * El `MediaPlayerItem` define las velocidades de reproducción permitidas.
   * TVSDK selecciona la tasa permitida más cercana si la tasa especificada no está permitida.

     Cuando se cambia la velocidad de reproducción engañosa de 0 (pausa) o 1 (reproducción normal) a una velocidad mayor que 1 o menor que -1, se eliminan todos los anuncios de la cronología. Solo hay un punto en toda la cronología que facilita una acción de juego engañoso para permitir que el contenido se reenvíe y rebobine rápidamente sin detenerse en ninguna posición del anuncio. Esta acción se habilita mediante una acción de desprendimiento de escala de tiempo en TVSDK para eliminar todos los AdBreaks resueltos. Cuando el juego de trucos se reanuda en 0 o 1, la acción de adjunto de la cronología restaura primero los saltos de publicidad.

     Recuerde la siguiente información:

   * Si la acción de reproducción engañosa es rebobinar el contenido, la reproducción se reanuda cuando la velocidad se cambia a 1.
   * Si la acción de reproducción engañosa es avanzar rápidamente por el contenido, el último adBreak omitido se reproduce en la posición de reanudación.

   En este ejemplo se establece la velocidad de reproducción interna del reproductor en la velocidad solicitada.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Si lo desea, puede escuchar eventos de cambio de tarifa, que le permiten saber cuándo solicitó un cambio de tarifa y cuándo se produce realmente un cambio de tarifa.

   TVSDK envía los siguientes eventos relacionados con el juego de trucos:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` cuando la variable `rate` El valor cambia a un valor diferente.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

   TVSDK envía ambos eventos cuando el reproductor vuelve del modo de truco al modo de reproducción normal.

## Elementos de API de tasa de cambio {#rate-change-api}

TVSDK incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite el truco y otras funcionalidades relacionadas con el avance y el rebobinado rápidos.

Utilice los siguientes elementos de la API para cambiar las tasas de reproducción:

* `MediaPlayer.rate` propiedad con funciones de establecedor y captador
* `MediaPlayer.localTime property` con función de captador
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` propiedad con función de captador
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` propiedad con función de captador: especifica tasas válidas.

| Valor de tarifa | Efecto en la reproducción |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | Cambia al modo de rebobinado rápido |
| 1.0 | Cambia al modo de reproducción normal (llamando a `play` es lo mismo que establecer la propiedad tasa en 1,0) |
| 0.0 | Pausas (llamada a `pause` es lo mismo que establecer la propiedad tasa en 0,0) |

## Limitaciones y comportamiento para el juego de trucos {#limitations-behavior-trick-play}

Estas son las limitaciones del modo de juego con trucos:

* La lista de reproducción principal debe contener segmentos solo de I-frame. En la pantalla solo se muestran los fotogramas clave de la pista I-frame.
* La pista de audio y los subtítulos están desactivados.
* La lógica de velocidad de bits adaptable (ABR) está deshabilitada. TVSDK selecciona una velocidad de bits entre la velocidad más baja proporcionada y 800 kbps y utiliza esa velocidad durante toda la sesión de truco.
* La reproducción y la pausa están habilitadas.
* La búsqueda no está permitida. Para buscar, llame a `pause` para salir del modo de juego truco y luego llamar a `seek`.

* Puede salir del modo truco-reproducción a cualquier velocidad de reproducción permitida (reproducción o pausa).
* Cuando los anuncios se incorporan al flujo:

   * Solo puedes ir a la reproducción con trucos mientras reproduces el contenido principal. Se envía un error si intenta cambiar a la reproducción con trucos durante una pausa publicitaria.
   * Después de iniciar el modo de reproducción con trucos, las pausas publicitarias se ignoran y no se activa ningún evento publicitario.
   * La cronología expuesta por TVSDK a la aplicación del reproductor no se modifica aunque se omitan las pausas publicitarias.
   * El `MediaPlayer.currentTime` La propiedad salta hacia delante (en avance rápido) o hacia atrás (en rebobinado rápido) con la duración de la pausa publicitaria omitida. Este comportamiento de salto para el tiempo actual permite que la duración del flujo permanezca sin modificar durante el juego de trucos. La aplicación de reproducción puede utilizar el `localTime` para realizar un seguimiento del tiempo en relación únicamente con el contenido principal. No se realizan saltos de tiempo en los valores devueltos para la hora local al omitir un anuncio.

   * El `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` el evento se envía inmediatamente antes de que se vaya a omitir una pausa publicitaria. El reproductor puede utilizar este evento para implementar una lógica personalizada relacionada con los saltos de publicidad omitidos.
   * La salida del juego de trucos invoca la misma política de reproducción de anuncios que al salir de la búsqueda.

     Por lo tanto, como en la búsqueda, el comportamiento depende de si la directiva de reproducción de la aplicación es diferente de la predeterminada. De forma predeterminada, la última pausa publicitaria omitida se reproduce en el punto en el que sale de la reproducción con trucos.
