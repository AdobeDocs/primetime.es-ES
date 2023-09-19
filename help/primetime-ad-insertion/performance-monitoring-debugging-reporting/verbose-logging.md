---
title: Registro detallado
description: Registro detallado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---

# Registro detallado {#verbose-logging}

## descripciones de eventos de ptdebug/logging {#ptdebug-logging-events}

Al iniciar el registro de depuración para una sesión del servidor de manifiesto, puede agregar `ptdebug` a la URL de solicitud para especificar las siguientes opciones para la información que devuelve el servidor de manifiesto en los encabezados HTTP:

* `ptdebug=true`
Todos los registros excepto TRACE_HTTP_HEADER y la mayoría de los datos de llamada/respuesta de los registros TRACE_AD_CALL.

* `ptdebug=AdCall`
Solo los registros de tipo TRACE_AD_ (por ejemplo, TRACE_AD_CALL).

* `ptdebug=Header`
Solo registros TRACE_HTTP_HEADER.

## Formatos de los registros de registro {#log-record-formats}

Cada registro tiene un tipo y un conjunto de campos, algunos de los cuales pueden ser opcionales. Los campos de todos los registros hasta el tipo de registro son los mismos. Proporcionan una marca de tiempo e información sobre la sesión. El tipo de registro identifica el tipo de evento que se registra y los campos siguientes proporcionan información sobre el evento registrado.

La estructura de un registro es la siguiente:

`datetime request_id session_id zone_id record_type other fields`.

| Campo | Tipo | Descripción |
|---|---|---|
| datetime | cadena | Marca de tiempo |
| request_id | cadena | ID de solicitud utilizado por el servidor de manifiesto (marca de tiempo Unix) |
| session_id | cadena | ID de sesión utilizado por el servidor de manifiesto |
| zone_id | entero | Zona |
| record_type | cadena | Tipo de evento que se registra |
| otros campos | varía | Depender del tipo de evento |

Los registros de este tipo registran los resultados de las solicitudes HTTP. Campos más allá `TRACE_REQUEST_INFO` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | cadena | Código de estado HTTP devuelto |
| request_method | cadena | Método HTTP (GET o POST) |
| request_uri | cadena | URI de solicitud HTTP (sin host) |
| request_length | entero | Longitud de la solicitud (bytes) |
| response_length | entero | Longitud de la respuesta (bytes) |
| delta | entero | Tiempo (milisegundos) para procesar la solicitud |
| module_type | cadena | Variante, Flujo o VOD |
| remote_address_aud_client_ip | cadena | **‡** |
| dirección_remota_x_fwd_for_hdr_key | cadena | **‡** |
| puerto_host_remoto | cadena | **‡** |

**‡** Los tres últimos campos son opcionales.

