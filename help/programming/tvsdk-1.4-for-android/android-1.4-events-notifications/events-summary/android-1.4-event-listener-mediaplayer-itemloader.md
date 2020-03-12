---
description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
seo-description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
seo-title: Eventos de cargador
title: Eventos de cargador
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Eventos de cargador{#loader-events}

TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.

Estos eventos proporcionan un flujo de trabajo alternativo. No es necesario que implemente esta interfaz al crear un MediaPlayer. Utilícelo cuando desee tener un `MediaPlayerItemLoader`.

Para recibir notificaciones sobre los eventos relacionados con la carga de un recurso de reproductor multimedia, registre una implementación que `MediaPlayerItemLoader.LoaderListener` incluya los siguientes eventos.

| Evento | Significado |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | La carga de recursos multimedia se completó correctamente. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Se produjo un problema con la carga de recursos multimedia. |

>[!NOTE]
>
>Consulte también `onLoadInfo (loadInfo)` en Eventos de QoS.

