---
description: MediaPlayerNotification proporciona información relacionada con el estado del reproductor.
title: Contenido de notificación
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Contenido de notificación{#notification-content}

MediaPlayerNotification proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de `MediaPlayerNotification` notificaciones. Cada notificación contiene la siguiente información:

* Marca de tiempo
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * escriba INFO, WARN o ERROR
   * `code`: una representación numérica de la notificación.
   * `name`: una descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`: Pares de clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`: una referencia a otra `MediaPlayerNotification` que afecta directamente a esta notificación.

Puede almacenar esta información localmente para su posterior análisis o enviarla a un servidor remoto para su registro y representación gráfica.
