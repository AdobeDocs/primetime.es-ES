---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-title: Cambios en la API de reemplazo y eliminación de publicidad
title: Cambios en la API de reemplazo y eliminación de publicidad
uuid: 3689d31f-4feb-4ea5-ac49-ef2e71472f4b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Cambios en la API de reemplazo y eliminación de publicidad {#ad-deletion-and-replacement-api-changes}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.

La función Eliminar y reemplazar amplía la función de marcadores de publicidad personalizados. Los marcadores de publicidad personalizados marcan secciones del contenido principal como períodos de contenido relacionados con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar dichos intervalos.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

Los siguientes cambios en TVSDK admiten la eliminación y sustitución.

**Nuevas API**

* `PTTimeRangeCollection` es una clase pública que define un conjunto predefinido de rangos y un tipo:

   * `property PTTimeRangeCollectionType type` indica el tipo de intervalo de tiempo.
   * `property NSArray* ranges` para establecer los intervalos de tiempo.

      El tipo esperado de objetos en la matriz es `PTReplacementTimeRange` o `CMTimeRange`.

      >[!TIP]
      >
      >Todos los objetos de la matriz deben ser del mismo tipo.

   * `PTTimeRangeCollectionType` es una enumeración que define el comportamiento de los rangos definidos en la  `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`:: El tipo de intervalos es  *Marcar*. Los intervalos se utilizan para marcar los intervalos en el contenido como Publicidades.

      * `PTTimeRangeCollectionTypeDeleteRanges`:: El tipo de rango es Eliminar. Los intervalos definidos se eliminan del contenido principal antes de la inserción de la publicidad.
      * `PTTimeRangeCollectionTypeReplaceRanges`:: El tipo de los rangos es Reemplazar. Los intervalos definidos se reemplazan del principal por Publicidades (el modo de señalización de publicidad se establece en `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nueva clase pública que define un único rango de  `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Define el inicio y la duración del rango.
   * `property long replacementDuration` - Si el tipo de  `TimeRangeCollection` es  `PTTimeRangeCollectionTypeReplaceRanges`,  `replacementDuration` se utiliza para crear una oportunidad de colocación (inserción de publicidad) con una duración de  `replacementDuration`. Si el `replacementDuration` no está configurado, el servidor de publicidad determinará la duración y el número de publicidades para esa oportunidad de colocación.

* `PTAdSignalingMode`::

   * `PTAdSignalingModeCustomTimeRanges` - Añadió un nuevo tipo de  `PTAdSignalingMode`. Este modo se utiliza junto con `PTTimeRangeCollection` con el tipo `PTTimeRangeCollectionReplace` para la inserción de publicidades en función de los intervalos de reemplazo.

* `PTAdMetadata`::

   * `property PTTimeRangeCollection* timeRangeCollection` - Para configurar los intervalos de tiempo utilizados en los rangos mark/delete/replace del contenido de reproducción.

* Registros de advertencia:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Advertencia
      * Descripción: el modo de señalización de publicidad se define como rangos personalizados, pero los rangos personalizados no se definen.
   * `INVALID_TIME_RANGES`

      * Tipo - Advertencia
      * Descripción: uno o varios intervalos de tiempo no son válidos y se omitirán o modificarán.


**API obsoletas**

* `PTAdMetadata`::

   * `property NSArray* externalAdRanges` - Esta propiedad se utilizó anteriormente para definir rangos C3 para marcar. Ahora está en desuso, ya que estos intervalos se establecen mediante `PTTimeRangeCollection`.