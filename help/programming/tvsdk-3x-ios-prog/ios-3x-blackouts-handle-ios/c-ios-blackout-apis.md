---
description: TVSDK proporciona elementos de API que son útiles para implementar interrupciones, incluidos métodos, metadatos y notificaciones.
title: Elementos de API de interrupción
exl-id: 76d99d8d-1aae-4faa-aaf2-bb7b535a1c71
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Elementos de API de interrupción {#blackout-api-elements}

TVSDK proporciona elementos de API que son útiles para implementar interrupciones, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de interrupción en el reproductor.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como recurso de fondo. If `replaceCurrentItemWithPlayerItem` se llama después de este método, TVSDK continúa descargando el manifiesto del elemento en segundo plano hasta que realice la llamada a `unregisterCurrentBackgroundItem` , `stop`, o `reset` .

   * `unregisterCurrentBackgroundItem` Establece el elemento de fondo como cero y detiene la recuperación y el análisis del manifiesto de fondo.

* **PTMetadata.PTBlackoutMetadata** A `PTMetadata` clase específica de las interrupciones.

   Esto le permite establecer intervalos no buscables (una matriz de `CMTimeRanges`) en TVSDK. TVSDK comprueba estos intervalos cada vez que el usuario realiza una búsqueda. Si está establecido y el usuario busca en un rango no buscable, TVSDK fuerza al visor al final del rango no buscable.

* **EMPIECE AQUÍ A CONTINUACIÓN** **PTAdMetadata** Habilitar o deshabilitar el anuncio previo a la emisión en un flujo en directo mediante la configuración `enableLivePreroll` a SÍ o NO. Si está definido en NO, TVSDK no realiza una llamada explícita al servidor de publicidad para los anuncios previos a la emisión antes de la reproducción del contenido y, por lo tanto, no reproduce el anuncio previo a la emisión. Esto no afecta a los mid-rolls. El valor predeterminado es SÍ.

* **NSNotifications**

   * `PTTimedMetadataChangedInBackgroundNotification` - Publicado cuando TVSDK detecta una etiqueta suscrita en el manifiesto de fondo y un nuevo `PTTimedMetadata` La instancia de se prepara a partir de ella. El objeto de la notificación es `PTMediaPlayerItem` instancia que se está reproduciendo. Puede obtener la `PTTimedMetadata` de la instancia de `userInfo` usando el diccionario de `PTTimedMetadataKey` clave.

   * `PTBackgroundManifestErrorNotification` : Se publica cuando el reproductor de contenido no puede cargar completamente el manifiesto de fondo, es decir, todas las direcciones URL de flujo devuelven un error o una respuesta no válida. El objeto de la notificación es `PTMediaPlayerItem` instancia que se está reproduciendo.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error al descargar el manifiesto en segundo plano.
   * `INVALID_SEEK_WARNING` Se envía cuando se intenta realizar una búsqueda en un intervalo no buscable (en `nonSeekableRanges` establecer en `PTBlackoutMetadata`).
