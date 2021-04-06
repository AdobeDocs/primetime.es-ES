---
title: Registro detallado
description: Registro detallado
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 0%

---

# Registro detallado {#verbose-logging}

## descripciones de eventos ptdebug/logging {#ptdebug-logging-events}

Al iniciar el registro de depuración para una sesión de servidor de manifiesto, puede añadir el parámetro `ptdebug` a la dirección URL de solicitud para especificar las siguientes opciones para la información que devuelve el servidor de manifiesto en los encabezados HTTP:

* `ptdebug=true`
Todos los registros excepto TRACE_HTTP_HEADER y la mayoría de los datos de llamada/respuesta de los registros TRACE_AD_CALL.

* `ptdebug=AdCall`
Solo los registros de tipo TRACE_AD_ (por ejemplo, TRACE_AD_CALL).

* `ptdebug=Header`
Solo registros TRACE_HTTP_HEADER.

## Formatos de los registros de registro {#log-record-formats}

Cada registro de registro tiene un tipo y un conjunto de campos, algunos de los cuales pueden ser opcionales. Los campos de todos los registros hasta el tipo de registro son los mismos. Proporcionan una marca de tiempo e información sobre la sesión. El tipo de registro identifica el tipo de evento que se registra y los campos posteriores proporcionan información sobre el evento registrado.

La estructura de un registro de registro es la siguiente:

`datetime request_id session_id zone_id record_type other fields`.

| Campo | Tipo | Descripción |
|---|---|---|
| datetime | string | Marca de tiempo |
| request_id | string | ID de solicitud utilizado por el servidor de manifiesto (Marca de tiempo Unix) |
| session_id | string | ID de sesión utilizado por el servidor de manifiesto |
| zone_id | integer | Zona |
| record_type | string | Tipo de evento que se registra |
| otros campos | variables | Depende del tipo de evento |

Los registros de este tipo registran los resultados de las solicitudes HTTP. Los campos más allá de `TRACE_REQUEST_INFO` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| request_method | string | Método HTTP (GET o POST) |
| request_uri | string | URI de solicitud HTTP (sin host) |
| request_length | integer | Longitud de la solicitud (bytes) |
| response_length | integer | Longitud de la respuesta (bytes) |
| delta | integer | Tiempo (milisegundos) para procesar la solicitud |
| module_type | string | Variant, Stream o VOD |
| remote_address_aud_client_ip | string | **}** |
| remote_address_x_fwd_for_hdr_key | string | **}** |
| remote_host_port | string | **}** |

**✓** Los tres últimos campos son opcionales.

