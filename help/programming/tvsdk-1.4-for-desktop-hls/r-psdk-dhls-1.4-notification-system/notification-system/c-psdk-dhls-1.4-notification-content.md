---
description: MediaPlayerNotification proporciona información relacionada con el estado del reproductor.
seo-description: MediaPlayerNotification proporciona información relacionada con el estado del reproductor.
seo-title: Contenido de notificación
title: Contenido de notificación
uuid: c2321a49-1b60-4e44-b8e2-a023b764d779
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Contenido de notificación{#notification-content}

MediaPlayerNotification proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de `MediaPlayerNotification` notificaciones. Cada notificación contiene la siguiente información:

* Marca de hora
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * escriba INFO, WARN o ERROR
   * `code`:: Una representación numérica de la notificación.
   * `name`:: Descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`:: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave llamada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`:: Referencia a otro `MediaPlayerNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información de forma local para analizarla posteriormente o enviarla a un servidor remoto para que registre y muestre una representación gráfica.
