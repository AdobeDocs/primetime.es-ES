---
description: El servidor de manifiesto admite subtítulos WebVTT habilitados para editor para todos los formatos de vídeo HLS. Cuando recibe solicitudes para insertar anuncios en contenido con subtítulos WebVTT, lo hace correctamente.
title: Compatibilidad con subtítulos WebVTT
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Compatibilidad con subtítulos WebVTT {#support-for-webvtt-captions}

El servidor de manifiesto admite subtítulos WebVTT habilitados para editor para formatos de vídeo HLS/DASH. Cuando recibe solicitudes para insertar anuncios en contenido con subtítulos WebVTT, lo hace correctamente.

Si el editor incluye subtítulos WebVTT en el contenido, el servidor de manifiesto envía al cliente un flujo de contenido con subtítulos. El editor debe habilitar WebVTT para que el servidor de manifiesto admita subtítulos. Cuando el cliente tiene subtítulos WebVTT habilitados y envía una solicitud al servidor de manifiesto, este manipula la cronología y el seguimiento WebVTT y devuelve al cliente contenido con anuncios y subtítulos vinculados.

El flujo de trabajo para las secuencias de contenido de VOD es el siguiente:

1. El cliente envía una secuencia de contenido con subtítulos WebVTT habilitados al servidor de manifiesto.
1. El servidor de manifiesto manipula la cronología para unir los anuncios al flujo de contenido.
1. El servidor de manifiestos manipula la pista WebVTT para añadir subtítulos al contenido (incluidos los anuncios).
1. El servidor de manifiestos envía el flujo de contenido al cliente, con anuncios y subtítulos insertados.

>[!NOTE]
>
>Si un segmento de subtítulos WebVTT se encuentra dentro de un anuncio durante la emisión, el visor ve que el subtítulo se reproduce antes y después de esa pausa publicitaria durante la emisión. Por ejemplo, en un segmento de rótulo de 10 segundos con un anuncio durante la emisión de 30 segundos en la marca de 5 segundos, el usuario verá ese segmento de rótulo durante 5 segundos antes de la pausa publicitaria durante la emisión y durante 5 segundos después de la emisión.

>[!NOTE]
>
>Si un cliente solicita que un vídeo se reproduzca en un idioma específico, como inglés, y luego solicita reproducir el vídeo en francés, el servidor de manifiesto no puede detectar que el cliente solicitó cambiar el idioma al francés. Dado que el cliente no se comunica con el servidor de manifiesto, este inserta el pie de ilustración del anuncio en el flujo de vídeo utilizando el primer idioma especificado en el archivo maestro M3U8 del anuncio.
