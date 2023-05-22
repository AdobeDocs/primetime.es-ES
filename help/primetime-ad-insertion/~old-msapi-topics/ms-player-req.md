---
description: Todos los reproductores de vídeo deben proporcionar funciones en las que se basa el servidor de manifiesto para insertar anuncios y habilitar el seguimiento de anuncios.
title: Requisitos del reproductor de vídeo
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Requisitos del reproductor de vídeo {#video-player-requirements}

Todos los reproductores de vídeo deben proporcionar funciones en las que se basa el servidor de manifiesto para insertar anuncios y habilitar el seguimiento de anuncios.

Para utilizar la API de inserción de anuncios de Primetime, un reproductor de vídeo debe cumplir los siguientes requisitos:

* Puede rastrear la posición del cabezal de reproducción a medida que se reproduce el contenido.
* Puede solicitar direcciones URL de seguimiento en el momento especificado.
* Se ejecuta en una plataforma de dispositivo compatible con HLS v3 o posterior, que incluye:

   * Discontinuidades de PTS marcadas por `EXT-X-DISCONTINUITY` etiquetas
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Se ejecuta en una plataforma que admite redirecciones HTTP y análisis de JSON.
* Funciona en una plataforma que admite CORS.