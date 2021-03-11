---
description: El servidor de manifiestos admite subtítulos WebVTT habilitados por el editor para todos los formatos de vídeo HLS. Cuando recibe solicitudes para insertar anuncios en contenido subtitulado de WebVTT, lo hace correctamente.
title: Compatibilidad con subtítulos WebVTT
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Compatibilidad con subtítulos WebVTT {#support-for-webvtt-captions}

El servidor de manifiestos admite subtítulos WebVTT habilitados por el editor para formatos de vídeo HLS/DASH. Cuando recibe solicitudes para insertar anuncios en contenido subtitulado de WebVTT, lo hace correctamente.

Si el editor incluye subtítulos WebVTT en el contenido, el servidor de manifiestos envía al cliente un flujo de contenido con subtítulos. El editor debe habilitar WebVTT para que el servidor de manifiestos admita subtítulos. Cuando el cliente tiene habilitados los subtítulos WebVTT y envía una solicitud al servidor de manifiestos, el servidor de manifiestos manipula la línea de tiempo y el seguimiento WebVTT y devuelve al cliente contenido con anuncios y subtítulos enlazados.

El flujo de trabajo para flujos de contenido de VOD es el siguiente:

1. El cliente envía un flujo de contenido con subtítulos WebVTT habilitados al servidor de manifiesto.
1. El servidor de manifiestos manipula la línea de tiempo para unir anuncios en el flujo de contenido.
1. El servidor de manifiestos manipula el seguimiento de WebVTT para agregar subtítulos al contenido (incluidos los anuncios).
1. El servidor de manifiestos envía el flujo de contenido al cliente, con anuncios insertados y rótulos.

>[!NOTE]
>
>Si un segmento de subtítulo WebVTT se encuentra dentro de un anuncio mid-roll, el visor ve que el subtítulo se reproduce antes y después de esa pausa publicitaria mid-roll. Por ejemplo, en un segmento de subtítulo de 10 segundos con un anuncio mid-roll de 30 segundos con una marca de 5 segundos, el visor ve ese segmento de subtítulo durante 5 segundos antes de la pausa publicitaria mid-roll y durante 5 segundos después de la emisión media.

>[!NOTE]
>
>Si un cliente solicita que un vídeo se reproduzca en un idioma específico, como inglés, y luego solicita reproducir el vídeo en francés, el servidor de manifiestos no puede detectar que el cliente solicitó cambiar el idioma al francés. Dado que el cliente no se comunica con el servidor de manifiesto, este inserta el pie de ilustración del anuncio en el flujo de vídeo utilizando el primer idioma especificado en el archivo maestro M3U8 del anuncio.
