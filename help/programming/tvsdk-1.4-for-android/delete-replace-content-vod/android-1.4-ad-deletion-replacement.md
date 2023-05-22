---
description: Estos cambios en la API de TVSDK para Android admiten la eliminación y el reemplazo de.
title: Eliminación de anuncios y cambios de API de reemplazo
exl-id: bde8bd6e-0afe-42d0-b716-f33f75de757e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Eliminación de anuncios y cambios de API de reemplazo{#ad-deletion-and-replacement-api-changes}

Estos cambios en la API de TVSDK para Android admiten la eliminación y el reemplazo de.

* `AdSignalingMode` Nuevo modo de señalización de anuncio de intervalo de tiempo personalizado

* `AdvertisingMetadata` Nuevo `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: establece los intervalos de tiempo para marcar, eliminar o reemplazar al procesar metadatos

* `ContentResolver`

   * Nuevo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nuevo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nuevo `ContentRemoval` clase

   `TimelineOperation` que define el intervalo de tiempo que se va a eliminar de la cronología

* `AuditudeResolver`

   * Nuevo `private LinkedList<AuditudeRequest> _requestQueue`
   * Nuevo `void startConsumer()`: comienza a procesar la cola de solicitudes de Primetime y Decisioning y garantiza que cada solicitud se emita en `MIN_INIT_REQUEST_INTERVAL` intervalos

   * Nuevo `processReplacementRange()`: extrae intervalos de tiempo de los metadatos de publicidad y genera `PlacementInformations`y crea una solicitud de Primetime y Decisioning que contiene `PlacementInformations`.

   * Nuevo `canDoResolver()`: Comprueba si la oportunidad de ubicación tiene metadatos de Primetime y Decisioning

* Nuevo `CustomRangeHelper` Clase de ayuda que extrae metadatos de intervalo de tiempo de los metadatos de publicidad y elimina subconjuntos, superposiciones o intervalos de tiempo no válidos.

* Nuevo `DeleteContentResolver` Resolución de contenido que resuelve las oportunidades de colocación de `PlacementInformation.Mode.DELETE`

* Nuevo `NopTimelineOperation` Nueva operación de cronología para los casos en los que no es necesario realizar ninguna colocación o sustitución de pausa publicitaria. Esta clase se utiliza para distinguir entre esto y cuando se produce un error durante el proceso de resolución.

* `TimelineOperationQueue` Comprueba si la operación de cronología es una `NopTimelineOperation` antes de procesar.

* `CustomAdMarkersContentResolver` Nuevo `canDoResolve()`: comprueba si una oportunidad de ubicación es del tipo `Mode.MARK`

* `MetadataResolver` Nuevo `canDoResolve()`: comprueba si una oportunidad de ubicación es del tipo `Mode.INSERT`

* `DefaultMetadataKeys` Nuevo `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nuevo modo `enum (INSERT, DELETE, REPLACE, MARK)`
   * Nuevo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Nuevo `compareTo(TimeRange timeRange)`: Puede ordenar intervalos de tiempo según la hora de inicio

* Nuevo `ReplacementTimeRange` Amplía el `TimeRange` que representa un intervalo de tiempo de reemplazo, con una clase `begin`, `end`, y `replacement-duration` parámetro.

* `TimeRangeCollection`

   * Nuevo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Cambiando nombre `CUSTOM_AD_MARKERS` hasta `MARK_RANGES`

   * Modificado `toMetadata(Metadata options)` para incluir rangos de eliminación/marca/reemplazo en los metadatos de publicidad.

* `MediaPlayerNotification`

   * Nuevo `UNDEFINED_TIME_RANGES`: Cuando el modo de señalización de anuncio es Mapa del servidor o Señales de manifiesto y los intervalos de reemplazo también están en los metadatos de anuncio, se omiten los intervalos de reemplazo.
   * Nuevo `REPLACE_RANGES_NOT_AVAILABLE`: Cuando el modo de señalización de anuncio es Intervalos de tiempo personalizados y los intervalos de reemplazo no están disponibles, se envía una advertencia.

* `AdvertisingFactory` Nuevo `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nuevo `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nuevo `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * Entrada `prepareToPlay()`: realiza una búsqueda inicial en 0, ya que si el intervalo `[0,n]` se elimina, el reproductor de contenidos no se reproducirá automáticamente.

   * Entrada `prepareToPlay()`: Realiza un bucle en la lista de información de ubicación inicial de `mediaplayerclient` para resolver.

   * Entrada `extractAdSignalingMode()`: acepte el nuevo modo de intervalo de tiempo personalizado.
   * Nuevo `private static List<PlacementInformation> createInitalPlacementInformations()`: genera la información de ubicación inicial para el modo de señalización de publicidad y los solucionadores de contenido (derivados de los metadatos de publicidad).
   * Entrada `ContentPlacementCompletedListener`: comprueba si `mediaPlayerClient` es `doneInitialResolving` antes de llamar a `endAdResolving`.

* `MediaPlayerClient`

   * Nuevo `List<ContentResolver> _contentResolvers`
   * Nuevo `int _reservations`
   * Nuevo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Busca el solucionador que puede resolver el problema `PlacementOpportunity`.

   * Se ha modificado el código para crear varias resoluciones de contenido.
   * Nuevo `public boolean doneInitialResolving()`: comprueba si quedan oportunidades por resolver.

* `VideoEngineTimeline`

   * Nuevo `removeContent(TimelineOperation timelineOperation)`: elimina un intervalo determinado de contenido de la cronología.
   * Nuevo `removeContentByLocalTime(long begin, long end)`: elimina el contenido según la hora local dada `begin` y `end`.

* `DefaultOpportunityDetectorFactory` Modificado `createOpportunityDetector`: para flujos de VOD, solo devuelve un nuevo `SpliceOutOpportunityDetector` si no hay rangos MARK o REPLACE (ya que esos rangos tienen prioridad sobre el modo de señalización).
