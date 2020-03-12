---
description: TVSDK distribuye eventos de servicio de publicidad en respuesta a operaciones de metadatos temporizadas.
seo-description: TVSDK distribuye eventos de servicio de publicidad en respuesta a operaciones de metadatos temporizadas.
seo-title: Servicio de publicidad/eventos de metadatos temporizados
title: Servicio de publicidad/eventos de metadatos temporizados
uuid: fd50a937-0c9b-4c47-acb2-1ffc0592ad54
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Servicio de publicidad/eventos de metadatos temporizados{#ad-serving-timed-metadata-events}

TVSDK distribuye eventos de servicio de publicidad en respuesta a operaciones de metadatos temporizadas.

Para recibir notificaciones sobre todos estos eventos relacionados, registre los oyentes de eventos con el `MediaPlayer` objeto para los siguientes eventos.

| Evento | Significado |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Se procesaron metadatos temporizados de ID3. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | Se procesaron metadatos temporizados y no se detectó ninguna oportunidad. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Los metadatos temporizados están disponibles y no se detectó ninguna oportunidad. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Los metadatos temporizados se procesaron y no se detectó ninguna oportunidad en el manifiesto en segundo plano. |