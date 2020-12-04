---
description: TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.
seo-description: TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.
seo-title: Elementos de API de cambio de tasa
title: Elementos de API de cambio de tasa
uuid: 3554bf45-9419-4740-8a0e-484fc14c7436
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---


# Elementos de API de cambio de tasa {#rate-change-api-elements}

TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Utilice los siguientes elementos de API para cambiar las tasas de reproducción:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, que especifica tasas válidas.

| Valor de tasa | Efecto en la reproducción |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | Cambia al modo de rebobinado rápido |
| 1.0 | Cambia al modo de reproducción normal (llamar a `play` es lo mismo que establecer la propiedad rate en 1.0) |
| 0,0 | Pausas (llamar a `pause` es lo mismo que establecer la propiedad rate en 0,0) |

