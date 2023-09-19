---
description: TVSDK envía eventos de servicio de anuncios en respuesta a operaciones de metadatos temporizadas.
title: Eventos de metadatos cronometrados/para servicio de anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Eventos de metadatos cronometrados/para servicio de anuncios{#ad-serving-timed-metadata-events}

TVSDK envía eventos de servicio de anuncios en respuesta a operaciones de metadatos temporizadas.

Para recibir notificaciones sobre todos estos eventos relacionados, registre detectores de eventos en `MediaPlayer` para los eventos siguientes.

| Evento | Significado |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Se ha procesado un metadato temporizado ID3. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | Se ha procesado un metadato cronometrado y no se ha detectado ninguna oportunidad. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Los metadatos cronometrados están disponibles y no se ha detectado ninguna oportunidad. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Se procesaron los metadatos cronometrados y no se detectó ninguna oportunidad en el manifiesto en segundo plano. |
