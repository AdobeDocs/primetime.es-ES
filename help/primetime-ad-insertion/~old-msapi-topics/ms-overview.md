---
description: El servidor de manifiestos coordina los sistemas que proporcionan contenido, anuncios, reproducción de vídeo y seguimiento de anuncios. Recibe listas de reproducción (manifiestos) codificadas en M3U8 que los reproductores de vídeo cliente reciben de los proveedores de contenido, vincula los anuncios de los proveedores de publicidad a los manifiestos y pasa los manifiestos vinculados a los reproductores de vídeo. Admite el seguimiento de anuncios del lado del cliente y del lado del servidor. Realiza sus interacciones mediante una interfaz de servicio web basada en HTTP.
title: Información general sobre las interacciones de Manifest Server
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Información general sobre las interacciones de Manifest Server {#overview-of-manifest-server-interactions}

El servidor de manifiestos coordina los sistemas que proporcionan contenido, anuncios, reproducción de vídeo y seguimiento de anuncios. Recibe listas de reproducción (manifiestos) codificadas en M3U8 que los reproductores de vídeo cliente reciben de los proveedores de contenido, vincula los anuncios de los proveedores de publicidad a los manifiestos y pasa los manifiestos vinculados a los reproductores de vídeo. Admite el seguimiento de anuncios del lado del cliente y del lado del servidor. Realiza sus interacciones mediante una interfaz de servicio web basada en HTTP.

Una configuración típica contiene:

* Servidor de manifiesto de Primetime
* El servicio de reempaquetado creativo de Primetime (CRS)
* Un cliente, que controla un reproductor de vídeo
* Un editor, normalmente con un sistema de administración de contenido (CMS)
* Una red de distribución de contenido (CDN)
* Un servidor de publicidad
* Un receptor para informes de seguimiento de anuncios

El flujo de trabajo varía en función de una serie de factores, como si la CDN es Akamai o si el cliente realiza el seguimiento de anuncios. Para ver un diagrama del flujo de trabajo para el seguimiento de anuncios del lado del cliente, consulte [Flujo de trabajo de seguimiento del lado del cliente](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

El servidor de manifiesto interactúa con los clientes de entrega de vídeo recibiendo y respondiendo a solicitudes de GET HTTP. Las respuestas son manifiestos codificados en M3U8 que describen contenido vinculado a anuncios, que incluyen opcionalmente una estructura JSON o VMAP (sidecar) que contiene instrucciones detalladas de seguimiento de anuncios (consulte [Formatos de archivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Un flujo de trabajo típico tiene el siguiente aspecto:

1. El publicador envía la dirección URL de contenido y la información del servidor de publicidad al cliente.
1. El cliente utiliza la información del publicador para generar una URL de servidor de manifiesto y envía una solicitud de GET a esa URL. Esto se conoce como URL del Bootstrap.
1. El servidor de manifiestos establece una sesión con el cliente.
1. El servidor de manifiestos obtiene manifiestos de contenido de la CDN, que pueden incluir información de pausas publicitarias.
1. El servidor de manifiestos redirige al cliente al manifiesto maestro/variante que generó para el cliente.

   >[!NOTE]
   >
   >Si los parámetros de consulta de URL del Bootstrap contienen el `pttrackingmode=simple` o `ptplayer=ios-mobileweb` Cuando se configura, el servidor de manifiestos devuelve la dirección URL del manifiesto principal/variante en un objeto JSON y el cliente envía una solicitud de GET a esa dirección URL del manifiesto de variante.

1. El cliente elige una secuencia en el manifiesto de variante generado para reproducir y enviar información de anuncio al servidor de manifiesto.
1. El servidor de manifiesto pasa la información proporcionada por el cliente al servidor de publicidad y recibe las direcciones URL de anuncios y de seguimiento de anuncios desde el servidor de publicidad. Si un anuncio proporcionado no está en formato HLS, el servidor de manifiesto lo envía a CRS para su conversión a HLS.
1. El servidor de manifiestos vincula los anuncios con el manifiesto de contenido y envía el nuevo manifiesto vinculado al cliente.
1. El cliente reproduce el contenido con los anuncios enlazados y realiza solicitudes en los momentos especificados a las direcciones URL de seguimiento especificadas.

La inserción de anuncios de Primetime admite clientes en muchas plataformas de entrega de vídeo. No todos los clientes se crean en el paquete TVSDK de Primetime, pero todos envían solicitudes de GET a la misma URL básica. Los parámetros de consulta distinguen una solicitud de cliente de otra indicando al servidor de manifiesto:

* qué cliente realiza la solicitud,
* lo que ese cliente quiere,
* y qué información de seguimiento de anuncios proporcionar.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

El servidor de manifiesto utiliza el estándar de uso compartido de recursos de origen cruzado (CORS). Se busca un `Origin` encabezado en las solicitudes que recibe. Si el encabezado está presente, responde con

* `Access-Control-Allow-Origin: *`cadena del encabezado Origen`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

Si no es así, responde con:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`