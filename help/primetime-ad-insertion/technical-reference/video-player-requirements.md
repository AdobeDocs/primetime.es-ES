---
description: Todos los reproductores de vídeo deben proporcionar funciones en las que el servidor de manifiesto confía para insertar anuncios y habilitar el seguimiento de anuncios.
title: Requisitos del reproductor de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Requisitos del reproductor de vídeo {#video-player-requirements}

Todos los reproductores de vídeo deben proporcionar funciones en las que el servidor de manifiesto confía para insertar anuncios y habilitar el seguimiento de anuncios.

Para utilizar la API de inserción de anuncios de Primetime, un reproductor de vídeo debe cumplir lo siguiente:

* Puede rastrear la posición del cabezal de reproducción cuando el contenido se reproduce.
* Puede solicitar direcciones URL de seguimiento en el momento especificado.
* Se ejecuta en una plataforma de dispositivo compatible con HLS v3 o posterior, que incluye:

   * Interrupciones de PTS marcadas con etiquetas `EXT-X-DISCONTINUITY`
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Se ejecuta en una plataforma que admite redirecciones HTTP y el análisis de JSON.
* Los reproductores basados en web deben ejecutarse en plataformas compatibles con CORS.