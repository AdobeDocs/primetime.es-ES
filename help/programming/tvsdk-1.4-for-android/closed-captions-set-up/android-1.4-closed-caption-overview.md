---
description: Los subtítulos muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.
title: Seleccionar una pista de rótulo actual entre las pistas disponibles
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Información general {#work-with-closed-captions}

Los subtítulos muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visor es difícil de oír.

Los subtítulos suelen estar en el mismo idioma que el audio y también muestran sonidos de fondo como texto, pero los subtítulos suelen estar en un idioma distinto y no incluyen sonidos de fondo.

TVSDK admite la renderización de estos formatos:

* 608 y 708 subtítulos cerrados, cuando se entregan como parte del flujo de transporte de vídeo a través de HLS como paquetes de datos en secuencias de vídeo MPEG-2.
* Los archivos de subtítulos WebVTT, a los que se hace referencia desde los archivos de manifiesto M3U8 tal como se definen en las especificaciones HLS. Están disponibles automáticamente como pistas de subtítulos en el reproductor Primetime.

Puede:

* Seleccione una pista de subtítulos disponible para que sea la pista actual y escuche los eventos que indiquen pistas disponibles adicionales.
* Active o desactive los subtítulos (visibles o no visibles) mediante la interfaz `MediaPlayer`.
* Seleccione las opciones de estilo que dictan cómo el motor de vídeo subyacente representa los subtítulos. Utilice la interfaz `MediaPlayerItem` para seleccionar formatos como la fuente o el color de fuente.
