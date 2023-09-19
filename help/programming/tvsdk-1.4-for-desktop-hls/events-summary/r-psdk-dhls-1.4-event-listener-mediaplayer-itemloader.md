---
description: TVSDK envía eventos de elementos del reproductor de medios en respuesta a la carga de un elemento de medios.
title: Eventos de cargador
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Eventos de cargador{#loader-events}

TVSDK envía eventos de elementos del reproductor de medios en respuesta a la carga de un elemento de medios.

Estos eventos proporcionan un flujo de trabajo alternativo. No es necesario implementar esta interfaz al crear una `MediaPlayer`. Utilice esta opción cuando desee tener un `MediaPlayerItemLoader`.

Para recibir notificaciones acerca de eventos relacionados con la carga de un recurso de reproductor de contenidos, registre oyentes para los siguientes eventos con el `MediaPlayerItemLoader` objeto.

| Evento | Significado |
|---|---|
| MediaPlayerItemLoader.[completado](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | La carga de medios se completó correctamente. |
| MediaPlayerItemLoader.[error](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Se ha producido un problema con la carga de medios. |
