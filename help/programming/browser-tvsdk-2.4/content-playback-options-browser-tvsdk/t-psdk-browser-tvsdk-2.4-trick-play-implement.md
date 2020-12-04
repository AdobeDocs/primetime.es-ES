---
description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-title: Implemente un avance rápido y rebobine
title: Implemente un avance rápido y rebobine
uuid: c1992757-d067-4c11-8d08-fec09099476f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---


# Implemente un avance rápido y rebobine{#implement-fast-forward-and-rewind}

Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

>[!IMPORTANT]
>
>* El modo de reproducción de trucos solo se admite para contenido MPEG Dash y HLS VOD.
>* El modo de reproducción de trucos no es compatible con transmisiones en directo o anuncios.
>* Cuando se cambia del contenido principal a una publicidad, el SDK de TVSDK del explorador deja el modo de reproducción incorrecta.

>



Para cambiar la velocidad, debe establecer un valor.

1. Pasar del modo de reproducción normal (1x) al modo de reproducción de trucos estableciendo la velocidad en `MediaPlayer` a un valor permitido.

   * La clase `MediaPlayerItem` define las tasas de reproducción permitidas.
   * TVSDK del explorador selecciona la velocidad permitida más cercana si no se permite la velocidad especificada.

      La siguiente función de ejemplo establece la velocidad:

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      Se puede utilizar la siguiente función de ejemplo para consulta de las tasas de reproducción disponibles:

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. De forma opcional, puede escuchar eventos de cambio de tasa, que le informarán cuando solicitó un cambio de tasa y cuando realmente se produce un cambio de tasa.

       El SDK de TVSDK del explorador distribuye los siguientes eventos relacionados con la reproducción mediante trucos:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` cuando el  `rate` valor cambia a otro valor.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

      El SDK de TVSDK del explorador distribuye ambos eventos cuando el reproductor regresa del modo de reproducción mediante trucos al modo de reproducción normal.

## Elementos de API de cambio de tasa {#rate-change-API-elements}

El SDK de explorador incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.

Utilice los siguientes elementos de API para cambiar las tasas de reproducción:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - especifica tasas válidas.

   | Valor de tasa | Efecto en la reproducción |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | Cambia al modo de rebobinado rápido |
   | 1.0 | Cambia al modo de reproducción normal (llamar a `play` es lo mismo que establecer la propiedad rate en 1.0) |
   | 0,0 | Pausas (llamar a `pause` es lo mismo que establecer la propiedad rate en 0,0) |

## Limitaciones y comportamiento para el juego de trucos {#limitations-and-behavior-trick-play}

Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de reproducción mediante trucos.

A continuación se muestra una lista de las limitaciones del modo de reproducción mediante trucos:

* Si el flujo no contiene una adaptación de reproducción mediante trucos, el rebobinado rápido se desactiva y la velocidad máxima de reproducción para el avance rápido se limita a 8.
* Cuando se utilizan las adaptaciones de reproducción mediante trucos para proporcionar el modo de truco, la pista de audio se desactiva.
* En el modo de reproducción con trucos, se desactiva el cambio de pistas de audio y de subtítulos opcionales.
* La reproducción y la pausa están activadas.
* En la búsqueda, si la reproducción está en modo de reproducción con trucos, la velocidad de reproducción se establece en 1 y se reanuda la reproducción normal.
* La lógica de velocidad de bits adaptable (ABR) está habilitada.

   Cuando se utilizan adaptaciones normales, los perfiles se restringen entre `ABRControlParameters.minBitRate` y `ABRControlParameters.maxBitRate`. Cuando se utilizan adaptaciones de juego de trucos, los perfiles se restringen entre `ABRControlParameters.minTrickPlayBitRate` y `ABRControlParameters.maxTrickPlayBitRate`.