---
description: Estos cambios en la API TVSDK de Android admiten la eliminación y sustitución de anuncios.
title: Cambios en la API de reemplazo y eliminación de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---


# Cambios en la API de reemplazo y eliminación de publicidad{#ad-deletion-and-replacement-api-changes}

Estos cambios en la API TVSDK de Android admiten la eliminación y sustitución de anuncios.

* `AdSignalingMode` Nuevo modo de señalización de anuncio de intervalo de tiempo personalizado

* `AdvertisingMetadata` Nuevo  `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Establece los intervalos de tiempo para marcar, eliminar o reemplazar al procesar metadatos

* `ContentResolver`

   * Nuevo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nuevo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nueva clase `ContentRemoval`

   `TimelineOperation` clase que define el intervalo de tiempo que se va a eliminar de la cronología

* `AuditudeResolver`

   * Nuevo `private LinkedList<AuditudeRequest> _requestQueue`
   * Nuevo `void startConsumer()`: Inicia el procesamiento de la cola de solicitudes de primetime y decisioning y garantiza que cada solicitud se publique a intervalos `MIN_INIT_REQUEST_INTERVAL`

   * Nuevo `processReplacementRange()`: Extrae intervalos de tiempo de los metadatos de publicidad, genera `PlacementInformations` y crea una solicitud de toma de decisiones de publicidad de Primetime que contiene el `PlacementInformations`.

   * Nuevo `canDoResolver()`: Comprueba si la oportunidad de colocación tiene metadatos de Primetime y decisioning

* Nueva clase `CustomRangeHelper` Helper que extrae metadatos de intervalo de tiempo de los metadatos de anuncio y elimina los subconjuntos/superposiciones/intervalos de tiempo no válidos.

* Nuevo `DeleteContentResolver` solucionador de contenido que resuelve las oportunidades de colocación de `PlacementInformation.Mode.DELETE`

* Nueva `NopTimelineOperation` nueva operación de cronología para los casos en los que no es necesario realizar la colocación o el reemplazo de una pausa publicitaria. Esta clase se utiliza para distinguir entre esto y cuando se produce un error durante el proceso de resolución.

* `TimelineOperationQueue` Comprueba si la operación de línea de tiempo es una  `NopTimelineOperation` antes del procesamiento.

* `CustomAdMarkersContentResolver` Nuevo  `canDoResolve()`: Comprueba si una oportunidad de colocación es del tipo  `Mode.MARK`

* `MetadataResolver` Nuevo  `canDoResolve()`: Comprueba si una oportunidad de colocación es del tipo  `Mode.INSERT`

* `DefaultMetadataKeys` Nuevo  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nuevo modo `enum (INSERT, DELETE, REPLACE, MARK)`
   * Nuevo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Nuevo  `compareTo(TimeRange timeRange)`: De modo que puede ordenar los intervalos de tiempo en función de la hora de inicio

* La nueva `ReplacementTimeRange` amplía la clase `TimeRange` que representa un intervalo de tiempo de reemplazo, con un parámetro `begin`, `end` y `replacement-duration`.

* `TimeRangeCollection`

   * Nuevo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Se cambió el nombre `CUSTOM_AD_MARKERS` a `MARK_RANGES`

   * Se ha modificado `toMetadata(Metadata options)` para colocar intervalos de eliminación/marca/sustitución en metadatos de publicidad.

* `MediaPlayerNotification`

   * Nuevo `UNDEFINED_TIME_RANGES`: Cuando el modo de señalización de anuncio es Mapa del servidor o Señales de manifiesto, y los rangos de sustitución también están en los metadatos de anuncio, se omiten los rangos de reemplazo.
   * Nuevo `REPLACE_RANGES_NOT_AVAILABLE`: Cuando el modo de señalización de publicidad es Intervalos de tiempo personalizados y los intervalos de reemplazo no están disponibles, se envía una advertencia.

* `AdvertisingFactory` Nuevo  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nuevo  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nuevo  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * En `prepareToPlay()`: Realiza una búsqueda inicial a 0, ya que si se elimina el rango `[0,n]`, el reproductor de contenidos no se reproducirá automáticamente.

   * En `prepareToPlay()`: Pasa por la lista de información de colocación inicial para que `mediaplayerclient` se resuelva.

   * En `extractAdSignalingMode()`: Aloje el nuevo modo Intervalo de tiempo personalizado .
   * Nuevo `private static List<PlacementInformation> createInitalPlacementInformations()`: Genera la información de colocación inicial para el modo de señalización de publicidad y los resoltores de contenido (derivados de los metadatos de publicidad).
   * En `ContentPlacementCompletedListener`: Comprueba si `mediaPlayerClient` es `doneInitialResolving` antes de llamar a `endAdResolving`.

* `MediaPlayerClient`

   * Nuevo `List<ContentResolver> _contentResolvers`
   * Nuevo `int _reservations`
   * Nuevo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Busca qué resolución puede resolver el `PlacementOpportunity`.

   * Se ha modificado el código para crear varios solucionadores de contenido.
   * Nuevo `public boolean doneInitialResolving()`: Comprueba si quedan oportunidades por resolver.

* `VideoEngineTimeline`

   * Nuevo `removeContent(TimelineOperation timelineOperation)`: Quita un intervalo de contenido determinado de la cronología.
   * Nuevo `removeContentByLocalTime(long begin, long end)`: Elimina el contenido por hora local, dado `begin` y `end`.

* `DefaultOpportunityDetectorFactory` Modificado  `createOpportunityDetector`: Para los flujos de VOD, solo devuelve un valor nuevo  `SpliceOutOpportunityDetector` si no hay intervalos MARK o REPLACE (ya que dichos intervalos tienen prioridad sobre el modo de señalización).

