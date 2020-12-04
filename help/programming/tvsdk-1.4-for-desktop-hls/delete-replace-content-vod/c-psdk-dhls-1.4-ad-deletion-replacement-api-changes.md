---
description: Estos cambios en TVSDK admiten la eliminación y sustitución de publicidades.
seo-description: Estos cambios en TVSDK admiten la eliminación y sustitución de publicidades.
seo-title: Cambios en la API de reemplazo y eliminación de publicidad
title: Cambios en la API de reemplazo y eliminación de publicidad
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Cambios en la API de reemplazo y eliminación de publicidad {#ad-deletion-and-replacement-api-changes}

Estos cambios en TVSDK admiten la eliminación y sustitución de publicidades.

* `AdSignalingMode` Modo  `CUSTOM_RANGES` de señalización añadido.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Se establece  `AdSignalingMode.CUSTOM_RANGES` si los rangos de sustitución están en los metadatos.

* `PlacementType`  `CUSTOM_RANGE` Tipo añadido.

* `PlacementMode`

   * Modo añadido `DELETE`.
   * Modo `MARK` añadido
   * Modo añadido `FreeReplace`: este modo tiene una duración pero es una inserción pura

* `TimeRange` Ya no es una  `final` clase

* Método `ReplaceTimeRange()` añadido

   Extiende `TimeRange` para tener una propiedad `replacementDuration`. En los casos MARK y DELETE, `replacementDuration` es 0.

* `TimeRangeCollection`

   * Se añadió la función de utilidad `toReplaceMetadata()` para extraer `timeRanges`.

   * Modificado para trabajar con `DELETE` y `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`,  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Añadido `createCustomTimeRangesFrom()`: crea metadatos para casos de uso MARK/DELETE/REPLACE desde el archivo JSON.
   * Eliminado `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Añadido `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Añadido `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (no cambió)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Se añadió `CustomRangesOpportunityGenerator` para cuando los metadatos contienen intervalos personalizados
   * `doRetrieveResolvers()`

      * Añadir `CustomRangeResolver` para cuándo están presentes los rangos personalizados DELETE y REEMPLAZAR en los metadatos
      * Se movió `CustomAdMarkerResolver` por delante de `AuditudeResolver`


* Añadido `CustomRangeOpportunityGenerator`

   * `doUpdate()` Sale vacío: sin actualización, VOD
   * `doProcess()` Crea una nueva colocación de un nuevo tipo  `Placement.Delete_Range`

   * Se añadió `CustomRangeOppotunityGenerator` en la parte superior de la lista de generadores en `DefaultContentFactory`, por lo que los rangos de eliminación se procesan antes de las inserciones de publicidad.

   * Se añadió `createCustomRangeOpportunities` para crear todas las oportunidades

      MARK: una oportunidad para cada intervalo de marcas válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.MARK`

      DELETE: una oportunidad para cada intervalo de eliminación válido de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`

      REEMPLAZAR: Dos oportunidades para cada intervalo de reemplazo válido:

      1. Una oportunidad de eliminar intervalo de `PlacementType.CUSTOM_RANGE` y `PlacementMode.DELETE`.

      1. Una oportunidad de toma de decisiones y decisiones publicitarias Primetime de `PlacementType.MID_ROLL` o `PlacementType.PRE_ROLL` y `PlacementMode.FREEREPLACE`

* Se añadió `CustomRangeResolver`:

   * `doCanResolve()` devuelve  `true` para eliminar intervalos.

   * Se añadió `createDeleteRangeOperation()` para crear `DeleteRange` para la colocación

* Se añadió `CustomRangeHelper`:

   * Clase de utilidad común para extraer Mark/Delete/Replace `timeRanges` y procesarlos.
   * Añadido `extractCustomRangesMetadata()`
   * Añadido `extractCustomRanges()`
   * Añadido `mergeRanges()`: resuelve conflictos y subconjuntos/combinaciones

* `MediaPlayerTimeline`::

   * &quot;>En `executeOperation()`, si la operación es `DeleteRange`, se agregó una llamada al método remove en la operación

   * En `executeOperation()`, si la operación es `NOPTimelineOperation` (vacía `AdBreaks` regresando del servidor), se agregó una llamada para borrar.

   * Añadido `onDeleteRangeComplete()`
   * Añadido `removeRange()`
   * En el modo `adjustPlacement()`, para `PlacementMode.FREEREPLACE`, se agotó la duración. Esta duración se necesita antes cuando se solicita `AdBreaks`, en este punto debe ser cero para que sea pura inserción.

* `VideoEngineTimeline` Añadido  `removeC3Ad()` - llamada  `removeByLocalTime()` para eliminar intervalos

* `AdSignalingModeGenerator`

   * `doConfigure()` - No resolver si no se genera ninguna oportunidad
   * `createInitialOpportunity()` - No genere una oportunidad inicial para  `AdSignalingMode.CUSTOM_RANGE`. El `CustomRangeOpportunityGenerator` ya cubre esto.

* `DeleteRange`

   * Extiende `TimelineOperation`.
   * Creado por `CustomRangeResolver` para eliminación y reemplazo (la parte de eliminación de reemplazo)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir embalaje
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` El  `accepts()` método se modificó para permitir el empaquetado de diferentes tipos de colocación (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correcciones de errores para permitir que el servidor anule los parámetros de publicidad

* `AuditudeResolver` Se cambió el  `canBePacked()` método para permitir el empaquetado

* `CustomAdResolver` Se han eliminado las funciones de  `timeRange` extracción. Obtenemos una colocación a la vez y la convertimos en `AdBreakPlacement timelineOperation`.

