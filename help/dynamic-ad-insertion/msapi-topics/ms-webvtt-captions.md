---
description: El servidor de manifiesto admite subtítulos WebVTT activados por el editor para todos los formatos de vídeo HLS. Cuando recibe solicitudes para insertar publicidades en contenido con subtítulos WebVTT, lo hace correctamente.
seo-description: El servidor de manifiesto admite subtítulos WebVTT activados por el editor para todos los formatos de vídeo HLS. Cuando recibe solicitudes para insertar publicidades en contenido con subtítulos WebVTT, lo hace correctamente.
seo-title: Compatibilidad con subtítulos WebVTT
title: Compatibilidad con subtítulos WebVTT
uuid: 1dc728b0-5aeb-4c48-8f3b-54ff4b135742
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Compatibilidad con subtítulos WebVTT {#support-for-webvtt-captions}

El servidor de manifiesto admite subtítulos WebVTT activados por el editor para todos los formatos de vídeo HLS. Cuando recibe solicitudes para insertar publicidades en contenido con subtítulos WebVTT, lo hace correctamente.

Si el editor incluye subtítulos WebVTT en el contenido, el servidor de manifiesto envía al cliente un flujo de contenido con subtítulos. El editor debe habilitar WebVTT para que el servidor de manifiesto admita subtítulos. Cuando el cliente tiene los subtítulos WebVTT activados y envía una solicitud al servidor de manifiesto, el servidor de manifiesto manipula la línea de tiempo y el seguimiento WebVTT y devuelve al cliente el contenido con los rótulos y publicidades enlazadas.

El flujo de trabajo para flujos de contenido de VOD es el siguiente:

1. El cliente envía un flujo de contenido con subtítulos WebVTT habilitados al servidor de manifiesto.
1. El servidor de manifiesto manipula la línea de tiempo para unir publicidades en el flujo de contenido.
1. El servidor de manifiesto manipula el seguimiento de WebVTT para agregar rótulos al contenido (incluidos los anuncios).
1. El servidor de manifiesto envía el flujo de contenido al cliente, con anuncios y rótulos insertados.

>[!NOTE]
>
>Si un segmento de subtítulos WebVTT se encuentra dentro de un anuncio intermedio, el visor ve que el subtítulo se reproduce antes y después de ese salto de anuncios de mitad de carrera. Por ejemplo, en un segmento de subtítulos de 10 segundos con un anuncio intermedio de 30 segundos con una marca de 5 segundos, el visor ve ese segmento de subtítulos durante 5 segundos antes de la pausa publicitaria media y durante 5 segundos después de la mitad del rollo.

>[!NOTE]
>
>Si un cliente solicita que un vídeo se reproduzca en un idioma específico, como el inglés, y luego solicita reproducir el vídeo en francés, el servidor de manifiesto no puede detectar que el cliente solicitado para cambiar el idioma al francés. Dado que el cliente no se comunica con el servidor de manifiesto, este inserta el rótulo de anuncio en el flujo de vídeo utilizando el primer idioma especificado en el archivo maestro M3U8 del anuncio.