**Un ejemplo**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER registra {#trace-http-header-records}

Registros de este tipo de encabezados HTTP de registro intercambiados durante llamadas HTTP entre el servidor de manifiesto y el cliente, el servidor de publicidad o el servidor de contenido. Los campos más allá de TRACE_HTTP_HEADER aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| request_type | string | Tipo de solicitud (PRINCIPAL o DESCONOCIDO) |
| request_response | string | Encabezado de respuesta (solicitud o respuesta) |
| header_name | string | Nombre de encabezado HTTP |
| header_value | string | Valor de encabezado HTTP codificado en base64 |

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

### Registros de TRACE_AD_CALL {#tracing-ad-call-records}

Los registros de este tipo registran los resultados de las solicitudes de anuncios del servidor de manifiesto. Los campos más allá de `TRACE_AD_CALL` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| request_duration | integer | Tiempo (milisegundos) de la solicitud a la respuesta |
| ad_server_query_url | string | URL de la llamada de anuncio, incluidos los parámetros de consulta |
| ad_system_id | string | Sistema de publicidad, desde la respuesta del servidor de publicidad (Auditude si no se especifica) |
| avail_id | string | ID del avail, desde la señal del anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| avail_duration | number | Duración (segundos) del avail, desde el cue de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| ad_server_response | string | Respuesta codificada en base64 desde el servidor de publicidad |

Un ejemplo:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE y TRACE_AD_REDIRECT registros {#trace-ad-insert-resolve-redirect}

Los registros de este tipo registran los resultados de las solicitudes de publicidad indicadas por el tipo de registro. Los campos más allá del tipo de registro aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Se ha devuelto el código de estado HTTP. |
| avail_id | string | ID del avail, desde la señal del anuncio en el archivo de manifiesto de contenido (activo) o desde el servidor de manifiestos (VOD). |
| ad_type | string | Tipo de anuncio (DIRECTO o REDIRECTO). |
| ad_duration | integer | Duración (segundos) del anuncio, desde la respuesta del servidor de publicidad. |
| ad_content_url | string | URL del archivo de manifiesto de la publicidad, desde la respuesta del servidor de publicidad. |
| **✓** ad_content_url_actual | string | URL del archivo de manifiesto del anuncio insertado. Vacío para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de publicidad, a partir de la respuesta del servidor de publicidad (Auditude si no se especifica). |
| ad_id | string | ID del anuncio, desde la respuesta del servidor de publicidad. |
| creative_id | string | ID del creativo, desde el nodo de publicidad, desde la respuesta del servidor de publicidad. |
| **✓** ad_call_id | string | No se usa. Reservado para uso futuro. |
| delta | integer | Tiempo (milisegundos) que tarda este evento. |
| **✓** misc | string | Motivo por el que se omitió el anuncio. |

**Los** `ad_content_url_actual`campos ✓  `ad_call_id`,  `misc`  y son opcionales.

>[!NOTE]
>
>Para `TRACE_AD_RESOLVE` y `TRACE_AD_INSERT`, la dirección URL en el campo `ad_content_url_actual` es para el transcodificado y si hay uno disponible. De lo contrario, el campo está vacío para `TRACE_AD_RESOLVE` o lo mismo que `ad_content_url` para `TRACE_AD_INSERT`.

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

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE registros {#trace-transcoding-no-media-to-transcode}

Los registros de este tipo registran un creativo de publicidad que falta. El único campo más allá de `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` aparece en la tabla.

| Campo | Tipo | Descripción |
|---|---|---|
| ad_id | string | ID de anuncio completo (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOCOLO:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLO: AUDITUDE,VAST) |

Los registros de este tipo registran los resultados de las solicitudes de transcodificación que el servidor de manifiestos envía a CRS. Los campos más allá de `TRACE_TRANSCODING_REQUESTED` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| ad_id | string | ID de publicidad completa |
| ad_manifest_url | string | URL del archivo de manifiesto de la publicidad, desde la respuesta del servidor de publicidad |
| creative_type | string | Tipo de medio |
| indicadores | string | ID3 indica si la solicitud de transcodificación incluye una solicitud para añadir una etiqueta ID3 |
| target_duration | string | Duración del objetivo (segundos) del creativo transcodificado |

Los registros de este tipo indican una solicitud para realizar un seguimiento del lado del servidor. Los campos más allá de `TRACE_TRACKING_REQUEST` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| tracking_url_count | integer | Número de direcciones URL de seguimiento |
| start | float | Tiempo de inicio del fragmento PTS (segundos con precisión de milisegundos) |
| end | float | Tiempo de finalización del fragmento PTS (segundos con precisión de milisegundos) |

Los registros de este tipo proporcionan una URL de seguimiento para el seguimiento del lado del servidor. Los campos más allá de `TRACE_TRACKING_REQUEST_URL` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| timestamp | float | Tiempo (segundos, con precisión .001) dentro de la sesión de reproducción para hacer ping en la URL de seguimiento. |
| ad_system | string | Sistema de publicidad (por ejemplo, auditude) |
| url | string | Dirección URL de ping |

Registros de este tipo de solicitudes de registro que realiza el servidor de manifiestos para `WEBVTT` subtítulos. Los campos más allá de `TRACE_WEBVTT_REQUEST` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| vtt_uri | string | URL para la solicitud |
| start | float | Tiempo de inicio dividido (segundos con precisión de milisegundos) |
| end | float | Tiempo de finalización dividido (segundos con precisión de milisegundos) |

Registros de este tipo de respuestas de registro que el servidor de manifiestos envía a los clientes en `answer` a solicitudes de `WEBVTT` subtítulos. Los campos más allá de `TRACE_WEBVTT_RESPONSE` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| response | string | Respuesta codificada Base64 enviada al cliente |

Registros de este tipo de respuestas de registro a solicitudes que realiza el servidor de manifiestos para `WEBVTT` subtítulos. Los campos más allá de `TRACE_WEBVTT_SOURCE` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP devuelto |
| source | string | Contenido VTT original codificado en base64 |

Los registros de este tipo permiten que el servidor de manifiesto registre eventos e información que de otra manera no se planifica para el momento de la ingesta de anuncios. El campo más allá de `TRACE_MISC` consiste en una cadena de mensaje. Los mensajes que pueden aparecer son los siguientes:

* Anuncio ignorado: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= seconds, ignore= ignore, redirectAd= redirectAd, priority= priority
* La ubicación de la publicidad devolvió un valor nulo.
* Se vinculó correctamente.
* Error en la llamada de anuncio : mensaje de error.
* Añadir User-Agent para recuperar el manifiesto sin procesar: user-agent.
* Añadir cookie para recuperar el manifiesto sin procesar: #
* Mensaje de error de URL solicitada incorrecta. (No se pudo analizar la URL de la variante)
* URL llamada: URL devuelta: código de respuesta. (URL en directo)
* URL llamada: Código de retorno de URL: código de respuesta. (URL de VOD)
* Conflicto encontrado al resolver anuncios: uno de: inicio de la emisión media o final de la emisión media se encuentra dentro del anuncio previo a la emisión o el anuncio previo a la emisión contenido en la emisión media (VOD).
* Excepción no controlada detectada lanzada por el controlador para URI: URL de solicitud.
* Se ha terminado de generar el manifiesto de variante. (Variante)
* Se ha terminado de generar el manifiesto de variante.
* Excepción en la gestión de redireccionamiento VAST *URL de redireccionamiento *error: mensaje de error.
* No se pudo recuperar la lista de reproducción del anuncio para la dirección URL del manifiesto del anuncio.
* No se pudo generar el manifiesto de destino. (HLSManifestResolver)
* No se pudo analizar la primera respuesta de llamada de anuncio: mensaje de error.
* No se pudo procesar *GET|POST *solicitud de ruta: URL de solicitud. (Activo/VOD)
* No se pudo procesar la solicitud de manifiesto activo: URL de solicitud. (Activo)
* No se pudo devolver un manifiesto de variante: mensaje de error.
* No se pudo validar el ID del grupo: ID del grupo.
* Recuperando manifiesto sin procesar: URL de contenido. (Activo)
* Redireccionamiento VAST siguiente: dirección URL de redireccionamiento.
* Se encontraron disponibles vacías. (VOD)
* Se encontraron *anuncios numéricos*. (VOD)
* Solicitud HTTP recibida. (Muy primer mensaje)
* Ignorando el anuncio porque la diferencia entre la duración de la respuesta del anuncio (*duración de la respuesta del anuncio *s) y la duración real del anuncio (*duración real *s) es mayor que el límite. (HLSManifestResolver)
* Omitir el valor de avail que no proporcionó ningún valor de ID. (GroupAdResolver.java)
* Omitiendo el valor de valor de tiempo no válido: *hora *para availId = ID de avail.
* Omitir el valor de avail que proporcionó un valor de duración no válido: *duración *para availId = ID de avail.
* Inicializar nueva sesión. (Variante)
* Método HTTP no válido. Debe ser un GET. (VOD)
* Método HTTP no válido. La solicitud de seguimiento debe ser una GET. (Activo)
* Mensaje de error de URL solicitada no válida. (Variante)
* Grupo no válido. (HLSManifestResolver)
* Solicitud no válida. El rótulo no es una solicitud de seguimiento válida. (VOD)
* Solicitud no válida. La solicitud de subtítulo debe realizarse una vez establecida la sesión. (VOD)
* Solicitud no válida. La solicitud de seguimiento debe realizarse una vez establecida la sesión. (VOD)
* Instancia de servidor no válida para el ID de grupo de sobrecarga: ID del grupo. (Activo)
* Límite de redirecciones VAST alcanzado: número.
* Realización de llamada de anuncio: dirección URL de la llamada de anuncio.
* No se encontró ningún manifiesto para: URL de contenido. (Activo)
* No se encontró ningún valor coincidente para el ID de avail: ID de avail. (HLSManifestResolver)
* No se encontró ninguna sesión de reproducción. (HLSManifestResolver)
* Procesamiento de la solicitud de VOD para la URL de contenido de manifiesto.
* Procesando variante.
* Procesamiento de la solicitud de rótulo para la URL de contenido de manifiesto.
* Procesando la solicitud de seguimiento. (VOD)
* La respuesta de la publicidad de redireccionamiento está vacía. ( VASTStAX)
* Solicitando: URL.
* Se devuelve la respuesta de error para la solicitud de GET porque no se encontró ninguna sesión de reproducción. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET debido a un error interno del servidor.
* Devolviendo la respuesta de error para la solicitud de GET que especifica un recurso no válido: ID de solicitud de anuncio. (VOD)
* Se devuelve una respuesta de error para una solicitud de GET que especifica un ID de grupo no válido o vacío: ID del grupo. (VOD)
* Se devuelve la respuesta de error para la solicitud de GET que especifica un valor de posición de seguimiento no válido. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET con sintaxis no válida: URL de solicitud. (Activo/VOD)
* Devolviendo la respuesta de error para la solicitud con un método HTTP no admitido: GET|POST. (Activo/VOD)
* Devolver manifiesto de la caché. (VOD)
* El servidor está sobrecargado. Continúe sin la solicitud de unión de anuncios. (Variante)
* Empiece a generar el manifiesto de destino. (HLSManifestResolver)
* Empiece a generar el manifiesto de variante desde: URL de contenido. (Variante)
* Empiece a vincular anuncios al manifiesto. (VODHLSResolver)
* Intentando unir el anuncio a `HH:MM:SS`: AdPlacement \[adManifestURL= ad Manifest URL, durationSeconds= seconds, ignore= ignore, redirectAd= redirect ad, priority= priority.\] \(HLSManifestResolver\)
* No se pueden obtener anuncios debido a una línea de tiempo no válida: se devolvió el contenido sin anuncios. (VOD)
* No se pueden obtener publicidades: se devolvió el contenido sin anuncios. (VOD)
* No se puede obtener la consulta de publicidad y no se ha proporcionado ninguna URL de contenido. (VOD)
* URL válida recibida. (VOD/Variant)
* No se encuentra la variante M3U8. (Variante)

### Registros de TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

El servidor de manifiesto genera registros de este tipo cuando recibe una señal sobre el progreso de reproducción durante el flujo de trabajo de seguimiento del lado del servidor. Los campos más allá de `TRACE_PLAYBACK_PROGRESS` aparecen en el orden que se muestra en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | string | Código de estado HTTP |
| ancho de banda | integer | Ancho de banda de la emisión |
| puntos | integer | Tiempo de PTS dentro del flujo |
| ms_time | integer | Hora a la que el servidor de manifiesto generó la URL de seguimiento |
| url | string | Dirección URL de redireccionamiento |
| **¿** header_user_agent | string | Encabezado HTTP User-Agent |
| **¿** header_dnt | integer | Encabezado HTTP no-do-track |
| **¿** effective_remote_address | string | Dirección remota efectiva IPv4 |
| **¿Dirección** remota? | string | Dirección remota IPv4 |

**¿** Los últimos cuatro campos son opcionales.

## Flujos de velocidad de bits múltiples {#multiple-bitrate-streams}

Las solicitudes de cliente para inserción de publicidad suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiestos genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8s.

El servidor de manifiesto utiliza la información de la solicitud URL del Bootstrap del cliente para recuperar la lista de reproducción de la variante de contenido. Genera una nueva lista de reproducción de variante que contiene vínculos de servidor de manifiesto al contenido de nivel de flujo. El cliente los utiliza para construir solicitudes de inserción de anuncios. Los vínculos de contenido de nivel de flujo del servidor de manifiesto tienen el siguiente formato:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vodEl servidor de manifiesto establece este valor en función del tipo de lista de reproducción del contenido: Live/linear (
`#EXT-X-PLAYLIST-TYPE:EVENT`) o VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* ****
ID exclusivo de publisherAssetIDPublisher para el contenido específico proporcionado en la solicitud de URL del Bootstrap.

* ****
renditionEl servidor de manifiesto lo establece en función de la variable 
`BANDWIDTH` del flujo de contenido y lo utiliza para hacer coincidir la velocidad de bits del anuncio con la velocidad de bits del contenido. La velocidad de bits del anuncio no puede superar la velocidad de bits del contenido a menos que lo haga la representación de anuncio con la tasa de bits más baja.

* ****
groupIDTel servidor de manifiestos genera este valor y lo utiliza para asegurarse de que coloca los anuncios de forma consistente, independientemente de las representaciones de velocidad de bits que el cliente solicite los anuncios.

* **url codificada en base64 del**
flujo de velocidad de bitsLa base64 segura para URL del servidor de manifiesto codifica la dirección URL absoluta del flujo de contenido. Cada flujo tiene su propia dirección URL.

* **Parámetros de**
consultaParámetros de consulta proporcionados en la solicitud de URL del Bootstrap.
