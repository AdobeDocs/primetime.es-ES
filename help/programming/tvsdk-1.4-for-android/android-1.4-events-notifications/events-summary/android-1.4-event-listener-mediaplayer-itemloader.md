---
description: TVSDK envía eventos de elementos del reproductor de medios en respuesta a la carga de un elemento de medios.
title: Eventos de cargador
exl-id: 80a503f2-ad2e-44e5-93dc-2311df77f52e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Eventos de cargador{#loader-events}

TVSDK envía eventos de elementos del reproductor de medios en respuesta a la carga de un elemento de medios.

Estos eventos proporcionan un flujo de trabajo alternativo. No es necesario que implemente esta interfaz al crear un MediaPlayer. Utilice esta opción cuando desee tener un `MediaPlayerItemLoader`.

Para recibir notificaciones acerca de eventos relacionados con la carga de un recurso de reproductor de contenidos, registre una implementación de `MediaPlayerItemLoader.LoaderListener` incluidos los eventos siguientes.

| Evento | Significado |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | La carga de medios se completó correctamente. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Se ha producido un problema con la carga de medios. |

>[!NOTE]
>
>Consulte también `onLoadInfo (loadInfo)` en eventos de QoS.
