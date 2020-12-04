---
description: TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.
seo-description: TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.
seo-title: Elementos de API de cambio de tasa
title: Elementos de API de cambio de tasa
uuid: 0040d35c-f9cb-4066-9bee-828ed5541194
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---


# Elementos API de cambio de tasa{#rate-change-api-elements}

TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

Utilice los siguientes elementos de API para cambiar las tasas de reproducción:

* `PlaybackRateEvent.getRate`
* `MediaPlayer.getLocalTime`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.getAvailablePlaybackRates` - especifica tasas válidas.

| Valor de tasa | Efecto en la reproducción |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | Cambia al modo de rebobinado rápido |
| 1.0 | Cambia al modo de reproducción normal (llamar a `play` es lo mismo que establecer la propiedad rate en 1.0) |
| 0,0 | Pausas (llamar a `pause` es lo mismo que establecer la propiedad rate en 0,0) |

