---
description: TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación de los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.
title: Eventos de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Eventos de QoS{#qos-events}

TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación de los eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer o la búsqueda.

Para recibir notificaciones sobre todos los eventos relacionados con QoS, registre una implementación de `MediaPlayer.QOSEventListener` que incluya las siguientes llamadas de retorno:

| Evento | Significado |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | El almacenamiento en búfer ha finalizado. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Se ha iniciado el almacenamiento en búfer. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo)) (loadInfo) | Un fragmento se ha descargado correctamente. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html) (MediaPlayerNotification. [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) Advertencia) | Se ha producido un error recuperable. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long)) (long setTime ajustado) | La llamada a otro punto del contenido ha finalizado. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | La llamada a otro punto del contenido está empezando. |