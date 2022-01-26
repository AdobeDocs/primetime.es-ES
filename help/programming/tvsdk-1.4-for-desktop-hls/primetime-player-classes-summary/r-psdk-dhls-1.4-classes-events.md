---
description: Estas clases describen eventos que el SDK de TVSDK envía al reproductor de medios como respuesta a varias actividades.
title: Clases de eventos
exl-id: a349984a-5e47-4895-a56f-ef25eb372c79
source-git-commit: 776d3d1668f063f1595bd3ecb53603171905014a
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Clases de eventos {#events-classes}

Estas clases describen eventos que el SDK de TVSDK envía al reproductor de medios como respuesta a varias actividades.

Paquete: [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| Nombre | Significado |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | Clase. Se ha iniciado o completado una pausa publicitaria. |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | Clase. El usuario hizo clic en un anuncio. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | Clase. El reproductor reprodujo un anuncio. |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | Clase. El reproductor inició o detuvo el almacenamiento en búfer. |
| [CustomAdEvent](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-1-4-for-desktop-hls/advertising/custom-ads/r-psdk-dhls-1.4-custom-ad-events.html?lang=en) | Clase. El reproductor muestra el estado de carga de la publicidad personalizada y puede ignorar las publicidades que tienen errores o que tardan demasiado en cargarse. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | Clase. Los nuevos metadatos DRM están asociados con el elemento actual. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | Clase. La información de descarga está disponible para el flujo de medios actual que se está reproduciendo. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | Clase. Se ha creado un elemento del reproductor de contenidos. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | Clase. Se ha completado una operación de carga. Enviado por `MediaPlayerItemLoader` para notificar a sus clientes. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | Clase. Se ha cambiado el estado del reproductor de contenidos. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | Clase. La variable `MediaPlayerView` se ha hecho clic. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | Clase. La velocidad de reproducción del reproductor de contenidos cambia. |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | Clase. El algoritmo de conmutación de velocidad de bits adaptable del reproductor de medios ha cambiado a otro perfil debido a condiciones de red o de equipo. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | Clase. El reproductor empezó a buscar o la operación de búsqueda se completó. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | Clase. El tamaño del vídeo está disponible. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | Clase. Se ha cambiado el estado del reproductor de contenidos. |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | Clase. El detector de oportunidades procesa los metadatos temporizados. |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | Clase. La cronología del reproductor de contenidos ha cambiado. |
