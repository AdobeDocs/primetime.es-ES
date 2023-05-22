---
description: Cuando los usuarios avanzan o rebobinan rápidamente a través de los medios, se encuentran en el modo de reproducción con trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
title: Implementar avance rápido y rebobinado
exl-id: 21f9a3f6-1cae-4240-991d-c03a0e49adf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Implementar avance rápido y rebobinado{#implement-fast-forward-and-rewind}

Cuando los usuarios avanzan o rebobinan rápidamente a través de los medios, se encuentran en el modo de reproducción con trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

>[!IMPORTANT]
>
>* El modo Trick Play solo es compatible con contenido MPEG Dash y HLS VOD.
>* El modo Trick Play no es compatible con emisiones en vivo o anuncios.
>* Al cambiar del contenido principal a un anuncio, el TVSDK del explorador deja el modo de reproducción con trucos.
>


Para cambiar la velocidad, debe establecer un valor.

1. Cambie del modo de reproducción normal (1x) al modo de reproducción con trucos ajustando la velocidad en el `MediaPlayer` a un valor permitido.

   * El `MediaPlayerItem` define las velocidades de reproducción permitidas.
   * TVSDK del explorador selecciona la tasa permitida más cercana si la tasa especificada no está permitida.

      La siguiente función de ejemplo establece la tasa:

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

1. Si lo desea, puede escuchar eventos de cambio de tarifa, que le permiten saber cuándo solicitó un cambio de tarifa y cuándo se produce realmente un cambio de tarifa.

       El TVSDK del explorador distribuye los siguientes eventos relacionados con el juego de trucos:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` cuando la variable `rate` El valor cambia a un valor diferente.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

      El TVSDK del explorador envía ambos eventos cuando el reproductor vuelve del modo truco-reproducción al modo de reproducción normal.

## Elementos de API de tasa de cambio {#rate-change-API-elements}

El TVSDK del explorador incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite el truco y otras funcionalidades relacionadas con el avance y el rebobinado rápidos.

Utilice los siguientes elementos de la API para cambiar las tasas de reproducción:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - especifica tasas válidas.

   | Valor de tarifa | Efecto en la reproducción |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | Cambia al modo de rebobinado rápido |
   | 1.0 | Cambia al modo de reproducción normal (llamando a `play` es lo mismo que establecer la propiedad tasa en 1,0) |
   | 0.0 | Pausas (llamada a `pause` es lo mismo que establecer la propiedad tasa en 0,0) |

## Limitaciones y comportamiento para el truco {#limitations-and-behavior-trick-play}

Hay algunas limitaciones y algunos problemas en la forma en que se comporta el modo de juego con trucos.

Esta es una lista de las limitaciones del modo truco-juego:

* Si el flujo no contiene una adaptación de juego con trucos, el rebobinado rápido se desactiva y la tasa de juego máxima para el avance rápido está limitada a 8.
* Cuando se utilizan adaptaciones de juego de trucos para proporcionar el modo de truco, la pista de audio se desactiva.
* En el modo de reproducción con trucos, se desactiva la conmutación de pistas de audio y subtítulos.
* La reproducción y la pausa están habilitadas.
* En las búsquedas, si la reproducción se encuentra en modo de reproducción con trucos, la velocidad de reproducción se establece en 1 y la reproducción normal se reanuda.
* La lógica de velocidad de bits adaptable (ABR) está habilitada.

   Cuando se utilizan adaptaciones normales, los perfiles están restringidos entre `ABRControlParameters.minBitRate` y `ABRControlParameters.maxBitRate`. Al utilizar adaptaciones de juego con trucos, los perfiles están restringidos entre `ABRControlParameters.minTrickPlayBitRate` y `ABRControlParameters.maxTrickPlayBitRate`.
