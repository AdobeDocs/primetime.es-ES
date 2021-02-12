---
title: Introducción a Adobe Primetime Ad Insertion
description: Introducción a Adobe Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Introducción a Adobe Primetime Ad Insertion {#ptai-get-started}

Primetime Ad Insertion coordina los sistemas que proporcionan contenido y publicidades para crear experiencias publicitarias personalizadas en el flujo y, a continuación, realizar un seguimiento de la reproducción de anuncios para los anunciantes.

Primetime Ad Insertion interactúa con las aplicaciones cliente de envío de vídeo reescribiendo los manifiestos de vídeo para proporcionar anuncios con objetivos y experiencias personalizadas para cada visor. Estos manifiestos combinan el contenido y las publicidades enviadas desde un servidor de publicidad y, opcionalmente, pueden incluir metadatos que contengan instrucciones detalladas de seguimiento de anuncios. Primetime Ad Insertion admite el seguimiento de anuncios en el lado del cliente y en el servidor.

Una vez configurado correctamente el sistema, un flujo de trabajo típico podría tener el siguiente aspecto:

1. La aplicación cliente genera una [URL de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) con información sobre el flujo de vídeo y envía una solicitud de GET a Primetime Ad Insertion.  Primetime Ad Insertion admite HLS y DASH con una variedad de formatos de señalización de anuncios.

1. Primetime Ad Insertion responde enviando el manifiesto de contenido desde la CDN del editor a la aplicación cliente.

1. La aplicación cliente elige los flujos adecuados en el manifiesto generado que se van a reproducir y realiza solicitudes al Ad Insertion Primetime.

1. Primetime Ad Insertion obtiene los flujos solicitados de la CDN de contenido, analiza o lee cualquier información de referencia, realiza llamadas al servidor de publicidad y reemplaza los saltos de anuncios según sea necesario.

1. Primetime Ad Insertion normaliza el manifiesto reescribiendo las direcciones URL de los recursos y detectando si los elementos creativos de publicidad requieren transcodificación, consulte [Transcodificación de publicidad puntual](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. Primetime Ad Insertion obtiene los elementos creativos de publicidad necesarios e inserta los fragmentos correspondientes en los manifiestos.

1. Primetime Ad Insertion entrega los manifiestos finales, incluidos los anuncios, a la aplicación cliente para su reproducción.

1. El envío de la publicidad y la visibilidad se pueden medir mediante el seguimiento de la publicidad del cliente o del servidor; consulte [Configuración del seguimiento de publicidad](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

Primetime Ad Insertion admite la mayoría de las configuraciones de cliente y reproductor HLS/DASH. Para obtener más información sobre los formatos específicos de señalización de publicidad admitidos, consulte [Formatos de señal admitidos](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
