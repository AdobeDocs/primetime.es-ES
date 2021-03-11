---
description: TVSDK proporciona elementos de API que son útiles para implementar bloqueos, incluidos métodos, metadatos y notificaciones.
title: Elementos de API de bloqueo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Bloqueo de elementos de API{#blackout-api-elements}

TVSDK proporciona elementos de API que son útiles para implementar bloqueos, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de bloqueo en el reproductor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como el recurso en segundo plano. Si se llama a `replaceCurrentResource` después de este método, TVSDK continúa descargando el manifiesto del elemento de fondo hasta que realiza la llamada `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Borra el recurso en segundo plano establecido actualmente y deja de recuperar y analizar el manifiesto en segundo plano.

* **** BlackoutMetadataUn tipo de metadatos específico para los bloqueos.

   Esto le permite establecer rangos que no se pueden buscar (un atributo `TimeRange` adicional denominado `nonseekableRange`) en TVSDK. TVSDK comprueba estos intervalos (si la posición de búsqueda deseada está dentro de `nonseekableRange`) cada vez que el usuario busca. Si está configurado y el usuario busca en un intervalo que no se puede buscar, TVSDK fuerza al visor a la hora de finalización de `seekableRange`.

* **INICIE AQUÍ** **** NEXTDefaultMetadataKeysHabilite o deshabilite el preroll en un flujo en directo estableciendo  `ENABLE_LIVE_PREROLL` en true o false. Si es false, TVSDK no realiza una llamada explícita al servidor de publicidad para los anuncios previos a la emisión antes de la reproducción del contenido y, por lo tanto, no reproduce el anuncio previo a la emisión. Esto no afecta a los grupos intermedios. El valor predeterminado es true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` subtipo de evento : se envía cuando TVSDK detecta una etiqueta suscrita en el manifiesto de fondo.

* **Notificaciones**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error en la descarga del manifiesto en segundo plano.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Se envía cuando se intenta realizar una búsqueda en un intervalo no visible.


