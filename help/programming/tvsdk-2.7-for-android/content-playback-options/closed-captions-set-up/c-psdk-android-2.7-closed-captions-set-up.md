---
description: Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visualizador tiene dificultades auditivas.
title: Trabajar con subtítulos opcionales
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Información general {#work-with-closed-captions-overview}

Los subtítulos opcionales muestran la parte de audio de un vídeo como texto en la pantalla cuando el sonido es inaudible o el visualizador tiene dificultades auditivas.

Los subtítulos cerrados suelen estar en el mismo idioma que el audio y también muestran sonidos de fondo como texto, pero los subtítulos suelen estar en un idioma diferente y no incluyen sonidos de fondo.

TVSDK admite la renderización de estos formatos:

* Subtítulos 608 y 708, cuando se entregan como parte del flujo de transporte de vídeo a través de HLS como paquetes de datos en flujos de vídeo MPEG-2.
* Archivos de subtítulos WebVTT, a los que se hace referencia desde los archivos de manifiesto M3U8 tal como se definen en las especificaciones de HLS.

  Estos archivos están disponibles automáticamente como pistas de subtítulos ocultos en el reproductor de Primetime.

Puede hacer lo siguiente:

* Seleccione una pista de subtítulos disponible para que sea la pista actual y escuche eventos que indiquen pistas disponibles adicionales.
* Activar (visible) o desactivar (no visible) los subtítulos utilizando `MediaPlayer` interfaz.
* Seleccione las opciones de estilo que dictan cómo el motor de vídeo subyacente procesa los subtítulos.

  Utilice el `MediaPlayerItem` para seleccionar formatos, como la fuente o el color de fuente.
