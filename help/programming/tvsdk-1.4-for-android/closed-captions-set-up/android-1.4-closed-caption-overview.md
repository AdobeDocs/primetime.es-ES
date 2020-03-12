---
description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
seo-title: Seleccionar una pista de rótulo actual entre las pistas disponibles
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Información general {#work-with-closed-captions}

Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.

Los subtítulos cerrados suelen estar en el mismo idioma que el audio y también muestran sonidos de fondo como texto, pero los subtítulos suelen estar en un idioma diferente y no incluyen sonidos de fondo.

TVSDK admite la representación de estos formatos:

* Subtítulos opcionales 608 y 708, cuando se envían como parte del flujo de transporte de vídeo a través de HLS como paquetes de datos en flujos de vídeo MPEG-2.
* Archivos de subtítulos WebVTT a los que se hace referencia desde los archivos de manifiesto M3U8 tal como se definen en las especificaciones de HLS. Están disponibles automáticamente como pistas de subtítulos opcionales en el reproductor Primetime.

Puede:

* Seleccione una pista de subtítulos disponible para que sea la pista actual y escuche los eventos que indican pistas adicionales disponibles.
* Activa o desactiva los subtítulos cerrados (visibles o no visibles) mediante la `MediaPlayer` interfaz.
* Seleccione las opciones de estilo que dictan cómo el motor de vídeo subyacente procesa los subtítulos opcionales. Utilice la `MediaPlayerItem` interfaz para seleccionar formatos como la fuente o el color de fuente.
