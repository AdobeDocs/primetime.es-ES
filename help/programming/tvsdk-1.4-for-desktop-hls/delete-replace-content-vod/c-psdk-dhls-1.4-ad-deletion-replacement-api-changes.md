---
description: Estos cambios en TVSDK admiten la eliminación y el reemplazo de.
title: Eliminación de anuncios y cambios de API de reemplazo
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Eliminación de anuncios y cambios de API de reemplazo {#ad-deletion-and-replacement-api-changes}

Estos cambios en TVSDK admiten la eliminación y el reemplazo de.

* `AdSignalingMode` Añadido `CUSTOM_RANGES` modo de señalización.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Configurar `AdSignalingMode.CUSTOM_RANGES` si los rangos de reemplazo están en los metadatos.

* `PlacementType` Añadido `CUSTOM_RANGE` escriba.

* `PlacementMode`

   * Añadido `DELETE` modo.
   * Añadido `MARK` modo
   * Añadido `FreeReplace` modo: este modo tiene una duración, pero es una inserción pura

* `TimeRange` Ya no es `final` clase

* Añadido `ReplaceTimeRange()` método

   Extiende `TimeRange` para tener un `replacementDuration` propiedad. Para los casos MARK y DELETE, `replacementDuration` es 0.

* `TimeRangeCollection`

   * Añadido `toReplaceMetadata()` función de utilidad para extraer `timeRanges`.

   * Modificado para que funcione con `DELETE` y `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Añadido `createCustomTimeRangesFrom()` : crea metadatos para casos de uso de MARK/DELETE/REPLACE a partir del archivo JSON.
   * Eliminado `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Añadido `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Añadido `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (no ha cambiado)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Añadido `CustomRangesOpportunityGenerator` para cuando los metadatos contienen intervalos personalizados
   * `doRetrieveResolvers()`

      * Añadir `CustomRangeResolver` para cuando los intervalos personalizados de DELETE y REEMPLAZO están presentes en los metadatos
      * Movido `CustomAdMarkerResolver` por delante de `AuditudeResolver`


* Añadido `CustomRangeOpportunityGenerator`

   * `doUpdate()` Deja vacío: sin actualización, VOD
   * `doProcess()` Crea una nueva ubicación de un nuevo tipo `Placement.Delete_Range`

   * Añadido `CustomRangeOppotunityGenerator` al principio de la lista de generadores en `DefaultContentFactory`, por lo que los intervalos de eliminación se procesan antes de las inserciones de publicidad.

   * Añadido `createCustomRangeOpportunities` para crear todas las oportunidades

      MARK: una oportunidad para cada intervalo de marcas válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.MARK`

      DELETE: una oportunidad para cada intervalo de eliminación válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`

      REPLACE: dos oportunidades para cada intervalo de reemplazo válido:

      1. Una oportunidad de intervalo de eliminación de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`.

      1. Una oportunidad de Primetime y decisiones de `PlacementType.MID_ROLL` o `PlacementType.PRE_ROLL` y `PlacementMode.FREEREPLACE`

* Añadido `CustomRangeResolver`:

   * `doCanResolve()` devoluciones `true` para eliminar intervalos.

   * Añadido `createDeleteRangeOperation()` para crear `DeleteRange` para la ubicación

* Añadido `CustomRangeHelper`:

   * Clase de utilidad común para extraer Marcar/Eliminar/Reemplazar `timeRanges` y procesarlos.
   * Añadido `extractCustomRangesMetadata()`
   * Añadido `extractCustomRanges()`
   * Añadido `mergeRanges()` - Resuelve conflictos y subconjuntos/combinaciones

* `MediaPlayerTimeline`:

   * &quot;>En `executeOperation()`, si la operación es `DeleteRange`, se agregó una llamada al método remove en la operación

   * Entrada `executeOperation()`, si la operación es `NOPTimelineOperation` (vacío) `AdBreaks` regresando del servidor), se ha añadido la llamada para borrar.

   * Añadido `onDeleteRangeComplete()`
   * Añadido `removeRange()`
   * Entrada `adjustPlacement()`, para `PlacementMode.FREEREPLACE` modo, se ha eliminado la duración. Esta duración es necesaria con anterioridad al solicitar `AdBreaks`, en este punto debe ser cero para que sea pura inserción.

* `VideoEngineTimeline` Añadido `removeC3Ad()` - llamada `removeByLocalTime()` para eliminar intervalos

* `AdSignalingModeGenerator`

   * `doConfigure()` - No resolver si no se genera ninguna oportunidad
   * `createInitialOpportunity()` - No generar la oportunidad inicial para `AdSignalingMode.CUSTOM_RANGE`. El `CustomRangeOpportunityGenerator` ya cubre esto.

* `DeleteRange`

   * Extiende `TimelineOperation`.
   * Creado por `CustomRangeResolver` para eliminación y reemplazo (la parte de eliminación del reemplazo)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir el embalaje
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` El `accepts()` El método fue modificado para permitir el empaque de diferentes tipos de colocación (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correcciones de errores para permitir que el servidor anule los parámetros de publicidad

* `AuditudeResolver` El `canBePacked()` se ha cambiado el método para permitir el empaquetado

* `CustomAdResolver` El `timeRange` se han eliminado las funciones de extracción. Obtenemos una ubicación a la vez, y la convertimos en una `AdBreakPlacement timelineOperation`.
