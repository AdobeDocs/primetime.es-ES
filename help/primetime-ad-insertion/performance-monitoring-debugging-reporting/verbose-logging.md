---
title: Registro detallado
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---


# Registro detallado {#verbose-logging}

## descripciones de eventos ptdebug/logging {#ptdebug-logging-events}

Al iniciar el registro de depuración para una sesión de servidor de manifiesto, puede agregar el parámetro `ptdebug` a la dirección URL de la solicitud para especificar las siguientes opciones para la información que devuelve el servidor de manifiesto en los encabezados HTTP:

* `ptdebug=true`
Todos los registros excepto TRACE_HTTP_HEADER y la mayoría de los datos de llamada/respuesta de los registros TRACE_AD_CALL.

* `ptdebug=AdCall`
Sólo registros de tipo TRACE_AD_ (por ejemplo, TRACE_AD_CALL).

* `ptdebug=Header`
Sólo registros TRACE_HTTP_HEADER.

## Formatos de registros {#log-record-formats}

Cada registro de registro tiene un tipo y un conjunto de campos, algunos de los cuales pueden ser opcionales. Los campos de todos los registros hasta el tipo de registro son los mismos. Proporcionan una marca de hora e información sobre la sesión. El tipo de registro identifica el tipo de evento que se registra y los campos posteriores proporcionan información sobre el evento registrado.

La estructura de un registro de registro es la siguiente:

`datetime request_id session_id zone_id record_type other fields`.

| Campo | Tipo | Descripción |
|---|---|---|
| datetime | string | Marca de hora |
| request_id | string | Id. de solicitud utilizado por el servidor de manifiesto (marca de hora Unix) |
| session_id | string | Id. de sesión utilizado por el servidor de manifiesto |
| zone_id | integer | Zona |
| record_type | string | Tipo de evento que se registra |
| otros campos | varía | Depende del tipo de evento |

Los registros de este tipo registran los resultados de las solicitudes HTTP. Los campos más allá de `TRACE_REQUEST_INFO` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| request_method | string | Método HTTP (GET o POST) |
| request_uri | string | URI de solicitud HTTP (sin host) |
| request_length | integer | Duración de la solicitud (bytes) |
| response_length | integer | Duración de la respuesta (bytes) |
| delta | integer | Tiempo (milisegundos) para procesar la solicitud |
| module_type | string | Variant, Stream o VOD |
| remote_address_aud_client_ip | string | **answer** |
| remote_address_x_fwd_for_hdr_key | string | **answer** |
| remote_host_port | string | **answer** |

**Los tres últimos campos** son opcionales.

