---
description: Estos cambios en la API de Android TVSDK admiten eliminación y sustitución.
seo-description: Estos cambios en la API de Android TVSDK admiten eliminación y sustitución.
seo-title: Cambios en la API de reemplazo y eliminación de publicidad
title: Cambios en la API de reemplazo y eliminación de publicidad
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Cambios en la API de reemplazo y eliminación de publicidad{#ad-deletion-and-replacement-api-changes}

Estos cambios en la API de Android TVSDK admiten eliminación y sustitución.

* `AdSignalingMode` Nuevo modo personalizado de señalización de publicidad de intervalo de tiempo

* `AdvertisingMetadata` Nuevo  `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Establece los intervalos de tiempo para marcar, eliminar o reemplazar al procesar metadatos

* `ContentResolver`

   * Nuevo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nuevo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nueva clase `ContentRemoval`

   `TimelineOperation` clase que define el intervalo de tiempo que se va a eliminar de la línea de tiempo

* `AuditudeResolver`

   * Nuevo `private LinkedList<AuditudeRequest> _requestQueue`
   * Nuevo `void startConsumer()`: Inicios que procesan la cola de solicitudes de Primetime y toma de decisiones y se aseguran de que cada solicitud se emite a intervalos `MIN_INIT_REQUEST_INTERVAL`

   * Nuevo `processReplacementRange()`: Extrae intervalos de tiempo de los metadatos de publicidad y genera `PlacementInformations`, y crea una solicitud de toma de decisiones de publicidad Primetime que contiene `PlacementInformations`.

   * Nuevo `canDoResolver()`: Comprueba si la oportunidad de colocación tiene metadatos de primetime y decisioning

* Nueva `CustomRangeHelper` clase auxiliar que extrae metadatos de intervalo de tiempo de los metadatos de anuncio y elimina subconjuntos/superposiciones/intervalos de tiempo no válidos.

* Nueva `DeleteContentResolver` resolución de contenido que resuelve las oportunidades de colocación de `PlacementInformation.Mode.DELETE`

* Nueva `NopTimelineOperation` operación de la nueva línea de tiempo para cuando no se necesita reemplazar o colocar una pausa publicitaria. Esta clase se utiliza para distinguir entre esto y cuando se produce un error durante el proceso de resolución.

* `TimelineOperationQueue` Comprueba si la Operación de línea de tiempo es una operación  `NopTimelineOperation` antes de procesarla.

* `CustomAdMarkersContentResolver` Nuevo  `canDoResolve()`: Comprueba si una oportunidad de colocación es del tipo  `Mode.MARK`

* `MetadataResolver` Nuevo  `canDoResolve()`: Comprueba si una oportunidad de colocación es del tipo  `Mode.INSERT`

* `DefaultMetadataKeys` Nuevo  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nuevo modo `enum (INSERT, DELETE, REPLACE, MARK)`
   * Nuevo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Nuevo  `compareTo(TimeRange timeRange)`: Así se pueden ordenar los intervalos de tiempo en función del tiempo de inicio

* Nueva `ReplacementTimeRange` Amplía la clase `TimeRange` que representa un intervalo de tiempo de reemplazo, con un parámetro `begin`, `end` y `replacement-duration`.

* `TimeRangeCollection`

   * Nuevo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Se cambió el nombre `CUSTOM_AD_MARKERS` a `MARK_RANGES`

   * Se modificó `toMetadata(Metadata options)` para colocar los rangos delete/mark/replace en metadatos de publicidad.

* `MediaPlayerNotification`

   * Nuevo `UNDEFINED_TIME_RANGES`: Cuando el modo de señalización de publicidad es Mapa del servidor o Señales de manifiesto, y los rangos de reemplazo también están en los metadatos de publicidad, se omiten los rangos de reemplazo.
   * Nuevo `REPLACE_RANGES_NOT_AVAILABLE`: Cuando el modo de señalización de publicidad es Intervalos de tiempo personalizados y los rangos de reemplazo no están disponibles, se enviará una advertencia.

* `AdvertisingFactory` Nuevo  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nuevo  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nuevo  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * En `prepareToPlay()`: Realiza una búsqueda inicial a 0, ya que si se elimina el rango `[0,n]`, el reproductor multimedia no se reproducirá automáticamente.

   * En `prepareToPlay()`: Recorre la lista de información de colocación inicial para que `mediaplayerclient` se resuelva.

   * En `extractAdSignalingMode()`: Aloje el nuevo modo Intervalo de tiempo personalizado.
   * Nuevo `private static List<PlacementInformation> createInitalPlacementInformations()`: Genera la información de colocación inicial para el modo de señalización de publicidad y los solucionadores de contenido (derivados de metadatos de publicidad).
   * En `ContentPlacementCompletedListener`: Comprueba si `mediaPlayerClient` es `doneInitialResolving` antes de llamar a `endAdResolving`.

* `MediaPlayerClient`

   * Nuevo `List<ContentResolver> _contentResolvers`
   * Nuevo `int _reservations`
   * Nuevo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Busca qué resolución puede resolver el `PlacementOpportunity`.

   * Se ha modificado el código para crear varios solucionadores de contenido.
   * Nuevo `public boolean doneInitialResolving()`: Comprueba si quedan oportunidades por resolver.

* `VideoEngineTimeline`

   * Nuevo `removeContent(TimelineOperation timelineOperation)`: Quita un rango determinado de contenido de la línea de tiempo.
   * Nuevo `removeContentByLocalTime(long begin, long end)`: Elimina el contenido por hora local, dado `begin` y `end`.

* `DefaultOpportunityDetectorFactory` Modificado  `createOpportunityDetector`: Para los flujos VOD, solo devuelve un nuevo  `SpliceOutOpportunityDetector` si no hay intervalos MARK o REPLACE (ya que dichos intervalos tienen prioridad sobre el modo de señalización).

