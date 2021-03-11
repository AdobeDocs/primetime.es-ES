---
description: MediaPlayerNotification proporciona información relacionada con el estado del reproductor.
title: Contenido de la notificación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Contenido de notificación{#notification-content}

MediaPlayerNotification proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de notificaciones `MediaPlayerNotification`. Cada notificación contiene la siguiente información:

* Marca de tiempo
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * escriba INFO, WARN o ERROR
   * `code`: Una representación numérica de la notificación.
   * `name`: Una descripción de la notificación legible en lenguaje natural, como SEEK_ERROR
   * `metadata`: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`: Referencia a otro  `MediaPlayerNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información localmente para análisis posteriores o enviarla a un servidor remoto para el registro y la representación gráfica.
