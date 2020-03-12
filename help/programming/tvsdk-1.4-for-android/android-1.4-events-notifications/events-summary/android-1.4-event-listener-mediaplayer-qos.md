---
description: TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.
seo-description: TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.
seo-title: Eventos de QoS
title: Eventos de QoS
uuid: 27f60cd3-d3fc-4ea3-81df-96d0fe9f7068
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Eventos de QoS{#qos-events}

TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.

Para recibir notificaciones sobre todos los eventos relacionados con QoS, registre una implementación que `MediaPlayer.QOSEventListener` incluya las siguientes rellamadas:

| Evento | Significado |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | Se completó el almacenamiento en búfer. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Se ha iniciado el almacenamiento en búfer. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | Un fragmento se ha descargado correctamente. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification. [Advertencia](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) ) | Se ha producido un error recuperable. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long setTime) | La búsqueda ha finalizado. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | La búsqueda está empezando. |