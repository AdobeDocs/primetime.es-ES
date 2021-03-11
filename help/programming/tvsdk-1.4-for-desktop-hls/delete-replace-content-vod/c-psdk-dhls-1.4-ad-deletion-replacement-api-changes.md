---
description: Estos cambios en TVSDK admiten la eliminación y sustitución de anuncios.
title: Cambios en la API de reemplazo y eliminación de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Cambios en la API de reemplazo y eliminación de publicidad {#ad-deletion-and-replacement-api-changes}

Estos cambios en TVSDK admiten la eliminación y sustitución de anuncios.

* `AdSignalingMode` Se ha agregado el modo de  `CUSTOM_RANGES` señalización.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Se establece  `AdSignalingMode.CUSTOM_RANGES` si los intervalos de sustitución están en los metadatos.

* `PlacementType` Se ha añadido el  `CUSTOM_RANGE` tipo .

* `PlacementMode`

   * Se ha agregado el modo `DELETE`.
   * Se ha agregado el modo `MARK`
   * Modo `FreeReplace` agregado: este modo tiene una duración pero es una inserción pura

* `TimeRange` Ya no es una  `final` clase

* Se ha agregado el método `ReplaceTimeRange()`

   Amplía `TimeRange` para tener una propiedad `replacementDuration`. Para los casos MARK y DELETE, `replacementDuration` es 0.

* `TimeRangeCollection`

   * Se ha agregado la función de utilidad `toReplaceMetadata()` para extraer `timeRanges`.

   * Modificado para trabajar con `DELETE` y `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`,  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Se ha añadido `createCustomTimeRangesFrom()`: crea metadatos para casos de uso MARK/DELETE/REPLACE desde el archivo JSON.
   * Se ha eliminado `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Se ha añadido `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Se ha añadido `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (no cambió)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Se ha agregado `CustomRangesOpportunityGenerator` para cuándo los metadatos contienen intervalos personalizados
   * `doRetrieveResolvers()`

      * Agregue `CustomRangeResolver` para cuándo están presentes los intervalos personalizados DELETE y REEMPLAZAR en los metadatos
      * Se ha movido `CustomAdMarkerResolver` delante de `AuditudeResolver`


* Se ha añadido `CustomRangeOpportunityGenerator`

   * `doUpdate()` Deja vacío: sin actualización, VOD
   * `doProcess()` Crea una nueva colocación de un tipo nuevo  `Placement.Delete_Range`

   * Se ha agregado `CustomRangeOppotunityGenerator` al principio de la lista de generadores en `DefaultContentFactory`, por lo que los intervalos de eliminación se procesan antes de las inserciones de anuncios.

   * Se ha agregado `createCustomRangeOpportunities` para crear todas las oportunidades

      MARK: una oportunidad para cada rango de marcas válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.MARK`

      DELETE: una oportunidad para cada intervalo de eliminación válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`

      REEMPLAZAR - Dos oportunidades para cada rango de reemplazo válido:

      1. Una oportunidad de rango de eliminación de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`.

      1. Una oportunidad y toma de decisiones de anuncios de Primetime de `PlacementType.MID_ROLL` o `PlacementType.PRE_ROLL` y `PlacementMode.FREEREPLACE`

* Se ha añadido `CustomRangeResolver`:

   * `doCanResolve()` devuelve  `true` para intervalos de eliminación.

   * Se ha añadido `createDeleteRangeOperation()` para crear `DeleteRange` para la ubicación

* Se ha añadido `CustomRangeHelper`:

   * Clase de utilidad común para extraer Mark/Delete/Replace `timeRanges` y procesarlos.
   * Se ha añadido `extractCustomRangesMetadata()`
   * Se ha añadido `extractCustomRanges()`
   * Se ha añadido `mergeRanges()`: resuelve conflictos y subconjuntos/combinaciones

* `MediaPlayerTimeline`:

   * &quot;>En `executeOperation()`, si la operación es `DeleteRange`, se agregó una llamada para eliminar el método en la operación

   * En `executeOperation()`, si la operación es `NOPTimelineOperation` (`AdBreaks` vacío que regresa del servidor), se ha añadido la llamada a borrar.

   * Se ha añadido `onDeleteRangeComplete()`
   * Se ha añadido `removeRange()`
   * En `adjustPlacement()`, para el modo `PlacementMode.FREEREPLACE`, se agotó la duración como cero. Esta duración se necesita antes al solicitar `AdBreaks`, en este punto debe ser cero para que sea pura inserción.

* `VideoEngineTimeline` Se ha añadido  `removeC3Ad()` - Llamada  `removeByLocalTime()` para rangos de eliminación

* `AdSignalingModeGenerator`

   * `doConfigure()` - No resuelva si no se genera ninguna oportunidad
   * `createInitialOpportunity()` - No genere una oportunidad inicial para  `AdSignalingMode.CUSTOM_RANGE`. El `CustomRangeOpportunityGenerator` ya lo cubre.

* `DeleteRange`

   * Amplía `TimelineOperation`.
   * Creado por `CustomRangeResolver` para eliminación y reemplazo (la parte de eliminación de reemplazo)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir embalaje
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` El  `accepts()` método se modificó para permitir el empaquetado de diferentes tipos de ubicación (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correcciones de errores para permitir que el servidor anule los parámetros de anuncio

* `AuditudeResolver` Se cambió el  `canBePacked()` método para permitir el embalaje

* `CustomAdResolver` Se han eliminado las funciones de  `timeRange` extracción. Obtenemos una ubicación a la vez y la convertimos en `AdBreakPlacement timelineOperation`.