**Un ejemplo**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Registros TRACE_HTTP_HEADER {#trace-http-header-records}

Los registros de este tipo registran los encabezados HTTP intercambiados durante las llamadas HTTP entre el servidor de manifiesto y el cliente, el servidor de publicidad o el servidor de contenido. Los campos que se encuentran más allá de TRACE_HTTP_HEADER aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| request_type | cadena | Tipo de solicitud (PRINCIPAL o DESCONOCIDA) |
| request_response | cadena | Encabezado de respuesta (solicitud o respuesta) |
| header_name | cadena | Nombre del encabezado HTTP |
| header_value | cadena | Valor de encabezado HTTP codificado en Base64 |

>[!NOTE]
>
>El `request_type` y `header_value` Los campos de son opcionales.

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

Los registros de este tipo registran los resultados de las solicitudes de anuncios del servidor de manifiesto. Campos más allá `TRACE_AD_CALL` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | cadena | Código de estado HTTP devuelto |
| request_duration | entero | Tiempo (milisegundos) desde la solicitud hasta la respuesta |
| ad_server_query_url | cadena | URL para la llamada de anuncio, incluidos los parámetros de consulta |
| ad_system_id | cadena | Sistema de publicidad, desde la respuesta del servidor de publicidad (Auditude si no se especifica) |
| avail_id | cadena | ID de la ventaja, de la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| avail_duration | número | Duración (segundos) de la disponibilidad, desde la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| ad_server_response | cadena | Respuesta codificada en Base64 del servidor de publicidad |

Un ejemplo:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### Registros TRACE_AD_INSERT, TRACE_AD_RESOLVE y TRACE_AD_REDIRECT {#trace-ad-insert-resolve-redirect}

Los registros de este tipo registran los resultados de las solicitudes de publicidad indicadas por el tipo de registro. Los campos que se encuentran más allá del tipo de registro aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | cadena | Código de estado HTTP devuelto. |
| avail_id | cadena | ID de la utilidad, desde la señal de anuncio en el archivo de manifiesto de contenido (activo) o desde el servidor de manifiesto (VOD). |
| ad_type | cadena | Tipo de anuncio (DIRECTO o REDIRECTO). |
| ad_duration | entero | Duración (segundos) de la publicidad, desde la respuesta del servidor de publicidad. |
| ad_content_url | cadena | URL del archivo de manifiesto del anuncio, desde la respuesta del servidor de publicidad. |
| **†** ad_content_url_actual | cadena | URL del archivo de manifiesto del anuncio insertado. Vacío para TRACE_AD_REDIRECT. |
| ad_system_id | cadena | Sistema de publicidad, desde la respuesta del servidor de publicidad (Auditude si no se especifica). |
| ad_id | cadena | ID del anuncio, de la respuesta del servidor de publicidad. |
| creative_id | cadena | ID del creativo, desde el nodo de publicidad, desde la respuesta del servidor de publicidad. |
| **†** ad_call_id | cadena | No se usa. Reservado para uso futuro. |
| delta | entero | Tiempo (milisegundos) empleado por este evento. |
| **†** varios | cadena | Motivo por el que se omitió el anuncio. |

**†** `ad_content_url_actual`, `ad_call_id`, y `misc` Los campos de son opcionales.

>[!NOTE]
>
>Para `TRACE_AD_RESOLVE` y `TRACE_AD_INSERT`, la dirección URL en `ad_content_url_actual` El campo es para la transcodificación y si hay una disponible. De lo contrario, el campo está vacío para `TRACE_AD_RESOLVE` o igual que `ad_content_url` para `TRACE_AD_INSERT`.

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

### Registros TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE {#trace-transcoding-no-media-to-transcode}

Los registros de este tipo registran la falta de creatividad publicitaria. El único campo más allá `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` aparece en la tabla.

| Campo | Tipo | Descripción |
|---|---|---|
| ad_id | cadena | ID de anuncio completo (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLO: AUDITUDE,VAST) |

Los registros de este tipo registran los resultados de las solicitudes de transcodificación que el servidor de manifiesto envía a CRS. Campos más allá `TRACE_TRANSCODING_REQUESTED` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| ad_id | cadena | ID de anuncio completo |
| ad_manifest_url | cadena | URL del archivo de manifiesto del anuncio, desde la respuesta del servidor de publicidad |
| creative_type | cadena | Tipo de medios |
| banderas | cadena | ID3 indica si la solicitud de transcodificación incluye una solicitud para agregar una etiqueta ID3 |
| target_duration | cadena | Duración de destino (segundos) del creativo transcodificado |

Los registros de este tipo indican una solicitud para realizar el seguimiento del lado del servidor. Campos más allá `TRACE_TRACKING_REQUEST` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| tracking_url_count | entero | Número de URL de seguimiento |
| start | float | Tiempo de inicio del fragmento PTS (segundos con precisión de milisegundos) |
| fin | float | Tiempo de finalización del fragmento PTS (segundos con precisión de milisegundos) |

Los registros de este tipo proporcionan una dirección URL de seguimiento para el seguimiento del lado del servidor. Campos más allá `TRACE_TRACKING_REQUEST_URL` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| timestamp | float | Tiempo (segundos, con precisión 0,001) dentro de la sesión de reproducción para hacer ping a la URL de seguimiento. |
| ad_system | cadena | Sistema de publicidad (por ejemplo, audiencia) |
| url | cadena | URL para ping |

Registros de este tipo para los que el servidor de manifiesto realiza solicitudes de registro `WEBVTT` subtítulos. Campos más allá `TRACE_WEBVTT_REQUEST` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | cadena | Código de estado HTTP devuelto |
| vtt_uri | cadena | URL para la solicitud |
| start | float | Tiempo de inicio dividido (segundos con precisión de milisegundos) |
| fin | float | Tiempo de fin de división (segundos con precisión de milisegundos) |

Los registros de este tipo registran las respuestas que el servidor de manifiesto envía a los clientes en `answer` a solicitudes de `WEBVTT` subtítulos. Campos más allá `TRACE_WEBVTT_RESPONSE` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | cadena | Código de estado HTTP devuelto |
| respuesta | cadena | Respuesta codificada en Base64 enviada al cliente |

Los registros de este tipo registran las respuestas a las solicitudes realizadas por el servidor de manifiesto para `WEBVTT` subtítulos. Campos más allá `TRACE_WEBVTT_SOURCE` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | cadena | Código de estado HTTP devuelto |
| origen | cadena | Contenido VTT original con codificación Base64 |

Los registros de este tipo permiten que el servidor de manifiesto registre eventos e información que no se planea de otra manera cuando ingiere anuncios. El campo más allá `TRACE_MISC` consiste en una cadena de mensaje. Los mensajes que pueden aparecer son los siguientes:

* Anuncio omitido: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= segundos, ignore= omitir, redirectAd= redirectAd, priority= prioridad
* La ubicación del anuncio devolvió un valor nulo.
* Anuncio vinculado correctamente.
* Error en la llamada de anuncio: mensaje de error.
* Agregando el agente de usuario para recuperar el manifiesto sin procesar: user-agent.
* Agregando cookie para recuperar manifiesto sin procesar: #
* Mensaje de error de URL solicitada de URL incorrecta. (Error al analizar la URL de variante)
* URL llamada: la URL obtuvo el código de respuesta devuelto:. ( Dirección URL activa)
* URL llamada: código de retorno de URL: código de respuesta. ( URL de VOD)
* Se ha encontrado un conflicto al resolver los anuncios: uno de los siguientes: inicio durante la emisión o final durante la emisión está dentro del anuncio previo a la emisión o del anuncio previo a la emisión contenido en el anuncio durante la emisión (VOD).
* Se ha detectado una excepción no controlada generada por el controlador para URI: URL de solicitud.
* Finalizó la generación del manifiesto de variante. (Variante)
* Finalizó la generación del manifiesto de variante.
* Excepción al gestionar el redireccionamiento de VAST *redirect URL *error: mensaje de error.
* Error al recuperar la lista de reproducción del anuncio para la URL de manifiesto del anuncio.
* Error al generar manifiesto de destino. (HLSManifestResolver)
* Error al analizar la primera respuesta de llamada de anuncio: mensaje de error.
* Error al procesar la solicitud del GET POST para la ruta: URL de solicitud. (Activo/VOD)
* Error al procesar la solicitud de manifiesto activa: URL de solicitud. (Activo)
* Error al devolver un manifiesto de variante: mensaje de error.
* Error al validar el ID de grupo: ID de grupo.
* Obteniendo manifiesto sin procesar: URL de contenido. (Activo)
* Después del redireccionamiento VAST: URL de redireccionamiento.
* Se han encontrado disponibilidades vacías. (VOD)
* Encontrado *número* anuncios. (VOD)
* Solicitud HTTP recibida. (Primer mensaje)
* Se ignora el anuncio porque la diferencia entre la duración de la respuesta del anuncio (*duración de la respuesta del anuncio *s) y la duración del anuncio real (*duración real *s) es mayor que el límite. (HLSManifestResolver)
* Se ignoran las variables que no proporcionaron ningún valor de ID. (GroupAdResolver.java)
* Se omitirá la variable que proporcionó un valor de tiempo no válido: *time *for availId = avail ID.
* Se omitirá la variable que proporcionó un valor de duración no válido: *duration *for availId = avail ID.
* Inicializar nueva sesión. (Variante)
* Método HTTP no válido. Debe ser un GET. (VOD)
* Método HTTP no válido. La solicitud de seguimiento debe ser una GET. (Activo)
* Mensaje de error de URL solicitada no válida. (Variante)
* Grupo no válido. (HLSManifestResolver)
* Solicitud no válida. El pie de ilustración no es una solicitud de seguimiento válida. (VOD)
* Solicitud no válida. La solicitud de rótulo debe realizarse una vez establecida la sesión. (VOD)
* Solicitud no válida. La solicitud de seguimiento debe realizarse después de establecer la sesión. (VOD)
* Instancia de servidor no válida para el ID de grupo de sobrecarga: ID de grupo. (Activo)
* Se alcanzó el límite de redirecciones VAST: número.
* Realización de una llamada de anuncio: URL de llamada de anuncio.
* No se ha encontrado ningún manifiesto para: URL de contenido. (Activo)
* No se ha encontrado ningún valor coincidente para el ID de disponibilidad: ID de disponibilidad. (HLSManifestResolver)
* No se ha encontrado ninguna sesión de reproducción. (HLSManifestResolver)
* Procesando solicitud de VOD para URL de contenido de manifiesto.
* Variante de procesamiento.
* Procesando solicitud de rótulo para la URL de contenido de manifiesto.
* Procesando solicitud de seguimiento. (VOD)
* Respuesta de anuncio de redirección vacía. ( VASTStAX)
* Solicitando: URL.
* Devolviendo respuesta de error para la solicitud de GET porque no se encontró ninguna sesión de reproducción. (VOD)
* Devolver la respuesta de error para la solicitud de GET debido a un error interno del servidor.
* Devolviendo respuesta de error para la solicitud de GET que especifica un recurso no válido: ID de solicitud de anuncio. (VOD)
* Devolución de una respuesta de error para una solicitud de GET que especifica un ID de grupo no válido o vacío: ID de grupo. (VOD)
* Devolviendo respuesta de error para la solicitud de GET que especifica un valor de posición de seguimiento no válido. (VOD)
* Devolviendo respuesta de error para la solicitud de GET con sintaxis no válida: URL de solicitud. (Activo/VOD)
* Devolviendo respuesta de error para la solicitud con método HTTP no compatible: GET|POST. (Activo/VOD)
* Devolviendo manifiesto de la caché. (VOD)
* Servidor sobrecargado. Continuar sin solicitud de vinculación de publicidad. (Variante)
* Inicie la generación del manifiesto de destino. (HLSManifestResolver)
* Comience a generar el manifiesto de variante desde: URL de contenido. (Variante)
* Empiece a vincular anuncios al manifiesto. (VODHLSResolver)
* Intentando unir el anuncio en `HH:MM:SS`: AdPlacement \[adManifestURL= URL de manifiesto de anuncio, durationSeconds= segundos, ignore= omitir, redirectAd= anuncio de redireccionamiento, priority= prioridad.\] \(HLSManifestResolver\)
* No se pueden obtener anuncios debido a un pttimeline no válido; se ha devuelto el contenido sin anuncios. (VOD)
* No se han podido obtener los anuncios - ha devuelto el contenido sin anuncios. (VOD)
* No se pudo obtener la consulta del anuncio y no se proporcionó ninguna dirección URL de contenido. (VOD)
* URL válida recibida. (VOD/Variante)
* No se ha encontrado la variante M3U8. (Variante)

### Registros TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

El servidor de manifiesto genera registros de este tipo cuando recibe una señal sobre el progreso de reproducción durante el flujo de trabajo de seguimiento del lado del servidor. Campos más allá `TRACE_PLAYBACK_PROGRESS` aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|---|---|---|
| status | cadena | Código de estado HTTP |
| ancho de banda | entero | Ancho de banda de la secuencia |
| pts | entero | Tiempo de PTS dentro del flujo |
| ms_time | entero | Hora a la que el servidor de manifiesto generó la URL de seguimiento |
| url | cadena | URL de redireccionamiento |
| **¿** header_user_agent | cadena | Encabezado de agente de usuario HTTP |
| **¿** header_dnt | entero | Encabezado HTTP do-not-track |
| **¿** Effective_remote_address | cadena | Dirección remota efectiva IPv4 |
| **¿** remote_address | cadena | Dirección remota IPv4 |

**¿** Los últimos cuatro campos son opcionales.

## Varias secuencias de velocidad de bits {#multiple-bitrate-streams}

Las solicitudes de los clientes para la inserción de anuncios suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiesto genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8.

El servidor de manifiesto utiliza la información de la solicitud de URL del Bootstrap del cliente para recuperar la lista de reproducción de la variante de contenido. Genera una nueva lista de reproducción de variante que contiene vínculos de servidor de manifiesto al contenido de nivel de flujo. El cliente los utiliza para construir solicitudes de inserción de publicidad. Los vínculos de contenido de nivel de flujo del servidor de manifiesto tienen el siguiente formato:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/vod**
El servidor de manifiesto establece este valor en función del tipo de lista de reproducción del contenido: Live/linear (`#EXT-X-PLAYLIST-TYPE:EVENT`) o VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **publisherAssetID**
ID único del publicador para el contenido específico proporcionado en la solicitud de URL del Bootstrap.

* **representación**
El servidor de manifiestos lo establece en función de lo siguiente `BANDWIDTH` valor del flujo de contenido y lo utiliza para hacer coincidir la velocidad de bits del anuncio con la velocidad de bits del contenido. La velocidad de bits del anuncio no puede superar la velocidad de bits del contenido a menos que lo haga la representación del anuncio con la velocidad de bits más baja.

* **groupID**
El servidor de manifiestos genera este valor y lo utiliza para asegurarse de que coloca anuncios de forma coherente, independientemente de las representaciones de velocidad de bits para las que el cliente solicite los anuncios.

* **url codificada en base64 del flujo de velocidad de bits**
El servidor de manifiesto URL-safe base64 codifica la URL absoluta de la secuencia de contenido. Cada flujo tiene su propia URL.

* **Parámetros de consulta**
Parámetros de consulta proporcionados en la solicitud de URL del Bootstrap.
