---
description: 'Esta tabla proporciona información detallada sobre las notificaciones de optimización de ingresos. '
title: Código de optimización de los ingresos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# Código de optimización de ingresos {#revenue-optimization-code}

Esta tabla proporciona información detallada sobre las notificaciones de OPTIMIZACIÓN de INGRESOS.

## Habilitar los informes de optimización de ingresos {#enable-revenue-optimization-reporting}

Para habilitar este informe, use la api de PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>La mayoría de las notificaciones informativas contienen metadatos relevantes, por ejemplo, la dirección URL del recurso que no se pudo descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

| Código | Nombre | Notificación interna | Claves de metadatos | Comentarios |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | Ninguna | Consulte la siguiente tabla para obtener claves de metadatos basadas en diferentes eventos. | Ninguna |

| Detalles del evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_** STARTDispatched en TVSDK cuando se llama a MediaPlayer::replaceCurrentResource . | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackagingEnabled, Id, clientId |
| **CONTENT_PLAYBACK_** STARTDispatched en TVSDK cuando el contenido ha entrado en el estado preparado y está listo para la reproducción. Este evento no se envía en cada carga de manifiesto; solo se envía en la carga inicial. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_** GENERATEDDispatched en TVSDK cuando se genera una oportunidad. | clientTimestamp, evento, idOportunidad, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** STARTDispatched en TVSDK cuando una oportunidad empieza a resolverse. | clientTimestamp, evento, idOportunidad, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** FAILEDDispatched en TVSDK cuando una resolución de anuncio llama a MediaPlayerClient::notifyFailed(). Necesidad de rellenar los datos | idOportunidad, idNotificación |
| **AD_RESOURCE_** LOADDispatched cuando la dirección URL recupera cualquier recurso publicitario. responseStartTime:Unix marca de tiempo para cuándo se inició la solicitud por primera vez. responseTotalTime: Cantidad total de tiempo (en segundos) que tardó una respuesta en cargarse. responseStatus: código de estado que se encuentra al recuperar el recurso. status: referrerAdId de &quot;error&quot; o &quot;éxito&quot;: el id de anuncio de referencia que solicitó la recuperación de este recurso (si está presente). referrerUrl: la dirección url de referencia que solicitó la recuperación de este recurso. errorMessage:Si el estado es &quot;error&quot;, el motivo del error se encuentra aquí. | offerId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_** CRSDispatched en TVSDK cuando se aplica un CRS a un recurso, así como la respuesta para m3u8. resourceType:always &quot;crs&quot;. responseStartTime:Unix marca de tiempo para cuándo se inició la solicitud por primera vez. responseTotalTime: Cantidad total de tiempo (en segundos) que tardó una respuesta en cargarse. responseStatus: código de estado que se encuentra al recuperar el recurso. estado: &quot;error&quot; o &quot;éxito&quot;. errorMessage:Si el estado es &quot;error&quot;, el motivo del error se encuentra aquí. mediaFileUrl: la URL del archivo multimedia original que se seleccionó. mediaFileBitrate: velocidad de bits del archivo multimedia seleccionado. mediaFileMimeType: Tipo mime del archivo multimedia seleccionado. url:La dirección url final del recurso. | offerId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_** PLACEDispatched en TVSDK después de colocar un adBreak en la cronología. Este evento se producirá una vez para cada pausa publicitaria. offerTime: Hora a la que se solicitó la pausa publicitaria. realTime: la hora a la que se colocó realmente la pausa publicitaria. requiredDuration: duración de la pausa publicitaria que se solicitó para su inserción. Para el contenido en directo, esta sería la duración de referencia. Para el contenido de VOD, normalmente sería -1. realDuration: duración real de la pausa publicitaria insertada. Se calcula como la duración de la suma de todos los anuncios, definida por sus respectivas duraciones de segmento, añadidos o reemplazados en la cronología de flujo original. anuncios propuestos: el número de anuncios en la pausa publicitaria propuesta. totalAds: el número de anuncios que se colocaron correctamente. anuncios..n: Los anuncios insertados correctamente se insertarán aquí. Toda la información del manifiesto de anuncio se puede recuperar desde AD_OPPORTUNITY_RESOLVE_PROCESS | idOportunidad, estado, errorMessage, tiempoPropuesta, duraciónPropuesta, tiempoActual, duraciónActual, anunciosPropuestos, anunciosTotales, ad_id, ad_type, ad_duration, ad_url |
| **AD_PLAYBACK_** STARTDispatched en TVSDK después de que un anuncio comience la reproducción. | clientTimestamp, evento, id, url, duración, tipo, id de oportunidad, clientId |
| **AD_PLAYBACK_** COMPLETEDispatched en TVSDK después de que un anuncio termina de reproducirse. | clientTimestamp, evento, id, url, duración, tipo, id de oportunidad, clientId |
| **ADBREAK_PLAYBACK_** STARTDispatched en TVSDK cuando un adbreak inicia la reproducción. | clientTimestamp, evento, idOportunidad, duración, tiempo, clientId |
| **ADBREAK_PLAYBACK_** COMPLETEDispatched en TVSDK cuando una pausa publicitaria termina de reproducirse. | clientTimestamp, evento, oportunidadId, clientId |
| **CONTENT_PLAYBACK_** COMPLETEDispatched en TVSDK cuando se completa cualquier contenido. Esto puede ocurrir si se reemplaza la emisión, el reproductor entra en estado de error, el reproductor se restablece o el contenido se completa. Este evento será necesario para rastrear un sessionId. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_** ERRORDispatched en TVSDK cuando se reproduce un anuncio con un error (errores de flujo de variante). | evento, error, marca de tiempo, manifestUrl, tiempo, id de oportunidad, url |
