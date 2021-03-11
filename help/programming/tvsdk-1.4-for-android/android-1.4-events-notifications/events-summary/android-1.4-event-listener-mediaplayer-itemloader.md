---
description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
title: Eventos Loader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Loader events{#loader-events}

TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.

Estos eventos proporcionan un flujo de trabajo alternativo. No es necesario que implemente esta interfaz al crear un MediaPlayer. Utilícelo cuando desee tener un `MediaPlayerItemLoader`.

Para recibir notificaciones sobre eventos relacionados con la carga de un recurso de reproductor de medios, registre una implementación de `MediaPlayerItemLoader.LoaderListener` que incluya los siguientes eventos.

| Evento | Significado |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) mediaPlayerPackageItem) | La carga de recursos multimedia se completó correctamente. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Se ha producido un problema con la carga de recursos multimedia. |

>[!NOTE]
>
>Consulte también `onLoadInfo (loadInfo)` en los eventos de QoS.

