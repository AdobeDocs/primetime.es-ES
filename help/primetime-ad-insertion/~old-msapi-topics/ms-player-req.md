---
description: Todos los reproductores de vídeo deben proporcionar funciones en las que el servidor de manifiesto confía para insertar anuncios y habilitar el seguimiento de anuncios.
seo-description: Todos los reproductores de vídeo deben proporcionar funciones en las que el servidor de manifiesto confía para insertar anuncios y habilitar el seguimiento de anuncios.
seo-title: Requisitos del reproductor de vídeo
title: Requisitos del reproductor de vídeo
uuid: 29593d67-2901-4d9e-a08f-23c8a7667283
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '136'
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
* Se ejecuta en una plataforma que admite CORS.