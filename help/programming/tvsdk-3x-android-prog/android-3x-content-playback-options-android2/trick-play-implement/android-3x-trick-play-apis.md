---
description: TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.
seo-description: TVSDK incluye métodos, propiedades y eventos para determinar las tasas válidas, las tasas actuales, si se admite la reproducción mediante trucos y otras funciones relacionadas con el avance rápido y el rebobinado.
seo-title: Elementos de API de cambio de tasa
title: Elementos de API de cambio de tasa
uuid: c2bcd20c-0641-4d75-802c-08098786d572
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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

| **Valor de tasa** | **Efecto en la reproducción** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Cambia al modo de rebobinado rápido |
| 1.0 | Cambia al modo de reproducción normal (llamar `play` es lo mismo que establecer la propiedad rate en 1.0) |
| 0.0 | Pausas (llamar `pause` es lo mismo que establecer la propiedad rate en 0,0) |