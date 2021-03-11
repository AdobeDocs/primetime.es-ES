---
description: TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación de los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.
title: Eventos de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Eventos de QoS{#qos-events}

TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación de los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.

Para recibir notificaciones sobre todos los eventos relacionados con QoS, registre los oyentes de eventos con el objeto `MediaPlayer` para los siguientes eventos:

| Evento | Significado |
|---|---|
| BufferEvent.[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | El almacenamiento en búfer ha finalizado. |
| BufferEvent.[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | Se ha iniciado el almacenamiento en búfer. |
| SeekEvent.[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | La llamada a otro punto del contenido ha finalizado. |
| SeekEvent.[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | La llamada a otro punto del contenido está empezando. |
| SeekEvent.[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK cambió la posición de búsqueda como resultado de las políticas de publicidad actuales. |

