---
description: Todos los reproductores de vídeo deben proporcionar funciones en las que se basa el servidor de manifiesto para insertar anuncios y habilitar el seguimiento de anuncios.
title: Requisitos del reproductor de vídeo
exl-id: 23134e4c-6902-4b97-bf15-4524f47850e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
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
* Los reproductores basados en web deben ejecutarse en plataformas compatibles con CORS.
