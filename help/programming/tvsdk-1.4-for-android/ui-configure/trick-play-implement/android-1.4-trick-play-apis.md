---
description: TVSDK incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite el truco y otras funcionalidades relacionadas con el avance y el rebobinado rápidos.
title: Elementos de API de tasa de cambio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# Elementos de API de tasa de cambio{#rate-change-api-elements}

TVSDK incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite el truco y otras funcionalidades relacionadas con el avance y el rebobinado rápidos.

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

Utilice los siguientes elementos de la API para cambiar las tasas de reproducción:

* `PlaybackRateEvent.getRate`
* `MediaPlayer.getLocalTime`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.getAvailablePlaybackRates` - especifica tasas válidas.

| Valor de tarifa | Efecto en la reproducción |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Cambia al modo de rebobinado rápido |
| 1.0 | Cambia al modo de reproducción normal (llamando a `play` es lo mismo que establecer la propiedad tasa en 1,0) |
| 0.0 | Pausas (llamada a `pause` es lo mismo que establecer la propiedad tasa en 0,0) |
