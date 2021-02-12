---
description: El servidor de manifiesto coordina los sistemas que proporcionan contenido, proporcionan anuncios, reproducen vídeo y rastrean anuncios. Recibe listas de reproducción (manifiestos) con codificación M3U8 que los reproductores de vídeo del cliente reciben de los proveedores de contenido, vincula anuncios de los proveedores de publicidad a los manifiestos y pasa los manifiestos vinculados a los reproductores de vídeo. Admite el seguimiento de anuncios tanto del lado del cliente como del lado del servidor. Lleva a cabo sus interacciones utilizando una interfaz de servicio web basada en HTTP.
seo-description: El servidor de manifiesto coordina los sistemas que proporcionan contenido, proporcionan anuncios, reproducen vídeo y rastrean anuncios. Recibe listas de reproducción (manifiestos) con codificación M3U8 que los reproductores de vídeo del cliente reciben de los proveedores de contenido, vincula anuncios de los proveedores de publicidad a los manifiestos y pasa los manifiestos vinculados a los reproductores de vídeo. Admite el seguimiento de anuncios tanto del lado del cliente como del lado del servidor. Lleva a cabo sus interacciones utilizando una interfaz de servicio web basada en HTTP.
seo-title: Información general sobre las interacciones del servidor de manifiesto
title: Información general sobre las interacciones del servidor de manifiesto
uuid: 3e314a45-a4dd-492f-8915-19224a8fbbc7
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Información general sobre las interacciones del servidor de manifiesto {#overview-of-manifest-server-interactions}

El servidor de manifiesto coordina los sistemas que proporcionan contenido, proporcionan anuncios, reproducen vídeo y rastrean anuncios. Recibe listas de reproducción (manifiestos) con codificación M3U8 que los reproductores de vídeo del cliente reciben de los proveedores de contenido, vincula anuncios de los proveedores de publicidad a los manifiestos y pasa los manifiestos vinculados a los reproductores de vídeo. Admite el seguimiento de anuncios tanto del lado del cliente como del lado del servidor. Lleva a cabo sus interacciones utilizando una interfaz de servicio web basada en HTTP.

Una configuración típica contiene:

* El servidor de manifiesto Primetime
* El servicio de reempaquetado creativo Primetime (CRS)
* Un cliente, control de un reproductor de vídeo
* Un editor, normalmente con un sistema Gestor de contenido (CMS)
* Una red de Envío de contenido (CDN)
* Un servidor de publicidad
* Un receptor para los informes de seguimiento de publicidad

El flujo de trabajo varía en función de una serie de factores, como si la CDN es Akamai o si el cliente está realizando el seguimiento de anuncios. Para ver un diagrama del flujo de trabajo para el seguimiento de anuncios en el lado del cliente, consulte [Flujo de trabajo de seguimiento del lado del cliente](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

El servidor de manifiesto interactúa con los clientes de envío de vídeo recibiendo y respondiendo a las solicitudes de GET HTTP. Las respuestas son manifiestos con codificación M3U8 que describen el contenido con vinculación de publicidad, incluyendo opcionalmente una estructura JSON o VMAP (sidecar) que contiene instrucciones detalladas de seguimiento de anuncios (consulte [Formatos de archivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Un flujo de trabajo típico es el siguiente:

1. El editor envía la dirección URL de contenido y la información del servidor de publicidad al cliente.
1. El cliente utiliza la información del editor para generar una URL de servidor de manifiesto y envía una solicitud de GET a esa URL. Esto se conoce como URL de Bootstrap.
1. El servidor de manifiesto establece una sesión con el cliente.
1. El servidor de manifiesto obtiene los manifiestos de contenido de la CDN, que pueden incluir información de pausa publicitaria.
1. El servidor de manifiesto redirige al cliente al manifiesto maestro/variante que generó para el cliente.

   >[!NOTE]
   >
   >Si los parámetros de consulta de URL de Bootstrap contienen la configuración `pttrackingmode=simple` o `ptplayer=ios-mobileweb`, el servidor de manifiesto devuelve la URL de manifiesto maestro/variante en un objeto JSON y el cliente envía una solicitud de GET a esa URL de manifiesto de variante.

1. El cliente elige un flujo en el manifiesto de variante generado que se va a reproducir, y envía información de anuncio al servidor de manifiesto.
1. El servidor de manifiesto pasa la información proporcionada por el cliente al servidor de publicidad y recibe anuncios y direcciones URL de seguimiento de publicidad del servidor de publicidad. Si una publicidad suministrada no está en formato HLS, el servidor de manifiesto la envía a CRS para su conversión a HLS.
1. El servidor de manifiesto vincula publicidades al manifiesto de contenido y envía el nuevo manifiesto vinculado al cliente.
1. El cliente reproduce el contenido con las publicidades vinculadas y realiza solicitudes en los momentos especificados a las direcciones URL de seguimiento especificadas.

La inserción de anuncios Primetime admite clientes en muchas plataformas de envío de vídeo. No todos los clientes se crean en el paquete TVSDK de Primetime, pero todos los clientes envían solicitudes de GET a la misma dirección URL básica. Los parámetros de consulta distinguen una solicitud de cliente de otra comunicándole al servidor de manifiesto:

* qué cliente realiza la solicitud,
* lo que ese cliente quiere,
* y qué información de seguimiento de anuncios proporcionar.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

El servidor de manifiesto utiliza el estándar de uso compartido de recursos entre Orígenes (CORS). Busca un encabezado `Origin` en las solicitudes que recibe. Si el encabezado está presente, responde con

* `Access-Control-Allow-Origin: *`cadena del encabezado del Origen`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

En caso contrario, responde con:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`