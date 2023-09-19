---
title: Introducción a Adobe Primetime Ad Insertion
description: Introducción a Adobe Primetime Ad Insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Introducción a Adobe Primetime Ad Insertion {#ptai-get-started}

Primetime Ad Insertion coordina los sistemas que proporcionan contenido y anuncios para crear experiencias de publicidad personalizadas y en flujo y, a continuación, rastrear la reproducción de anuncios para sus anunciantes.

Primetime Ad Insertion interactúa con las aplicaciones cliente de entrega de vídeo reescribiendo manifiestos de vídeo para proporcionar anuncios segmentados y experiencias personalizadas para cada visualizador. Estos manifiestos combinan el contenido y los anuncios enviados desde un servidor de publicidad y, opcionalmente, pueden incluir metadatos que contengan instrucciones detalladas de seguimiento de anuncios. El Ad Insertion de Primetime admite el seguimiento de anuncios del lado del cliente y del lado del servidor.

Una vez configurado correctamente el sistema, un flujo de trabajo típico podría tener el siguiente aspecto:

1. La aplicación cliente genera un [URL del Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) con información sobre el flujo de vídeo y envía una solicitud de GET al Ad Insertion de Primetime.  El Ad Insertion de Primetime es compatible con HLS y DASH con una variedad de formatos de señalización de publicidad.

1. El Ad Insertion de Primetime responde enviando el manifiesto de contenido de la CDN del editor de nuevo a la aplicación cliente.

1. La aplicación cliente elige las secuencias adecuadas del manifiesto generado para reproducirlas y realiza solicitudes al Ad Insertion de Primetime.

1. El Ad Insertion de Primetime recupera los flujos solicitados de la CDN de contenido, analiza/lee cualquier información de referencia, realiza llamadas al servidor de publicidad y reemplaza las pausas publicitarias según sea necesario.

1. El Ad Insertion de Primetime normaliza el manifiesto reescribiendo las direcciones URL de recursos y detectando si los creativos de publicidad requieren transcodificación. Consulte [Transcodificación de publicidad Just-In-Time](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. Primetime Ad Insertion recupera los elementos publicitarios creativos necesarios e inserta los fragmentos adecuados en los manifiestos.

1. El Ad Insertion de Primetime envía los manifiestos identificados finales, incluidos los anuncios, a la aplicación cliente para su reproducción.

1. La entrega y la visibilidad de los anuncios se pueden medir mediante el seguimiento de anuncios del lado del cliente o del lado del servidor. Consulte [Configuración del seguimiento de anuncios](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

El Ad Insertion de Primetime es compatible con la mayoría de las configuraciones de cliente y reproductor HLS/DASH. Para obtener más información sobre los formatos específicos de señalización de publicidad admitidos, consulte [Formatos de referencia admitidos](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
