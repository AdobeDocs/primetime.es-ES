---
description: TVSDK envía eventos de servicio de publicidad en respuesta a operaciones de metadatos temporizadas.
title: Eventos de servicio de publicidad/metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Eventos de metadatos temporizados/servicio de publicidad{#ad-serving-timed-metadata-events}

TVSDK envía eventos de servicio de publicidad en respuesta a operaciones de metadatos temporizadas.

Para recibir notificaciones sobre todos estos eventos relacionados, registre los oyentes de eventos con el objeto `MediaPlayer` para los siguientes eventos.

| Evento | Significado |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Se procesaron metadatos temporizados de ID3. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | Se procesaron metadatos temporizados y no se detectó ninguna oportunidad. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Los metadatos temporizados están disponibles y no se ha detectado ninguna oportunidad. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Se procesaron metadatos temporizados y no se detectó ninguna oportunidad en el manifiesto de fondo. |