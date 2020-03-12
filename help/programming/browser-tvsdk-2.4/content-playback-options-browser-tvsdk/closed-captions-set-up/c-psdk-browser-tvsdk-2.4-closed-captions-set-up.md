---
description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-title: Trabajo con subtítulos opcionales
title: Trabajo con subtítulos opcionales
uuid: bc069e04-3ea3-4cdf-a8a6-d8aef91ece91
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Trabajo con subtítulos opcionales{#work-with-closed-captions}

Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.

Los subtítulos cerrados suelen estar en el mismo idioma que el audio y también muestran sonidos de fondo como texto, pero los subtítulos suelen estar en un idioma diferente y no incluyen sonidos de fondo.

El SDK de TVSDK del explorador admite la representación de estos formatos:

* Subtítulos opcionales 608 y 708, cuando se envían como parte del flujo de transporte de vídeo a través de HLS como paquetes de datos en flujos de vídeo MPEG-2.
* Archivos de subtítulos WebVTT a los que se hace referencia desde los archivos de manifiesto M3U8 tal como se definen en las especificaciones de HLS. Están disponibles automáticamente como pistas de subtítulos opcionales en el reproductor Primetime.

Puede:

* Seleccione una pista de subtítulos disponible para que sea la pista actual y escuche los eventos que indican pistas adicionales disponibles.
* Activa o desactiva los subtítulos cerrados (visibles o no visibles) mediante la `MediaPlayer` interfaz.
* Seleccione las opciones de estilo que dictan cómo el motor de vídeo subyacente procesa los subtítulos opcionales. Utilice la `MediaPlayerItem` interfaz para seleccionar formatos como la fuente o el color de fuente.

