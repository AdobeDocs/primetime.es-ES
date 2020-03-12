---
description: Estos cambios en TVSDK admiten la eliminación y sustitución de publicidades.
seo-description: Estos cambios en TVSDK admiten la eliminación y sustitución de publicidades.
seo-title: Cambios en la API de reemplazo y eliminación de publicidad
title: Cambios en la API de reemplazo y eliminación de publicidad
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Cambios en la API de reemplazo y eliminación de publicidad {#ad-deletion-and-replacement-api-changes}

Estos cambios en TVSDK admiten la eliminación y sustitución de publicidades.

* `AdSignalingMode` Se ha agregado el modo `CUSTOM_RANGES` de señalización.

* `OpportunityGenerator`  `extractAdSignalingMode()` : `AdSignalingMode.CUSTOM_RANGES` se establece si los rangos de sustitución están en los metadatos.

* `PlacementType` Se ha agregado `CUSTOM_RANGE` el tipo.

* `PlacementMode`

   * Se ha agregado `DELETE` el modo.
   * Se ha agregado `MARK` el modo
   * Modo agregado `FreeReplace` : este modo tiene una duración pero es una inserción pura

* `TimeRange` Ya no es una `final` clase

* Se ha agregado `ReplaceTimeRange()` el método

   Se amplía `TimeRange` para tener una `replacementDuration` propiedad. Para los casos MARK y DELETE, `replacementDuration` es 0.

* `TimeRangeCollection`

   * Se agregó `toReplaceMetadata()` una función de utilidad para extraer `timeRanges`.

   * Modificado para trabajar con `DELETE` y `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Agregado `createCustomTimeRangesFrom()` : crea metadatos para los casos de uso MARK/DELETE/REPLACE desde el archivo JSON.
   * Eliminado `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Agregado `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Agregado `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (no cambió)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Se agregó `CustomRangesOpportunityGenerator` para cuando los metadatos contienen intervalos personalizados
   * `doRetrieveResolvers()`

      * Agregar `CustomRangeResolver` para cuando los rangos personalizados ELIMINAR y REEMPLAZAR estén presentes en los metadatos
      * Se ha movido `CustomAdMarkerResolver` por delante de `AuditudeResolver`


* Agregado `CustomRangeOpportunityGenerator`

   * `doUpdate()` Sale vacío: sin actualización, VOD
   * `doProcess()` Crea una nueva colocación de un nuevo tipo `Placement.Delete_Range`

   * Se ha agregado `CustomRangeOppotunityGenerator` a la parte superior de la lista de generadores de `DefaultContentFactory`, por lo que los rangos de eliminación se procesan antes de las inserciones de publicidad.

   * Se agregó `createCustomRangeOpportunities` para crear todas las oportunidades

      MARK: una oportunidad para cada intervalo de marcas válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.MARK`

      ELIMINAR: una oportunidad para cada rango de eliminación válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`

      REEMPLAZAR: Dos oportunidades para cada intervalo de reemplazo válido:

      1. Una oportunidad de eliminar intervalo de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`.

      1. Una decisión y oportunidad de Primetime `PlacementType.MID_ROLL` o `PlacementType.PRE_ROLL` y `PlacementMode.FREEREPLACE`

* Se agregó `CustomRangeResolver`:

   * `doCanResolve()` devuelve `true` para los intervalos de eliminación.

   * Se agregó `createDeleteRangeOperation()` para crear `DeleteRange` la colocación

* Se agregó `CustomRangeHelper`:

   * Clase de utilidad común para extraer la marca/eliminar/reemplazar `timeRanges` y procesarlos.
   * Agregado `extractCustomRangesMetadata()`
   * Agregado `extractCustomRanges()`
   * Agregado `mergeRanges()` : resuelve conflictos y subconjuntos/combinaciones

* `MediaPlayerTimeline`:

   * &quot;>En `executeOperation()`, si la operación es `DeleteRange`, se agregó una llamada para quitar método en la operación

   * En `executeOperation()`, si la operación está `NOPTimelineOperation` (vacío `AdBreaks` regresando del servidor), se ha añadido una llamada para borrar.

   * Agregado `onDeleteRangeComplete()`
   * Agregado `removeRange()`
   * En `adjustPlacement()`, para `PlacementMode.FREEREPLACE` modo, se agotó la duración. Esta duración se necesita antes al solicitar `AdBreaks`, en este punto debe ser cero para ser una inserción pura.

* `VideoEngineTimeline` Se agregó `removeC3Ad()` - llamada `removeByLocalTime()` para eliminar rangos

* `AdSignalingModeGenerator`

   * `doConfigure()` - No resolver si no se genera ninguna oportunidad
   * `createInitialOpportunity()` - No genere una oportunidad inicial para `AdSignalingMode.CUSTOM_RANGE`. Ya `CustomRangeOpportunityGenerator` cubre esto.

* `DeleteRange`

   * Se amplía `TimelineOperation`.
   * Creado por `CustomRangeResolver` para eliminación y reemplazo (la parte de eliminación de reemplazo)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir embalaje
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` El `accepts()` método se modificó para permitir el empaquetado de diferentes tipos de colocación (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correcciones de errores para permitir que el servidor anule los parámetros de publicidad

* `AuditudeResolver` Se cambió el `canBePacked()` método para permitir el empaquetado

* `CustomAdResolver` Se han eliminado las `timeRange` funciones de extracción. Obtenemos una colocación a la vez, y la convertimos en una `AdBreakPlacement timelineOperation`.

