---
description: MediaPlayerNotification proporciona información relacionada con el estado del reproductor.
title: Contenido de notificación
exl-id: dc46f717-f08b-4d52-82ea-88107076f4fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
