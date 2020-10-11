---
title: Introducción a Adobe Primetime Ad Insertion
description: Introducción a Adobe Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Introducción a Adobe Primetime Ad Insertion {#ptai-get-started}

Primetime Ad Insertion coordina los sistemas que proporcionan contenido y publicidades para crear experiencias publicitarias personalizadas en el flujo y, a continuación, realizar un seguimiento de la reproducción de anuncios para los anunciantes.

El Ad Insertion Primetime interactúa con las aplicaciones cliente de envío de vídeo reescribiendo los manifiestos de vídeo para proporcionar anuncios con objetivos y experiencias personalizadas para cada visor. Estos manifiestos combinan el contenido y los anuncios enviados desde un servidor de publicidad y, de forma opcional, pueden incluir metadatos que contengan instrucciones detalladas sobre el seguimiento de anuncios. Primetime Ad Insertion admite el seguimiento de anuncios en el lado del cliente y en el servidor.

Una vez configurado correctamente el sistema, un flujo de trabajo típico podría tener el siguiente aspecto:

1. La aplicación cliente genera una URL [de](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md) Bootstrap con información sobre el flujo de vídeo y envía una solicitud de GET a Primetime Ad Insertion.

1. Primetime Ad Insertion responde enviando el manifiesto de contenido desde la CDN del editor a la aplicación cliente.

1. La aplicación cliente elige los flujos adecuados en el manifiesto generado que se van a reproducir y realiza solicitudes al Ad Insertion Primetime.

1. Primetime Ad Insertion obtiene los flujos solicitados de la CDN de contenido, analiza o lee cualquier información de referencia, realiza llamadas al servidor de publicidad y reemplaza los saltos de anuncios según sea necesario.

1. El Ad Insertion Primetime normaliza el manifiesto reescribiendo las direcciones URL de los recursos y detectando si los elementos creativos de publicidad requieren transcodificación, consulte [Just-in-time y transcoding](just-in-time-transcoding.md) and [packings](just-in-time-repackaging.md).

1. Primetime Ad Insertion obtiene los elementos creativos de publicidad necesarios e inserta los fragmentos correspondientes en los manifiestos.

1. Primetime Ad Insertion entrega los manifiestos finales, incluidos los anuncios, a la aplicación cliente para su reproducción.

1. El envío y la visibilidad de la publicidad se pueden medir mediante el seguimiento de la publicidad del lado del cliente o del servidor; consulte [Configuración del seguimiento](set-up-ad-tracking.md)de la publicidad.

Primetime Ad Insertion admite la mayoría de las configuraciones de cliente para HLS/DASH.
