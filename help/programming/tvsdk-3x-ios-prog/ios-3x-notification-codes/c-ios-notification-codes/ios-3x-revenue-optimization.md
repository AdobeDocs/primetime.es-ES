---
description: Esta tabla proporciona información detallada sobre las notificaciones de optimización de ingresos.
title: Código de optimización de ingresos
exl-id: 3657ba70-ec35-495b-ae7b-4198429bdf6a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Código de optimización de ingresos {#revenue-optimization-code}

Esta tabla proporciona información detallada sobre las notificaciones de OPTIMIZACIÓN DE INGRESOS.

## Habilitar informes de optimización de ingresos {#enable-revenue-optimization-reporting}

Para habilitar este sistema de informes, utilice la API de PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>La mayoría de las notificaciones informativas contienen metadatos relevantes como, por ejemplo, la dirección URL del recurso que no se ha podido descargar. Algunas notificaciones contienen metadatos para especificar si el problema se produjo en el contenido del vídeo principal, en el contenido de audio alternativo o en un anuncio.

| Código | Nombre | Notificación interna | Claves de metadatos | Comentarios |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | Ninguno | Consulte la tabla siguiente para obtener claves de metadatos basadas en diferentes eventos. | Ninguno |

| Detalles del evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** Se distribuye en TVSDK cuando se llama a MediaPlayer::replaceCurrentResource. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackersFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackingsEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** Se envía en TVSDK cuando el contenido ha entrado en el estado preparado y está listo para reproducirse. Este evento no se enviará en cada carga de manifiesto; solo se enviará en la carga inicial. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Se envía en TVSDK cuando se genera una oportunidad. | clientTimestamp, event, OpportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** Se envía en TVSDK cuando una oportunidad empieza a resolverse. | clientTimestamp, event, OpportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** Se envía en TVSDK cuando un solucionador de anuncios llama a MediaPlayerClient::notifyFailed(). Necesita rellenar los datos | OpportunityId, notificationAD |
| **AD_RESOURCE_LOAD** Se envía cuando la dirección URL recupera cualquier recurso publicitario. responseStartTime: marca de tiempo Unix para cuándo se inició la solicitud por primera vez. responseTotalTime: Cantidad total de tiempo (en segundos) que tardó una respuesta en cargarse. responseStatus: código de estado encontrado al recuperar el recurso. status:&quot;error&quot; o &quot;success&quot; referrerAdId: ID del anuncio de referencia que solicitó la recuperación de este recurso (si está presente). referrerUrl: Dirección URL de referencia que solicitó recuperar este recurso. errorMessage: Si el estado es &quot;error&quot;, el motivo del error se encuentra aquí. | OpportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** Se envía en TVSDK cuando se aplica un CRS a un recurso, así como la respuesta para m3u8. resourceType: siempre &quot;crs&quot;. responseStartTime: marca de tiempo Unix para cuándo se inició la solicitud por primera vez. responseTotalTime: Cantidad total de tiempo (en segundos) que tardó una respuesta en cargarse. responseStatus: código de estado encontrado al recuperar el recurso. estado: &quot;error&quot; o &quot;success&quot;. errorMessage: Si el estado es &quot;error&quot;, el motivo del error se encuentra aquí. mediaFileUrl: URL del archivo multimedia original seleccionado. mediaFileBitrate: velocidad de bits del archivo multimedia seleccionado. mediaFileMimeType: tipo MIME del archivo multimedia seleccionado. url: La URL final del recurso. | OpportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Se envía en TVSDK después de que se coloque un AdBreak en la cronología. Este evento se produce una vez por cada pausa publicitaria. posedTime: hora a la que se solicitó colocar la pausa publicitaria. actualTime: hora a la que se colocó realmente la pausa publicitaria. posedDuration: Duración de la pausa publicitaria solicitada para la inserción. Para el contenido en directo, esta sería la duración de referencia. Para el contenido de VOD, normalmente sería -1. actualDuration: Duración real de la pausa publicitaria insertada. Se calcula como la duración total de todos los anuncios, definida por sus respectivas duraciones de segmento, añadidos o reemplazados en la cronología del flujo original. Anuncios propuestos: El número de anuncios de la pausa publicitaria propuesta. totalAds: número de anuncios que se han colocado correctamente. ads...n: Los anuncios insertados correctamente se insertan aquí. Se puede recuperar toda la información de manifiesto de anuncio desde AD_OPPORTUNITY_RESOLVE_PROCESS | OpportunityId, status, errorMessage, posedTime, posedDuration, actualTime, actualDuration, posedAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** Se envía en TVSDK después de que comience la reproducción de un anuncio. | clientTimestamp, event, id, url, duration, type, OpportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** Se envía en TVSDK después de que se complete la reproducción de un anuncio. | clientTimestamp, event, id, url, duration, type, OpportunityId, clientId |
| **ADBREAK_PLAYBACK_START** Se envía en TVSDK cuando se inicia la reproducción de un AdBreak. | clientTimestamp, event, OpportunityId, duration, time, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** Se envía en TVSDK cuando un AdBreak termina de reproducirse. | clientTimestamp, event, OpportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** Se envía en TVSDK cuando se completa cualquier contenido. Esto puede ocurrir si se reemplaza el flujo, el reproductor entra en un estado de error, el reproductor se restablece o el contenido se completa. Este evento es necesario para realizar el seguimiento de un sessionId. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** Se envía en TVSDK cuando un anuncio tiene un error de reproducción (errores de flujo de variante). | evento, error, marca de tiempo, manifestUrl, hora, OpportunityId, url |
