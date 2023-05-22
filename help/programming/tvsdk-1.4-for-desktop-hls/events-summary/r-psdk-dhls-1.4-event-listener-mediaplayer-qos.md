---
description: TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la llamada a otro punto del contenido.
title: Eventos de QoS
exl-id: 7de28d00-12e2-4f2a-bb1b-53661e3578a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Eventos de QoS{#qos-events}

TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la llamada a otro punto del contenido.

Para recibir notificaciones acerca de todos los eventos relacionados con QoS, registre detectores de eventos en `MediaPlayer` para los eventos siguientes:

| Evento | Significado |
|---|---|
| BufferEvent.[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | Se ha completado el almacenamiento en búfer. |
| BufferEvent.[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | Se ha iniciado el almacenamiento en búfer. |
| SeekEvent.[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | La búsqueda se ha completado. |
| SeekEvent.[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | La búsqueda está empezando. |
| SeekEvent.[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK cambió la posición de búsqueda como resultado de las políticas de publicidad actuales. |
