---
description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-title: Trabajo con subtítulos opcionales
title: Trabajo con subtítulos opcionales
uuid: 6e105316-a166-45c1-b6b0-70c89c97c297
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Información general {#work-with-closed-captions-overview}

Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.

Los subtítulos cerrados suelen estar en el mismo idioma que el audio y también muestran sonidos de fondo como texto, pero los subtítulos suelen estar en un idioma diferente y no incluyen sonidos de fondo.

TVSDK admite la representación de estos formatos:

* Subtítulos opcionales 608 y 708, cuando se envían como parte del flujo de transporte de vídeo a través de HLS como paquetes de datos en flujos de vídeo MPEG-2.
* Archivos de subtítulos WebVTT a los que se hace referencia desde los archivos de manifiesto M3U8 tal como se definen en las especificaciones de HLS.

   Estos archivos están disponibles automáticamente como pistas de subtítulos opcionales en el reproductor Primetime.

Puede hacer lo siguiente:

* Seleccione una pista de subtítulos disponible para que sea la pista actual y escuche eventos que indiquen pistas adicionales disponibles.
* Activar (visible) o desactivar (no visible) los subtítulos opcionales mediante la interfaz `MediaPlayer`.
* Seleccione las opciones de estilo que dictan cómo el motor de vídeo subyacente procesa los subtítulos opcionales.

   Utilice la interfaz `MediaPlayerItem` para seleccionar formatos como la fuente o el color de fuente.

