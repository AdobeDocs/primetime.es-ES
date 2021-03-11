---
description: TVSDK proporciona elementos de API que son útiles para implementar bloqueos, incluidos métodos, metadatos y notificaciones.
title: Elementos de API de bloqueo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Bloqueo de elementos de API{#blackout-api-elements}

TVSDK proporciona elementos de API que son útiles para implementar bloqueos, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de bloqueo en el reproductor.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como el recurso en segundo plano. Si se llama a `replaceCurrentItemWithPlayerItem` después de este método, TVSDK continúa descargando el manifiesto del elemento de fondo hasta que realiza una llamada a `unregisterCurrentBackgroundItem` , `stop` o `reset` .

   * `unregisterCurrentBackgroundItem` Establece el elemento de fondo en nil y deja de recuperar y analizar el manifiesto de fondo.

* **PTMetadata.** PTBlackoutMetadataUna  `PTMetadata` clase específica para los apagones.

   Esto le permite establecer rangos que no se pueden buscar (una matriz de `CMTimeRanges`) en TVSDK. TVSDK comprueba estos intervalos cada vez que el usuario busca. Si está establecido y el usuario busca en un rango que no se puede buscar, TVSDK fuerza al visor al final del rango que no se puede buscar.

* **INICIE AQUÍ** **** NEXTPTAdMetadataHabilite o deshabilite el anuncio previo a la emisión en un flujo en directo estableciendo  `enableLivePreroll` en YES o NO. En caso negativo, TVSDK no realiza una llamada explícita al servidor de publicidad para los anuncios previos a la emisión antes de la reproducción del contenido, por lo que no reproduce el anuncio previo a la emisión. Esto no afecta a los grupos intermedios. El valor predeterminado es YES.

* **Notificaciones NSN**

   * `PTTimedMetadataChangedInBackgroundNotification` - Publicado cuando TVSDK detecta una etiqueta suscrita en el manifiesto de fondo y se prepara una nueva  `PTTimedMetadata` instancia a partir de él. El objeto de la notificación es la instancia `PTMediaPlayerItem` que se está reproduciendo actualmente. Puede recuperar la instancia `PTTimedMetadata` del diccionario `userInfo` de la notificación utilizando la clave `PTTimedMetadataKey`.

   * `PTBackgroundManifestErrorNotification` : Se publica cuando el reproductor de contenidos no puede cargar completamente el manifiesto de fondo, es decir, todas las URL de flujo devuelven un error o una respuesta no válida. El objeto de la notificación es la instancia `PTMediaPlayerItem` que se está reproduciendo actualmente.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error en la descarga del manifiesto en segundo plano.
   * `INVALID_SEEK_WARNING` Se envía cuando se intenta realizar una búsqueda en un intervalo no visible (en  `nonSeekableRanges` configurado en  `PTBlackoutMetadata`).


