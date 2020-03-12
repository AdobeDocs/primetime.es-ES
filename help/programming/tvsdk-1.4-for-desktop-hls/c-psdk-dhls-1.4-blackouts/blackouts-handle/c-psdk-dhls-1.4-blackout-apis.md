---
description: TVSDK proporciona elementos de API que son útiles a la hora de implementar interrupciones, incluidos métodos, metadatos y notificaciones.
seo-description: TVSDK proporciona elementos de API que son útiles a la hora de implementar interrupciones, incluidos métodos, metadatos y notificaciones.
seo-title: Elementos de la API de bloqueo
title: Elementos de la API de bloqueo
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Elementos de la API de bloqueo{#blackout-api-elements}

TVSDK proporciona elementos de API que son útiles a la hora de implementar interrupciones, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de bloqueo en el reproductor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como recurso de fondo. Si `replaceCurrentResource` se llama después de este método, TVSDK continúa descargando el manifiesto del elemento de fondo hasta que llama a `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Borra el recurso en segundo plano establecido actualmente y deja de buscar y analizar el manifiesto en segundo plano.

* **BlackoutMetadata** Un tipo de metadatos que es específico de las interrupciones.

   Esto le permite establecer rangos no buscables (un `TimeRange` atributo adicional denominado `nonseekableRange`) en TVSDK. TVSDK comprueba estos intervalos (si la posición de búsqueda deseada se encuentra dentro de un `nonseekableRange`) cada vez que el usuario busca. Si se establece y el usuario busca en un rango no buscable, TVSDK fuerza al visor a la hora de finalización del `seekableRange`.

* **INICIAR AQUÍ SIGUIENTE** **DefaultMetadataKeys** Habilite o deshabilite la preconfiguración en un flujo en directo estableciendo `ENABLE_LIVE_PREROLL` en true o false. Si el valor es false, TVSDK no realiza una llamada explícita al servidor de publicidad para anuncios previos a la reproducción del contenido, por lo que no reproduce el anuncio previo. Esto no tiene ningún impacto en los rollos medios. El valor predeterminado es true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` subtipo de evento: se distribuye cuando TVSDK detecta una etiqueta suscrita en el manifiesto de fondo.

* **Notificaciones**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error en la descarga del manifiesto en segundo plano.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Se distribuye cuando se intenta realizar una búsqueda en un rango no buscable.