**Un ejemplo**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Registros TRACE_HTTP_HEADER {#trace-http-header-records}

Registros de este tipo registran encabezados HTTP intercambiados durante llamadas HTTP entre el servidor de manifiesto y el cliente, el servidor de publicidad o el servidor de contenido. Los campos más allá de TRACE_HTTP_HEADER aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| request_type | string | Tipo de solicitud (PRINCIPAL o DESCONOCIDO) |
| request_response | string | Encabezado de respuesta (solicitud o respuesta) |
| header_name | string | Nombre de encabezado HTTP |
| header_value | string | Valor de encabezado HTTP con codificación base64 |

>[!NOTE]
>
>Los campos `request_type` y `header_value` son opcionales.

**Un ejemplo**

```shell
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_MISC Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST Cookie aGRu. . .
2015-03-25T06:10:00.928Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST User-Agent TW96aW. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Server bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Content-Type YXBwb. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Last-Modified V2VkL. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE ETag IjIyY2. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Vary QWNjZXB. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Cache-Control bWF4LW. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Expires V2VkL. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Date V2VkLCA. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Age MQ==
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Via MS4xIH. . .
```

### Registros TRACE_AD_CALL {#tracing-ad-call-records}

Los registros de este tipo registran los resultados de las solicitudes de publicidad de servidor de manifiesto. Los campos más allá de `TRACE_AD_CALL` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| request_duration | integer | Tiempo (milisegundos) entre la solicitud y la respuesta |
| ad_server_consulta_url | string | Dirección URL de la llamada de publicidad, incluidos los parámetros de consulta |
| ad_system_id | string | Sistema de publicidad, desde la respuesta del servidor de publicidad (Auditude si no se especifica) |
| avail_id | string | ID del valor, de la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| avail_duration | number | Duración (segundos) del valor promedio, a partir de la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| ad_server_response | string | Respuesta codificada en base64 del servidor de publicidad |

Un ejemplo:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE y TRACE_AD_REDIRECT registros {#trace-ad-insert-resolve-redirect}

Los registros de este tipo registran los resultados de las solicitudes de publicidad indicadas por el tipo de registro. Los campos más allá del tipo de registro aparecen en el orden que se muestra en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Se devolvió el código de estado HTTP. |
| avail_id | string | ID del valor, desde la señal de anuncio en el archivo de manifiesto de contenido (activo) o desde el servidor de manifiesto (VOD). |
| ad_type | string | Tipo de publicidad (DIRECTA o REDIRECTA). |
| ad_duration | integer | Duración (segundos) del anuncio, desde la respuesta del servidor de publicidad. |
| ad_content_url | string | Dirección URL del archivo de manifiesto de la publicidad, desde la respuesta del servidor de publicidad. |
| **†** ad_content_url_actual | string | Dirección URL del archivo de manifiesto de la publicidad insertada. Vacío para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de publicidad, desde la respuesta del servidor de publicidad (Auditude si no se especifica). |
| ad_id | string | ID de la publicidad, de la respuesta del servidor de publicidad. |
| creative_id | string | ID del elemento creativo, desde el nodo de publicidad, desde la respuesta del servidor de publicidad. |
| **†** ad_call_id | string | No se usa. Reservado para uso futuro. |
| delta | integer | Tiempo (milisegundos) que tarda este evento. |
| **†** misc | string | Motivo por el que se omitió el anuncio. |

**†** `ad_content_url_actual`,  `ad_call_id`y  `misc` los campos son opcionales.

>[!NOTE]
>
>Para `TRACE_AD_RESOLVE` y `TRACE_AD_INSERT`, la dirección URL en el campo `ad_content_url_actual` es para la publicidad transcodificada si hay una disponible. De lo contrario, el campo está vacío para `TRACE_AD_RESOLVE` o lo mismo que `ad_content_url` para `TRACE_AD_INSERT`.

Un ejemplo:

```shell
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

<!-- ### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond `TRACE_TRACKING_URL` appear in the order shown in the table, separated by tabs.

| Field | Type | Description |
|---|---|---|
| pts | number | Program timestamp. Time within video to call the URL. |
| ad_system | string | Ad system (auditude or freewheel) |
| url | string | URL pinged |
| status | string | HTTP status returned from the ping |

```shell
2015-06-04T23:24:42.000-0700 1426742736208 3086f5cd . . . 12345 TRACE_TRACKING_URL 0.000000 ExampleSystem https://localhost/index.php?stream:test#8.1433485415; sid:3086f5cd . . .;pts:0 200
```

-->

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE registra {#trace-transcoding-no-media-to-transcode}

Los registros de este tipo registran un elemento creativo de publicidad que falta. El único campo más allá de `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` aparece en la tabla.

| Campo | Tipo | Descripción |
|---|---|---|
| ad_id | string | ID de publicidad completa (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOCOLO:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLO: AUDITUDE,VAST) |

Los registros de este tipo registran los resultados de las solicitudes de transcodificación que el servidor de manifiesto envía a CRS. Los campos más allá de `TRACE_TRANSCODING_REQUESTED` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| ad_id | string | ID de publicidad completa |
| ad_manifest_url | string | Dirección URL del archivo de manifiesto de la publicidad, desde la respuesta del servidor de publicidad |
| creative_type | string | Tipo de medio |
| indicadores | string | ID3 indica si la solicitud de transcodificación incluye una solicitud para agregar una etiqueta ID3 |
| destinatario_duration | string | Duración del destinatario (segundos) del elemento creativo transcodificado |

Los registros de este tipo indican una solicitud para realizar el seguimiento del lado del servidor. Los campos más allá de `TRACE_TRACKING_REQUEST` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| tracking_url_count | integer | Número de direcciones URL de seguimiento |
| inicio | float | Tiempo de inicio del fragmento PTS (segundos con precisión milisegundos) |
| end | float | Tiempo de finalización del fragmento PTS (segundos con precisión milisegundos) |

Los registros de este tipo proporcionan una dirección URL de seguimiento para el seguimiento del lado del servidor. Los campos más allá de `TRACE_TRACKING_REQUEST_URL` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| timestamp | float | Tiempo (segundos, con precisión .001) dentro de la sesión de reproducción para hacer ping en la URL de seguimiento. |
| ad_system | string | Sistema de publicidad (por ejemplo, auditude) |
| url | string | Dirección URL de ping |

Registros de este tipo de solicitudes de registro que realiza el servidor de manifiesto para `WEBVTT` rótulos. Los campos más allá de `TRACE_WEBVTT_REQUEST` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| vtt_uri | string | URL para solicitud |
| inicio | float | Tiempo de inicio dividido (segundos con precisión milisegundos) |
| end | float | Tiempo de finalización dividido (segundos con precisión milisegundos) |

Registros de este tipo de respuestas de registro que el servidor de manifiesto envía a los clientes en `answer` a solicitudes de `WEBVTT` rótulos. Los campos más allá de `TRACE_WEBVTT_RESPONSE` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| response | string | Respuesta codificada en base64 enviada al cliente |

Registros de este tipo de respuestas de registro a solicitudes que el servidor de manifiesto realiza para `WEBVTT` rótulos. Los campos más allá de `TRACE_WEBVTT_SOURCE` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| source | string | Contenido de VTT original codificado en base64 |

Los registros de este tipo permiten que el servidor de manifiesto registre eventos e información que no se haya planificado de otro modo cuando ingesta publicidades. El campo más allá de `TRACE_MISC` consiste en una cadena de mensaje. Los mensajes que podrían aparecer incluyen lo siguiente:

* Anuncio omitido: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= seconds, ignore= ignore, redirectAd= redirectAd, priority= priority
* La colocación de la publicidad devolvió un valor nulo.
* La publicidad se ha vinculado correctamente.
* Error en la llamada de publicidad: mensaje de error.
* Añadiendo User-Agent para recuperar el manifiesto sin procesar: user-agent.
* Añadiendo cookie para recuperar el manifiesto sin procesar: #
* Mensaje de error de URL solicitada incorrecta. (No se pudo analizar la URL de variante)
* Dirección URL llamada: URL devuelta: código de respuesta. (URL en directo)
* Dirección URL llamada: Código de devolución de URL: código de respuesta. (URL de VOD)
* Conflicto encontrado al resolver anuncios: uno de los inicios de rodadura media o uno de los extremos de rodadura media se encuentra dentro de la prerodadura o de la prerodadura incluida en el rollo medio (VOD).
* Excepción no controlada detectada lanzada por el controlador para URI: URL de solicitud.
* Finalizó la generación del manifiesto de variante. (Variante)
* Finalizó la generación del manifiesto de variante.
* Excepción en la gestión de redireccionamiento VAST *redireccionamiento de URL *error: mensaje de error.
* No se pudo recuperar la lista de reproducción del anuncio para la dirección URL del manifiesto del anuncio.
* No se pudo generar el manifiesto de objetivo. (HLSManifestResolver)
* No se pudo analizar la respuesta de la primera llamada de publicidad: mensaje de error.
* No se pudo procesar *GET|POST *solicitud de ruta: URL de solicitud. (Activo/VOD)
* No se pudo procesar la solicitud de manifiesto activo: URL de solicitud. (Activo)
* Error al devolver un manifiesto de variante: mensaje de error.
* No se pudo validar la ID del grupo: ID del grupo.
* Obteniendo manifiesto sin procesar: dirección URL de contenido. (Activo)
* Redirección VAST siguiente: dirección URL de redireccionamiento.
* Se han encontrado recursos vacíos. (VOD)
* Se encontraron *publicidades de número*. (VOD)
* Solicitud HTTP recibida. (Muy primer mensaje)
* Se ignora el anuncio porque la diferencia entre la duración de la respuesta del anuncio (*duración de la respuesta del anuncio *s) y la duración real del anuncio (*duración real *s) es mayor que el límite. (HLSManifestResolver)
* Omitiendo el valor de avail que no proporcionó ningún valor de ID. (GroupAdResolver.java)
* Omitiendo el valor de tiempo promedio que proporcionó un valor de tiempo no válido: *time *for availId = avail ID.
* Omitiendo el valor de duración promedio que proporcionó un valor de duración no válido: *duration *for availId = avail ID.
* Inicialice una nueva sesión. (Variante)
* Método HTTP no válido. Debe ser un GET. (VOD)
* Método HTTP no válido. La solicitud de seguimiento debe ser una GET. (Activo)
* Mensaje de error de URL solicitada no válida. (Variante)
* Grupo no válido. (HLSManifestResolver)
* Solicitud no válida. El rótulo no es una solicitud de seguimiento válida. (VOD)
* Solicitud no válida. La solicitud de subtítulos debe realizarse después de que se establezca la sesión. (VOD)
* Solicitud no válida. La solicitud de seguimiento debe realizarse después de que se establezca la sesión. (VOD)
* Instancia de servidor no válida para el identificador de grupo de sobrecarga: ID del grupo. (Activo)
* Se ha alcanzado el límite de redirecciones VAST: número.
* Realizar llamada de publicidad: dirección URL de llamada de publicidad.
* No se encontró ningún manifiesto para: dirección URL de contenido. (Activo)
* No se encontró ningún valor coincidente para el ID de avail: ID de avail. (HLSManifestResolver)
* No se encontró ninguna sesión de reproducción. (HLSManifestResolver)
* Procesamiento de la solicitud de VOD para la URL de contenido de manifiesto.
* Procesando variante.
* Procesamiento de la solicitud de rótulo para la URL de contenido de manifiesto.
* Procesando solicitud de seguimiento. (VOD)
* La respuesta de anuncio de redireccionamiento está vacía. (VASTStAX)
* Solicitud: URL.
* Devolviendo la respuesta de error para la solicitud de GET porque no se encontró ninguna sesión de reproducción. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET debido a un error interno del servidor.
* Devolviendo la respuesta de error para la solicitud de GET que especifica un recurso no válido: ID de solicitud de publicidad. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET que especifica un ID de grupo no válido o vacío: ID del grupo. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET que especifica un valor de posición de seguimiento no válido. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET con sintaxis no válida: URL de solicitud. (Activo/VOD)
* Devolviendo respuesta de error para la solicitud con método HTTP no admitido: GET|POST. (Activo/VOD)
* Devolviendo el manifiesto desde la caché. (VOD)
* El servidor está sobrecargado. Continúe sin la solicitud de punteado de publicidad. (Variante)
* Inicio que genera el manifiesto objetivo. (HLSManifestResolver)
* Manifiesto de variante que genera inicios de: dirección URL de contenido. (Variante)
* Inicio de poner los anuncios en manifiesto. (VODHLSResolver)
* Intentando unir publicidad a `HH:MM:SS`: AdPlacement \[adManifestURL= ad Manifest URL, durationSeconds= segundos, ignore= ignorar, redirectAd= redireccionar publicidad, priority= prioridad.\] \(HLSManifestResolver\)
* No se pueden obtener publicidades debido a una cronología de tiempo no válida; se devolvió el contenido sin publicidades. (VOD)
* No se pueden obtener publicidades: se devolvió el contenido sin publicidades. (VOD)
* No se pudo obtener la consulta de la publicidad y no se proporcionó ninguna dirección URL de contenido. (VOD)
* Se recibió una dirección URL válida. (VOD/Variant)
* No se encontró la variante M3U8. (Variante)

### TRACE_PLAYBACK_PROGRESS registra {#trace-playback-progress-records}

El servidor de manifiesto genera registros de este tipo cuando recibe una señal sobre el progreso de la reproducción durante el flujo de trabajo de seguimiento del lado del servidor. Los campos más allá de `TRACE_PLAYBACK_PROGRESS` aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP |
| ancho de banda | integer | Ancho de banda del flujo |
| pt | integer | Tiempo de PTS dentro del flujo |
| ms_time | integer | Hora en que el servidor de manifiesto generó la dirección URL de seguimiento |
| url | string | Dirección URL de redireccionamiento |
| **¿** header_user_agent | string | Encabezado HTTP User-Agent |
| **¿** header_dnt | integer | Encabezado HTTP no rastrear |
| **¿** effective_remote_address | string | Dirección remota efectiva IPv4 |
| **¿Dirección** remota? | string | Dirección remota IPv4 |

**¿** Los últimos cuatro campos son opcionales.

## Flujos de velocidad de bits múltiples {#multiple-bitrate-streams}

Las solicitudes de inserción de anuncios del cliente suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiesto genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8.

El servidor de manifiesto utiliza la información de la solicitud de URL del Bootstrap del cliente para recuperar la lista de reproducción de la variante de contenido. Genera una nueva lista de reproducción de variante que contiene vínculos de servidor de manifiesto al contenido de nivel de flujo. El cliente los utiliza para crear solicitudes de inserción de anuncios. Los vínculos de contenido de nivel de flujo del servidor de manifiesto tienen el siguiente formato:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vodEl servidor de manifiesto establece este valor en función del tipo de lista de reproducción del contenido: Activo/lineal (
`#EXT-X-PLAYLIST-TYPE:EVENT`) o VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **ID única de**
publisherAssetIDPublisher para el contenido específico proporcionado en la solicitud de URL del Bootstrap.

* ****
representaciónEl servidor de manifiesto lo establece en función de la variable 
`BANDWIDTH` del flujo de contenido y lo utiliza para coincidir con la velocidad de bits de la publicidad con la velocidad de bits del contenido. La velocidad de bits del anuncio no puede superar la velocidad de bits del contenido a menos que la representación del anuncio con la velocidad de bits más baja lo haga.

* ****
groupIDTel servidor de manifiesto genera este valor y lo utiliza para asegurarse de que coloca las publicidades de forma coherente, independientemente de qué representaciones de velocidad de bits solicita publicidades el cliente.

* **url codificada en base64 del**
flujo de velocidad de bitsLa base64 segura para URL del servidor de manifiesto codifica la dirección URL absoluta del flujo de contenido. Cada flujo tiene su propia dirección URL.

* **Parámetros**
de consultaParámetros de consulta proporcionados en la solicitud de URL del Bootstrap.
