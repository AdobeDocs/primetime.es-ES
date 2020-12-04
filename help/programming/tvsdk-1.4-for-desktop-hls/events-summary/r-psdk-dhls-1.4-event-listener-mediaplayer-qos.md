---
description: TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.
seo-description: TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.
seo-title: Eventos de QoS
title: Eventos de QoS
uuid: fd657cf0-c6d4-4e9a-b212-7d09d483cae9
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Eventos de QoS{#qos-events}

TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.

Para recibir notificaciones sobre todos los eventos relacionados con QoS, registre los oyentes de eventos con el objeto `MediaPlayer` para los siguientes eventos:

| Evento | Significado |
|---|---|
| BufferEvent.[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | Se completó el almacenamiento en búfer. |
| BufferEvent.[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | Se ha iniciado el almacenamiento en búfer. |
| SeekEvent.[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | La búsqueda ha finalizado. |
| SeekEvent.[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | La búsqueda está empezando. |
| SeekEvent.[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK ha cambiado la posición de búsqueda como resultado de las políticas de publicidad actuales. |

