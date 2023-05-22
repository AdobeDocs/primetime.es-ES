---
description: TVSDK envía eventos de elementos del reproductor de medios en respuesta a la carga de un elemento de medios.
title: Eventos de cargador
exl-id: ee5be2d4-5c77-4af4-b8fe-8cef18d7c0d9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
