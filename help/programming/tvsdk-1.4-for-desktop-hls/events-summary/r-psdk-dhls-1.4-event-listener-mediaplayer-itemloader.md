---
description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
title: Eventos Loader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Loader events{#loader-events}

TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.

Estos eventos proporcionan un flujo de trabajo alternativo. No es necesario que implemente esta interfaz al crear un `MediaPlayer`. Utilícelo cuando desee tener un `MediaPlayerItemLoader`.

Para recibir notificaciones sobre eventos relacionados con la carga de un recurso de reproductor de contenidos, registre oyentes para los eventos siguientes con el objeto `MediaPlayerItemLoader` .

| Evento | Significado |
|---|---|
| MediaPlayerItemLoader.[complete](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | La carga de recursos multimedia se completó correctamente. |
| MediaPlayerItemLoader.[failed](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Se ha producido un problema con la carga de recursos multimedia. |