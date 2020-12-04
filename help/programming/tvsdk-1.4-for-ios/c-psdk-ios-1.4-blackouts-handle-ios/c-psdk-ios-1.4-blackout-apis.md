---
description: TVSDK proporciona elementos de API que son útiles a la hora de implementar interrupciones, incluidos métodos, metadatos y notificaciones.
seo-description: TVSDK proporciona elementos de API que son útiles a la hora de implementar interrupciones, incluidos métodos, metadatos y notificaciones.
seo-title: Elementos de la API de bloqueo
title: Elementos de la API de bloqueo
uuid: ddc81558-4218-44d2-92df-15926c7c96b3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Elementos de API de bloqueo{#blackout-api-elements}

TVSDK proporciona elementos de API que son útiles a la hora de implementar interrupciones, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de bloqueo en el reproductor.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como recurso de fondo. Si se llama a `replaceCurrentItemWithPlayerItem` después de este método, TVSDK continúa descargando el manifiesto del elemento de fondo hasta que llama a `unregisterCurrentBackgroundItem` , `stop` o `reset`.

   * `unregisterCurrentBackgroundItem` Establece el elemento de fondo en nulo y deja de buscar y analizar el manifiesto de fondo.

* **PTMetadata.** PTBlackoutMetadataUna  `PTMetadata` clase específica para los apagones.

   Esto le permite establecer rangos no buscables (una matriz de `CMTimeRanges`) en TVSDK. TVSDK comprueba estos intervalos cada vez que el usuario busca. Si se establece y el usuario busca en un rango no buscable, TVSDK fuerza al visor al final del rango no buscable.

* **INICIO AQUÍ** **** NEXTPTAdMetadataHabilite o deshabilite el predesplazamiento en un flujo en directo  `enableLivePreroll` en YES o NO. Si NO, TVSDK no realiza una llamada explícita al servidor de publicidad para anuncios previos antes de la reproducción del contenido, por lo que no reproduce el anuncio previo. Esto no tiene ningún impacto en los rollos medios. El valor predeterminado es YES.

* **Notificaciones NSN**

   * `PTTimedMetadataChangedInBackgroundNotification` - Se publica cuando TVSDK detecta una etiqueta suscrita en el manifiesto de fondo y se prepara una nueva  `PTTimedMetadata` instancia a partir de él. El objeto de la notificación es la instancia `PTMediaPlayerItem` que se está reproduciendo actualmente. Puede recuperar la instancia `PTTimedMetadata` del diccionario `userInfo` de la notificación mediante la clave `PTTimedMetadataKey`.

   * `PTBackgroundManifestErrorNotification` - Se publica cuando el reproductor de medios no puede cargar completamente el manifiesto de fondo, es decir, todas las direcciones URL de flujo devuelven un error o una respuesta no válida. El objeto de la notificación es la instancia `PTMediaPlayerItem` que se está reproduciendo actualmente.

* **Notificación PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error en la descarga del manifiesto en segundo plano.
   * `INVALID_SEEK_WARNING` Se distribuye cuando se intenta buscar en un rango no buscable (en  `nonSeekableRanges` conjunto en  `PTBlackoutMetadata`).


