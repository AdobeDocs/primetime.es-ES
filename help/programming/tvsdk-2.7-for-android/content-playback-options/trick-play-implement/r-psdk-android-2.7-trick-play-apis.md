---
description: TVSDK incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite el truco y otras funcionalidades relacionadas con el avance y el rebobinado rápidos.
title: Elementos de API de tasa de cambio
exl-id: deb8c1cb-c6b2-4328-a5e1-cca893ea066f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Elementos de API de tasa de cambio {#rate-change-api-elements}

TVSDK incluye métodos, propiedades y eventos para determinar tasas válidas, tasas actuales, si se admite el truco y otras funcionalidades relacionadas con el avance y el rebobinado rápidos.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Utilice los siguientes elementos de la API para cambiar las tasas de reproducción:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, que especifica tasas válidas.

| Valor de tarifa | Efecto en la reproducción |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Cambia al modo de avance rápido con el multiplicador especificado más rápido de lo normal (por ejemplo, 4 es 4 veces más rápido de lo normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Cambia al modo de rebobinado rápido |
| 1.0 | Cambia al modo de reproducción normal (llamando a `play` es lo mismo que establecer la propiedad tasa en 1,0) |
| 0.0 | Pausas (llamada a `pause` es lo mismo que establecer la propiedad tasa en 0,0) |
