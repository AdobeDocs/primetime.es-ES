---
description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
seo-description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
seo-title: Eventos del cargador
title: Eventos del cargador
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Eventos del cargador{#loader-events}

TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.

Estos eventos proporcionan un flujo de trabajo alternativo. No es necesario que implemente esta interfaz al crear un MediaPlayer. Utilícelo cuando desee tener un `MediaPlayerItemLoader`.

Para recibir notificaciones sobre eventos relacionados con la carga de un recurso de reproductor de medios, registre una implementación de `MediaPlayerItemLoader.LoaderListener` que incluya los siguientes eventos.

| Evento | Significado |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) mediaPlayerItemplayerItem) | La carga de recursos multimedia se completó correctamente. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Se produjo un problema con la carga de recursos multimedia. |

>[!NOTE]
>
>Consulte también `onLoadInfo (loadInfo)` en eventos de QoS.

