---
description: TVSDK proporciona elementos de API que son útiles para implementar interrupciones, incluidos métodos, metadatos y notificaciones.
title: Elementos de API de interrupción
exl-id: 9dae236b-0bd8-4fce-9163-628d4ed94f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Elementos de API de interrupción{#blackout-api-elements}

TVSDK proporciona elementos de API que son útiles para implementar interrupciones, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de interrupción en el reproductor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como recurso de fondo. If `replaceCurrentResource` se llama después de este método, TVSDK continúa descargando el manifiesto del elemento en segundo plano hasta que realice la llamada a `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Borra el recurso en segundo plano establecido actualmente y detiene la recuperación y el análisis del manifiesto en segundo plano.

* **BlackoutMetadata** Un tipo de metadatos específico de las interrupciones.

   Esto le permite establecer intervalos no buscables (un `TimeRange` atributo llamado `nonseekableRange`) en TVSDK. TVSDK comprueba estos intervalos (si la posición de búsqueda deseada se encuentra dentro de un `nonseekableRange`) cada vez que el usuario lo busca. Si está configurado y el usuario busca en un rango no buscable, TVSDK fuerza al visualizador a la hora de finalización del `seekableRange`.

* **EMPIECE AQUÍ A CONTINUACIÓN** **DefaultMetadataKeys** Habilite o deshabilite el preroll en un flujo en vivo mediante la configuración `ENABLE_LIVE_PREROLL` a true o false. Si es false, TVSDK no realiza una llamada explícita al servidor de publicidad para los anuncios previos a la emisión antes de la reproducción del contenido y, por lo tanto, no reproduce el anuncio previo a la emisión. Esto no afecta a los mid-rolls. El valor predeterminado es True.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` subtipo de evento: se envía cuando TVSDK detecta una etiqueta suscrita en el manifiesto de fondo.

* **Notificaciones**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error al descargar el manifiesto en segundo plano.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Se envía cuando se intenta realizar una búsqueda en un intervalo no buscable.
