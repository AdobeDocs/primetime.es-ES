---
description: Todos los reproductores de vídeo deben proporcionar funciones en las que el servidor de manifiesto confía para insertar anuncios y habilitar el seguimiento de anuncios.
seo-description: Todos los reproductores de vídeo deben proporcionar funciones en las que el servidor de manifiesto confía para insertar anuncios y habilitar el seguimiento de anuncios.
seo-title: Requisitos del reproductor de vídeo
title: Requisitos del reproductor de vídeo
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Requisitos del reproductor de vídeo {#video-player-requirements}

Todos los reproductores de vídeo deben proporcionar funciones en las que el servidor de manifiesto confía para insertar anuncios y habilitar el seguimiento de anuncios.

Para utilizar la API de inserción de anuncios Primetime, un reproductor de vídeo debe satisfacer lo siguiente:

* Puede rastrear la posición del cursor de reproducción a medida que se reproduce el contenido.
* Puede solicitar direcciones URL de seguimiento en los momentos especificados.
* Se ejecuta en una plataforma de dispositivo compatible con HLS v3 o posterior, que incluye:

   * Interrupciones de PTS marcadas con etiquetas `EXT-X-DISCONTINUITY`
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Se ejecuta en una plataforma que admite redirecciones HTTP y análisis de JSON.
* Los reproductores basados en Web deben ejecutarse en plataformas compatibles con CORS.