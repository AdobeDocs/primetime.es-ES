---
description: Los siguientes cambios en la compatibilidad, eliminación y sustitución de TVSDK.
title: Eliminación de anuncios y cambios de API de reemplazo
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Eliminación de anuncios y cambios de API de reemplazo{#ad-deletion-and-replacement-api-changes}

Los siguientes cambios en la compatibilidad, eliminación y sustitución de TVSDK.

**Nuevas API**

* `PTTimeRangeCollection` es una clase pública que define un conjunto predefinido de intervalos y un tipo:

   * `property PTTimeRangeCollectionType type` indica el tipo de intervalo de tiempo.
   * `property NSArray* ranges` se utiliza para establecer los intervalos de tiempo.

      El tipo de objetos esperado en la matriz es `PTReplacementTimeRange` o `CMTimeRange`.

      >[!TIP]
      >
      >Todos los objetos de la matriz deben ser del mismo tipo.

   * `PTTimeRangeCollectionType` es una enumeración que define el comportamiento para los intervalos definidos en la variable `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: el tipo de los intervalos es *Marcar*. Los intervalos se utilizan para marcar los intervalos del contenido como anuncios.

      * `PTTimeRangeCollectionTypeDeleteRanges`: el tipo de los intervalos es Eliminar. Los intervalos definidos se eliminan del contenido principal antes de la inserción del anuncio.
      * `PTTimeRangeCollectionTypeReplaceRanges`: el tipo de los intervalos es Reemplazar. Los intervalos definidos se sustituyen del principal por anuncios (el modo de señalización de publicidad está configurado en `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nueva clase pública que define un único intervalo de las `PTTimeRangeCollection`:

   * `property CMTimeRange range` : define el inicio y la duración del intervalo.
   * `property long replacementDuration` - Si el tipo de `TimeRangeCollection` es `PTTimeRangeCollectionTypeReplaceRanges`, el `replacementDuration` se utiliza para crear una oportunidad de colocación (inserción de publicidad) con una duración de `replacementDuration`. Si la variable `replacementDuration` no está configurado, el servidor de publicidad determinará la duración y el número de anuncios para esa oportunidad de ubicación.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - Se ha añadido un nuevo tipo de `PTAdSignalingMode`. Este modo se utiliza junto con el `PTTimeRangeCollection` con tipo `PTTimeRangeCollectionReplace` para la inserción de anuncios en función de los intervalos de reemplazo.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Para configurar los intervalos de tiempo utilizados en los intervalos de marcado/eliminación/reemplazo en el contenido de reproducción.

* Registros de advertencia:

   * `UNDEFINED_TIME_RANGES`

      * Tipo: advertencia
      * Descripción: el modo de señalización de publicidad se define como intervalos personalizados, pero los intervalos personalizados no están definidos.
   * `INVALID_TIME_RANGES`

      * Tipo: advertencia
      * Descripción: uno o más intervalos de tiempo no son válidos y se ignorarán o modificarán.


**API obsoletas**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` : Esta propiedad se utilizaba anteriormente para definir intervalos C3 para el marcado. Ahora está en desuso, ya que estos intervalos se establecen mediante `PTTimeRangeCollection`.

