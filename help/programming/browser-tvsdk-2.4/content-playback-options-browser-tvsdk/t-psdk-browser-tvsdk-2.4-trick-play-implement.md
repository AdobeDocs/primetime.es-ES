---
description: Cuando los usuarios avancen o rebobinen rápidamente a través de los medios, se encuentran en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción engañosa, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
title: Implemente hacia adelante y rebobine rápidamente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# Implemente hacia adelante y rebobine rápidamente{#implement-fast-forward-and-rewind}

Cuando los usuarios avancen o rebobinen rápidamente a través de los medios, se encuentran en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción engañosa, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

>[!IMPORTANT]
>
>* El modo de reproducción de trucos solo es compatible con contenido MPEG Dash y HLS VOD.
>* El modo de reproducción de trucos no es compatible con emisiones en directo o anuncios.
>* Al cambiar del contenido principal a un anuncio, el SDK de explorador deja el modo de reproducción de trucos.

>



Para cambiar la velocidad, debe establecer un valor.

1. Pase del modo de reproducción normal (1x) al modo de reproducción de trucos ajustando la velocidad en `MediaPlayer` a un valor permitido.

   * La clase `MediaPlayerItem` define las tasas de reproducción permitidas.
   * El SDK del explorador selecciona la tasa permitida más cercana si no se permite la velocidad especificada.

      La siguiente función de ejemplo establece la velocidad:

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      La siguiente función de ejemplo se puede utilizar para consultar las tasas de reproducción disponibles:

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. Si lo desea, puede escuchar eventos de cambio de tasa, que le permiten saber cuándo solicitó un cambio de tasa y cuándo se produjo realmente un cambio de tasa.

       El SDK de TVSDK del explorador distribuye los siguientes eventos relacionados con la reproducción mediante trucos:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` cuando el  `rate` valor cambia a otro valor.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

      El SDK del explorador distribuye ambos eventos cuando el reproductor regresa del modo de reproducción truco al modo de reproducción normal.

## Elementos de API de cambio de tasa {#rate-change-API-elements}

El SDK de explorador incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con la redirección y el avance rápidos.

Utilice los siguientes elementos de API para cambiar las tasas de reproducción:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - especifica tasas válidas.

   | Valor de tasa | Efectos en la reproducción |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
   | -2,0, -4,0, -8,0, -16,0, -32,0, -64,0 | Cambia al modo de rebobinado rápido |
   | 1,0 | Cambia al modo de reproducción normal (llamar a `play` es lo mismo que establecer la propiedad rate en 1.0) |
   | 0,0 | Pausas (llamar a `pause` es lo mismo que establecer la propiedad rate en 0,0) |

## Limitaciones y comportamiento para el juego de trucos {#limitations-and-behavior-trick-play}

Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de reproducción de trucos.

Esta es una lista de las limitaciones del modo de reproducción mediante trucos:

* Si el flujo no contiene una adaptación de reproducción de trucos, el rebobinado rápido se desactiva y la velocidad de reproducción máxima para el avance rápido se limita a 8.
* Cuando se utilizan adaptaciones de reproducción de trucos para proporcionar el modo de truco, la pista de audio se desactiva.
* En el modo de reproducción mediante trucos, se desactiva la conmutación de las pistas de audio y de subtítulos.
* La reproducción y la pausa están activadas.
* En la llamada a otro punto del contenido, si la reproducción se encuentra en el modo de reproducción engañosa, la velocidad de reproducción se establece en 1 y se reanuda la reproducción normal.
* La lógica de velocidad de bits adaptable (ABR) está habilitada.

   Al utilizar adaptaciones normales, los perfiles se restringen entre `ABRControlParameters.minBitRate` y `ABRControlParameters.maxBitRate`. Cuando se utilizan adaptaciones de juego truco, los perfiles están restringidos entre `ABRControlParameters.minTrickPlayBitRate` y `ABRControlParameters.maxTrickPlayBitRate`.