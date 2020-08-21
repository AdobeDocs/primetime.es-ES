---
description: 'Esta tabla proporciona información detallada sobre las notificaciones de optimización de ingresos. '
seo-description: 'Esta tabla proporciona información detallada sobre las notificaciones de optimización de ingresos. '
seo-title: Código de optimización de ingresos
title: Código de optimización de ingresos
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# Código de optimización de ingresos {#revenue-optimization-code}

Esta tabla proporciona información detallada sobre las notificaciones de OPTIMIZACIÓN de INGRESOS.

## Habilitar Sistema de informes de optimización de ingresos {#enable-revenue-optimization-reporting}

Para habilitar este sistema de informes, utilice la API de PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>La mayoría de las notificaciones informativas contienen metadatos relevantes, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

|Código |Nombre |Notificación interna |Claves de metadatos |Comentarios |
|—|—|—|—|—|
|401001 | REVENUE_OPTIMIZATION_SISTEMA DE INFORMES | Ninguno | Consulte la tabla siguiente para ver las claves de metadatos basadas en diferentes eventos. | Ninguno |

| Detalles del evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_INICIO** Se distribuye en TVSDK cuando se llama a MediaPlayer::replaceCurrentResource. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, evento, adSignalingMode, resourceUrl, creativeRepackageFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackEnabled mediaId, clientId |
| **CONTENT_PLAYBACK_INICIO** Se distribuye en TVSDK cuando el contenido ha entrado en el estado de preparación y está listo para la reproducción. Este evento no se enviará en cada carga de manifiesto; solo se enviará en la carga inicial. | clientTimestamp, contentURL, contentType, evento, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Se distribuye en TVSDK cuando se genera una oportunidad. | clientTimestamp, evento, idOportunidad, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_INICIO** Se distribuye en TVSDK cuando se empieza a resolver una oportunidad. | clientTimestamp, evento, idOportunidad, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** Se distribuye en TVSDK cuando una resolución de publicidad llama a MediaPlayerClient::notificationFailed(). Necesidad de completar los datos | OpportId, notificationAD |
| **AD_RESOURCE_LOAD** Se distribuye cuando la dirección URL recupera cualquier recurso de publicidad. responseStartTime:Unix marca de hora para cuándo se inició la solicitud por primera vez. responseTotalTime: cantidad total de tiempo (en segundos) que tardó una respuesta en cargarse. responseStatus: código de estado que se ha encontrado al recuperar el recurso. status: &quot;error&quot; o &quot;éxito&quot; referrerAdId: la identificación de publicidad de referencia que solicitó la recuperación de este recurso (si está presente). referrerUrl: la dirección URL de referencia que solicitó la recuperación de este recurso. errorMessage: si el estado es &quot;error&quot;, el motivo del error se encontrará aquí. | Opportid, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** Se distribuye en TVSDK cuando se aplica un CRS a un recurso, así como la respuesta para m3u8. resourceType:always &quot;crs&quot;. responseStartTime:Unix marca de hora para cuándo se inició la solicitud por primera vez. responseTotalTime: cantidad total de tiempo (en segundos) que tardó una respuesta en cargarse. responseStatus: código de estado que se ha encontrado al recuperar el recurso. status:&quot;error&quot; o &quot;éxito&quot;. errorMessage: si el estado es &quot;error&quot;, el motivo del error se encontrará aquí. mediaFileUrl: la dirección URL del archivo multimedia original que se seleccionó. mediaFileBitrate: la velocidad de bits del archivo multimedia seleccionado. mediaFileMimeType: El tipo de MIME del archivo multimedia seleccionado. url:URL final del recurso. | OpportId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Se distribuye en TVSDK después de colocar un adBreak en la línea de tiempo. Este evento se producirá una vez por cada pausa publicitaria. propuestoTime: la hora en la que se solicitó la pausa publicitaria. realTime: la hora en la que se colocó realmente la pausa publicitaria. propuestoDuration: la duración de la pausa publicitaria que se solicitó para la inserción. Para el contenido en directo, esta sería la duración de la señal. Para el contenido de VOD, normalmente sería -1. actualDuration: duración real del desglose de publicidad insertado. Se calcula como la duración de la suma de todas las publicidades, definida por sus duraciones de segmento respectivas, agregadas o sustituidas en la línea de tiempo del flujo original. anuncios propuestos: el número de anuncios en la pausa publicitaria propuesta. totalAds: el número de anuncios que se colocaron correctamente. publicidades...n:Las publicidades de inserción exitosas se insertarán aquí. Se puede recuperar toda la información del manifiesto de publicidad desde AD_OPPORTUNITY_RESOLVE_PROCESS | idOportunidad, estado, mensajeError, tiempoPropuesta, duraciónPropuesta, tiempoActual, duraciónActual, anunciosPropuestos, totalesPublicidades, idPublicidad, tipoPublicidad, duraciónPublicidad, dirección_url |
| **AD_PLAYBACK_INICIO** Se distribuye en TVSDK después de que un anuncio empiece a reproducirse. | clientTimestamp, evento, id, url, duration, type, OpportId, clientId |
| **AD_PLAYBACK_COMPLETE** Se distribuye en TVSDK una vez que un anuncio termina de reproducirse. | clientTimestamp, evento, id, url, duration, type, OpportId, clientId |
| **ADBREAK_PLAYBACK_INICIO** Se distribuye en TVSDK cuando se reproduce un inicio adbreak. | clientTimestamp, evento, idOportunidad, duración, hora, idCliente |
| **ADBREAK_PLAYBACK_COMPLETE** Se distribuye en TVSDK cuando se completa la reproducción de un adbreak. | clientTimestamp, evento, idOportunidad, idCliente |
| **CONTENT_PLAYBACK_COMPLETE** Se distribuye en TVSDK cuando se completa cualquier contenido. Esto puede ocurrir si se reemplaza el flujo, el reproductor introduce un estado de error, el reproductor se restaura o el contenido se completa. Este evento será necesario para rastrear un sessionId. | clientTimestamp, evento, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** Se distribuye en TVSDK cuando se reproduce un anuncio con un error (errores de flujo de variante). | evento, error, marca de tiempo, manifestUrl, hora, id de oportunidad, url |