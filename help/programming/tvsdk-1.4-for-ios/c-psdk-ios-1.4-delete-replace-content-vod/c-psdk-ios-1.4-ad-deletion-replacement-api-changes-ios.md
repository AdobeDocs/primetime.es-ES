---
description: Los siguientes cambios en TVSDK admiten la eliminación y sustitución.
seo-description: Los siguientes cambios en TVSDK admiten la eliminación y sustitución.
seo-title: Cambios en la API de reemplazo y eliminación de publicidad
title: Cambios en la API de reemplazo y eliminación de publicidad
uuid: 7cc50e7a-666f-4588-9c16-ad6d7d75cb65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Cambios en la API de reemplazo y eliminación de publicidad{#ad-deletion-and-replacement-api-changes}

Los siguientes cambios en TVSDK admiten la eliminación y sustitución.

**Nuevas API**

* `PTTimeRangeCollection` es una clase pública que define un conjunto predefinido de rangos y un tipo:

   * `property PTTimeRangeCollectionType type` indica el tipo de intervalo de tiempo.
   * `property NSArray* ranges` para establecer los intervalos de tiempo.

      El tipo esperado de objetos en la matriz es `PTReplacementTimeRange` o `CMTimeRange`.

      >[!TIP]
      >
      >Todos los objetos de la matriz deben ser del mismo tipo.

   * `PTTimeRangeCollectionType` es una enumeración que define el comportamiento de los rangos definidos en la `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`:: El tipo de intervalos es *Marcar*. Los intervalos se utilizan para marcar los intervalos en el contenido como Publicidades.

      * `PTTimeRangeCollectionTypeDeleteRanges`:: El tipo de rango es Eliminar. Los intervalos definidos se eliminan del contenido principal antes de la inserción de la publicidad.
      * `PTTimeRangeCollectionTypeReplaceRanges`:: El tipo de los rangos es Reemplazar. Los rangos definidos se reemplazan del principal por Publicidades (el modo de señalización de publicidad está establecido en `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nueva clase pública que define un único rango de `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Define el inicio y la duración del intervalo.
   * `property long replacementDuration` - Si el tipo de `TimeRangeCollection` es `PTTimeRangeCollectionTypeReplaceRanges`, `replacementDuration` se utiliza para crear una oportunidad de colocación (inserción de publicidad) con una duración de `replacementDuration`. Si no `replacementDuration` se configura, el servidor de publicidad determinará la duración y el número de publicidades para esa oportunidad de colocación.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - Se ha agregado un nuevo tipo de `PTAdSignalingMode`. Este modo se utiliza junto con el `PTTimeRangeCollection` con el tipo `PTTimeRangeCollectionReplace` para la inserción de anuncios en función de los intervalos de reemplazo.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Para configurar los intervalos de tiempo utilizados en los rangos mark/delete/replace del contenido de reproducción.

* Registros de advertencia:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Advertencia
      * Descripción: el modo de señalización de publicidad se define como rangos personalizados, pero los rangos personalizados no se definen.
   * `INVALID_TIME_RANGES`

      * Tipo - Advertencia
      * Descripción: uno o varios intervalos de tiempo no son válidos y se omitirán o modificarán.


**API obsoletas**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Esta propiedad se utilizó anteriormente para definir rangos C3 para marcar. Ahora está en desuso, ya que estos intervalos se establecen mediante `PTTimeRangeCollection`.

