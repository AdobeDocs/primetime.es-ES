---
description: El servidor de manifiesto coordina los sistemas que proporcionan contenido, proporcionan anuncios, reproducen vídeo y rastrean anuncios. Recibe listas de reproducción (manifiestos) codificadas para M3U8 que los reproductores de vídeo clientes reciben de proveedores de contenido, vincula anuncios de proveedores de publicidad a los manifiestos y pasa los manifiestos enlazados a reproductores de vídeo. Admite el seguimiento de anuncios del lado del cliente y del lado del servidor. Lleva a cabo sus interacciones utilizando una interfaz de servicio web basada en HTTP.
title: Descripción general de las interacciones del servidor de manifiesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Descripción general de las interacciones del servidor de manifiesto {#overview-of-manifest-server-interactions}

El servidor de manifiesto coordina los sistemas que proporcionan contenido, proporcionan anuncios, reproducen vídeo y rastrean anuncios. Recibe listas de reproducción (manifiestos) codificadas para M3U8 que los reproductores de vídeo clientes reciben de proveedores de contenido, vincula anuncios de proveedores de publicidad a los manifiestos y pasa los manifiestos enlazados a reproductores de vídeo. Admite el seguimiento de anuncios del lado del cliente y del lado del servidor. Lleva a cabo sus interacciones utilizando una interfaz de servicio web basada en HTTP.

Una configuración típica contiene:

* El servidor de manifiestos de Primetime
* El servicio de reempaquetado creativo de Primetime (CRS)
* Un cliente, control de un reproductor de vídeo
* Un editor, normalmente con un sistema de administración de contenido (CMS)
* Una red de distribución de contenido (CDN)
* Un servidor de publicidad
* Un receptor para informes de seguimiento de anuncios

El flujo de trabajo varía en función de varios factores, como si la CDN es Akamai o si el cliente está realizando el seguimiento de anuncios. Para obtener un diagrama del flujo de trabajo para el seguimiento de anuncios del lado del cliente, consulte [Flujo de trabajo de seguimiento del lado del cliente](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

El servidor de manifiestos interactúa con los clientes de envío de vídeo recibiendo y respondiendo a las solicitudes de GET HTTP. Las respuestas son manifiestos con codificación M3U8 que describen contenido identificado, incluyendo opcionalmente una estructura JSON o VMAP (sidecar) que contiene instrucciones detalladas de seguimiento de anuncios (consulte [Formatos de archivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Un flujo de trabajo típico tiene el siguiente aspecto:

1. El editor envía la URL de contenido y la información del servidor de publicidad al cliente.
1. El cliente utiliza la información del editor para generar una URL de servidor de manifiesto y envía una solicitud de GET a esa URL. Esto se conoce como la dirección URL del Bootstrap.
1. El servidor de manifiesto establece una sesión con el cliente.
1. El servidor de manifiesto obtiene manifiestos de contenido de la CDN, que pueden incluir información de pausa publicitaria.
1. El servidor de manifiesto redirige al cliente al manifiesto maestro/variante que generó para el cliente.

   >[!NOTE]
   >
   >Si los parámetros de consulta de URL del Bootstrap contienen la configuración `pttrackingmode=simple` o `ptplayer=ios-mobileweb` , el servidor de manifiestos devuelve la URL del manifiesto maestro/variante en un objeto JSON y el cliente envía una solicitud de GET a esa URL del manifiesto de variante.

1. El cliente elige un flujo en el manifiesto de variante generado para reproducir, lo que envía información de anuncio al servidor de manifiesto.
1. El servidor de manifiesto pasa la información proporcionada por el cliente al servidor de publicidad y recibe los anuncios y las direcciones URL de seguimiento de anuncios del servidor de publicidad. Si un anuncio suministrado no está en formato HLS, el servidor de manifiestos lo envía a CRS para su conversión a HLS.
1. El servidor de manifiesto vincula anuncios al manifiesto de contenido y envía el nuevo manifiesto identificado al cliente.
1. El cliente reproduce el contenido con los anuncios enlazados y realiza solicitudes en los momentos especificados a las direcciones URL de seguimiento especificadas.

La inserción de anuncios de Primetime admite clientes en muchas plataformas de envío de vídeo. No todos los clientes están basados en el paquete TVSDK de Primetime, pero todos los clientes envían solicitudes de GET a la misma URL básica. Los parámetros de consulta distinguen una solicitud de cliente de otra indicando al servidor de manifiesto:

* qué cliente está realizando la solicitud,
* lo que el cliente desea,
* y qué información de seguimiento de anuncios proporcionar.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

El servidor de manifiestos utiliza el estándar de uso compartido de recursos de origen cruzado (CORS). Busca un encabezado `Origin` en las solicitudes que recibe. Si el encabezado está presente, responde con

* `Access-Control-Allow-Origin: *`cadena del encabezado Origen`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

Si no es así, responde con:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`