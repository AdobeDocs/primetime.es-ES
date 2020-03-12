---
description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
seo-description: TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.
seo-title: Eventos de cargador
title: Eventos de cargador
uuid: 0ad37715-14b1-457c-892f-0db0d6220f0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventos de cargador{#loader-events}

TVSDK distribuye eventos de elementos del reproductor de medios como respuesta a la carga de un elemento de medios.

Estos eventos proporcionan un flujo de trabajo alternativo. No es necesario que implemente esta interfaz al crear una `MediaPlayer`. Utilícelo cuando desee tener un `MediaPlayerItemLoader`.

Para recibir notificaciones sobre eventos relacionados con la carga de un recurso de reproductor multimedia, registre los oyentes para los siguientes eventos con el `MediaPlayerItemLoader` objeto.

| Evento | Significado |
|---|---|
| MediaPlayerItemLoader.[completado](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | La carga de recursos multimedia se completó correctamente. |
| MediaPlayerItemLoader.[error](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Se produjo un problema con la carga de recursos multimedia. |