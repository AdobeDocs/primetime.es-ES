---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos de VOD.
title: Cambios en la API de reemplazo y eliminación de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Cambios en la API de reemplazo y eliminación de publicidad {#ad-deletion-and-replacement-api-changes}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos de VOD.

La función de eliminar y reemplazar amplía la función de marcadores de anuncios personalizados. Los marcadores de anuncios personalizados marcan secciones del contenido principal como períodos de contenido relacionado con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar intervalos de tiempo.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

Los siguientes cambios en TVSDK admiten la eliminación y sustitución de anuncios.

**Nuevas API**

* `PTTimeRangeCollection` es una clase pública que define un conjunto predefinido de rangos y un tipo:

   * `property PTTimeRangeCollectionType type` indica el tipo de intervalo de tiempo.
   * `property NSArray* ranges` se utiliza para establecer los intervalos de tiempo.

      El tipo esperado de objetos en la matriz es `PTReplacementTimeRange` o `CMTimeRange`.

      >[!TIP]
      >
      >Todos los objetos de la matriz deben ser del mismo tipo.

   * `PTTimeRangeCollectionType` es una enumeración que define el comportamiento para los intervalos definidos en el  `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: El tipo de intervalos es  *Marcar*. Los intervalos se utilizan para marcar los intervalos en el contenido como anuncios.

      * `PTTimeRangeCollectionTypeDeleteRanges`: El tipo de intervalos es Eliminar. Los intervalos definidos se eliminan del contenido principal antes de la inserción del anuncio.
      * `PTTimeRangeCollectionTypeReplaceRanges`: El tipo de los intervalos es Reemplazar. Los intervalos definidos se sustituyen del principal por Anuncios (el modo de señalización de anuncio se establece en `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nueva clase pública que define un único rango de  `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Define el inicio y la duración del rango.
   * `property long replacementDuration` - Si el tipo de  `TimeRangeCollection` es  `PTTimeRangeCollectionTypeReplaceRanges`, se  `replacementDuration` utiliza para crear una oportunidad de colocación (inserción de publicidad) con una duración de  `replacementDuration`. Si no se configura el `replacementDuration`, el servidor de publicidad determinará la duración y el número de publicidades para esa oportunidad de colocación.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - Se ha añadido un nuevo tipo de  `PTAdSignalingMode`. Este modo se utiliza junto con `PTTimeRangeCollection` con el tipo `PTTimeRangeCollectionReplace` para la inserción de anuncios en función de los intervalos de reemplazo.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Para establecer los intervalos de tiempo utilizados en los intervalos de marca, eliminación o sustitución del contenido de reproducción.

* Registros de advertencia:

   * `UNDEFINED_TIME_RANGES`

      * Tipo: advertencia
      * Descripción: El modo de señalización de anuncio se define como rangos personalizados, pero no se definen.
   * `INVALID_TIME_RANGES`

      * Tipo: advertencia
      * Descripción: uno o varios intervalos de tiempo no son válidos y se ignorarán o modificarán.


**API obsoletas**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Esta propiedad se utilizó anteriormente para definir rangos C3 para el marcado. Ahora está en desuso, ya que estos intervalos se establecen mediante `PTTimeRangeCollection`.