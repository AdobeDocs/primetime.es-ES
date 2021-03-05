---
title: Herramienta de depuración del servidor de manifiesto
seo-title: Herramienta de depuración del servidor de manifiesto
description: Herramienta de depuración del servidor de manifiesto
seo-description: Herramienta de depuración del servidor de manifiesto
uuid: 0b4f06f5-4b1f-4f88-980a-5b4df28e0094
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiquuid: 00b49659-ce56-4b5c-87cd-c357a0936641
donotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 0%

---


# Herramienta de depuración del servidor de manifiesto {#manifest-server-debugging-tool}

La herramienta de depuración permite a los editores investigar problemas de inserción de anuncios potencialmente costosos examinando la información de depuración devuelta en tiempo real por el servidor de manifiesto en los encabezados HTTP o, cuando se necesita información más detallada, examinando los registros de sesión después de los hechos. Los socios de Adobe como Akamai pueden utilizar la herramienta para depurar sus integraciones con Primetime y la toma de decisiones.

La herramienta admite problemas de depuración e inserción en cualquiera de las configuraciones principales del servidor de manifiesto y del seguimiento de anuncios:

* Seguimiento del lado del cliente con un reproductor basado en TVSDK.
* Seguimiento del lado del cliente con un reproductor no basado en TVSDK.
* Seguimiento del lado del servidor.

Para admitir todos estos casos, la herramienta no requiere ni utiliza códigos de editor del reproductor.

Al iniciar una sesión de servidor de manifiesto, puede establecer un parámetro en la dirección URL de la solicitud para pedirle que registre la información de depuración. Si utiliza diferentes valores de ese parámetro, también puede solicitar al servidor de manifiesto que devuelva determinados fragmentos de información de depuración en encabezados HTTP, pero los encabezados sólo pueden contener una cantidad limitada de información. Puede obtener las credenciales de Adobe para acceder a archivos de registro completos, que el servidor de manifiesto guarda periódicamente (por ejemplo, cada hora) en un servidor de archivos. Una vez que tenga las credenciales de ese servidor, puede acceder a él directamente en cualquier momento.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Opciones de la herramienta de depuración {#debugging-tool-options}

Al invocar la herramienta de depuración, tiene varias opciones para la información que devuelve el servidor de manifiesto en los encabezados HTTP. Las opciones no afectan a lo que el servidor de manifiesto coloca en los archivos de registro.

### Especificación de ptdebug {#specifying-ptdebug}

Al iniciar el registro de depuración para una sesión de servidor de manifiesto, puede agregar el parámetro ptdebug a la dirección URL de la solicitud para especificar las siguientes opciones para la información que devuelve el servidor de manifiesto en los encabezados HTTP:

* ptdebug=true Todos los registros excepto `TRACE_HTTP_HEADER` y la mayoría `call/response data` de `TRACE_AD_CALL` registros.
* ptdebug=AdCall Sólo registros TRACE_AD_*tipo* (por ejemplo, TRACE_AD_CALL).
* ptdebug=Sólo encabezado Registros TRACE_HTTP_HEADER.

Las opciones no afectan a lo que el servidor de manifiesto coloca en los archivos de registro. Usted no tiene control de eso, pero los archivos de registro son archivos de texto, por lo que puede aplicar una amplia variedad de herramientas para extraer y cambiar el formato de la información que le interesa.

Este es un ejemplo del encabezado HTTP que se devuelve cuando `ptdebug=Header`. Algunas cadenas largas de dígitos hexadecimales se reemplazan por `. . .` para mayor claridad.

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## Formatos de registros {#formats-of-log-records}

Cada registro de registro tiene un tipo y un conjunto de campos, algunos de los cuales pueden ser opcionales. Los campos de todos los registros hasta el tipo de registro son los mismos. Proporcionan una marca de hora e información sobre la sesión. El tipo de registro identifica el tipo de evento que se registra y los campos posteriores proporcionan información sobre el evento registrado.

La estructura de un registro de registro es la siguiente:

`datetime request_id session_id zone_id record_type` *otros campos.*

| Campo | Tipo | Descripción |
|--- |--- |--- |
| datetime | string | Marca de hora |
| request_id | string | Id. de solicitud utilizado por el servidor de manifiesto (marca de tiempo unix) |
| session_id | string | Id. de sesión utilizado por el servidor de manifiesto |
| zone_id | integer | Id. de zona |
| record_type | string | Tipo de evento que se registra |
| otros campos | *** | Depende del tipo de evento |

### Registros de TRACE_REQUEST_INFO {#trace-request-info-records}

Los registros de este tipo registran los resultados de las solicitudes HTTP. Los campos más allá de TRACE_REQUEST_INFO aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | string | Código de estado HTTP devuelto |
| request_method | string | Método HTTP (GET o POST) |
| request_uri | string | URI de solicitud HTTP (sin host) |
| request_length | integer | Duración de la solicitud (bytes) |
| response_length | integer | Duración de la respuesta (bytes) |
| delta | integer | Tiempo (milisegundos) para procesar la solicitud |
| module_type | string | Variant, Stream o VOD |
| remote_address_aud_client_ip | string | (véase la nota) |
| remote_address_x_fwd_for_hdr_key | string | (véase la nota) |
| remote_host_port | string | (véase la nota) |

>[!NOTE]
>
>Los tres últimos campos son opcionales.

Un ejemplo:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Registros TRACE_HTTP_HEADER {#trace-http-header-records}

Registros de este tipo registran encabezados HTTP intercambiados durante llamadas HTTP entre el servidor de manifiesto y el cliente, el servidor de publicidad o el servidor de contenido. Los campos más allá de TRACE_HTTP_HEADER aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| request_type | string | Tipo de solicitud (PRINCIPAL o DESCONOCIDO) |
| request_response | string | Encabezado de respuesta (solicitud o respuesta) |
| header_name | string | Nombre de encabezado HTTP |
| header_value | string | Valor de encabezado HTTP con codificación base64 |

>[!NOTE]
>
>Los campos request_type y header_value son opcionales.

Un ejemplo:

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### Registros TRACE_AD_CALL {#trace-ad-call-records}

Los registros de este tipo registran los resultados de las solicitudes de publicidad de servidor de manifiesto. Los campos más allá de TRACE_AD_CALL aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | string | Código de estado HTTP devuelto |
| request_duration | integer | Tiempo (milisegundos) entre la solicitud y la respuesta |
| ad_server_consulta_url | string | Dirección URL de la llamada de publicidad, incluidos los parámetros de consulta |
| ad_system_id | string | Sistema de publicidad, desde la respuesta del servidor de publicidad (Auditude si no se especifica) |
| avail_id | string | ID del valor, de la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| avail_duration | number | Duración (segundos) del valor promedio, a partir de la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| ad_server_response | string | Respuesta codificada en base64 del servidor de publicidad |

Un ejemplo:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE y TRACE_AD_REDIRECT registros {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

Los registros de este tipo registran los resultados de las solicitudes de publicidad indicadas por el tipo de registro. Los campos más allá del tipo de registro aparecen en el orden que se muestra en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | string | Código de estado HTTP devuelto |
| avail_id | string | ID del archivo de avail, de la señal de anuncio en el archivo de manifiesto de contenido (activo) o del servidor de manifiesto (VOD) |
| ad_type | string | Tipo de publicidad (DIRECTA o REDIRECTA) |
| ad_duration | integer | Duración (segundos) del anuncio, desde la respuesta del servidor de publicidad |
| ad_content_url | string | Dirección URL del archivo de manifiesto de la publicidad, desde la respuesta del servidor de publicidad |
| ad_content_url_actual | string | Dirección URL del archivo de manifiesto de la publicidad insertada. Vacío para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de publicidad, desde la respuesta del servidor de publicidad (Auditude si no se especifica) |
| ad_id | string | ID de la publicidad, desde la respuesta del servidor de publicidad |
| creative_id | string | ID del elemento creativo, desde el nodo de publicidad, desde la respuesta del servidor de publicidad |
| ad_call_id | string | No se usa. Reservado para uso futuro. |
| delta | integer | Tiempo (milisegundos) que tarda este evento |
| misc | string | Motivo por el que se omitió la publicidad |

>[!NOTE]
>
>Los campos ad_content_url_actual, ad_call_id y misc son opcionales.

Para TRACE_AD_RESOLVE y TRACE_AD_INSERT, la dirección URL en el campo ad_content_url_actual es para la publicidad transcodificada si hay una disponible. De lo contrario, el campo está vacío para TRACE_AD_RESOLVE o lo mismo que ad_content_url para TRACE_AD_INSERT.

Un ejemplo:

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

### Registros de TRACE_TRACKING_URL {#trace-tracking-url-records}

Los registros de este tipo registran los resultados de las solicitudes de publicidad de servidor de manifiesto. Los campos más allá de TRACE_TRACKING_URL aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| pt | number | Marca de hora de programa. Tiempo dentro del video para llamar a la dirección URL. |
| ad_system | string | Sistema de publicidad (audiencia o rueda libre) |
| url | string | Ping de URL |
| status | string | Estado HTTP devuelto por el ping |

Un ejemplo:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE registra {#trace-transcoding-no-media-to-transcode-records}

Los registros de este tipo registran un elemento creativo de publicidad que falta. El único campo más allá de TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE aparece en la tabla.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| ad_id | string | ID de publicidad completa `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` PROTOCOLO: AUDITUDE,VAST) |

### Registros TRACE_TRANSCODING_REQUESTED {#trace-transcoding-requested-records}

Los registros de este tipo registran los resultados de las solicitudes de transcodificación que el servidor de manifiesto envía a CRS. Los campos más allá de TRACE_TRANSCODING_REQUESTED aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| ad_id | string | ID de publicidad completa |
| ad_manifest_url | string | Dirección URL del archivo de manifiesto de la publicidad, desde la respuesta del servidor de publicidad |
| creative_type | string | Tipo de medio |
| indicadores | string | ID3 indica si la solicitud de transcodificación incluye una solicitud para agregar una etiqueta ID3 |
| destinatario_duration | string | Duración del destinatario (segundos) del elemento creativo transcodificado |

### Registros TRACE_TRACKING_REQUEST {#trace-tracking-request-records}

Los registros de este tipo indican una solicitud para realizar el seguimiento del lado del servidor. Los campos más allá de TRACE_TRACKING_REQUEST aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| tracking_url_count | integer | Número de direcciones URL de seguimiento |
| inicio | float | Tiempo de inicio del fragmento PTS (segundos con precisión milisegundos) |
| end | float | Tiempo de finalización del fragmento PTS (segundos con precisión milisegundos) |

### TRACE_TRACKING_REQUEST_URL registra {#trace-tracking-request-url-records}

Los registros de este tipo proporcionan una dirección URL de seguimiento para el seguimiento del lado del servidor. Los campos más allá de TRACE_TRACKING_REQUEST_URL aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| timestamp | float | Tiempo (segundos, con precisión .001) dentro de la sesión de reproducción para hacer ping en la URL de seguimiento |
| ad_system | string | Sistema de publicidad (por ejemplo, auditude) |
| url | string | Dirección URL de ping |

### TRACE_WEBVTT_REQUEST registra {#trace-webvtt-request-records}

Registros de este tipo de solicitudes de registro que el servidor de manifiesto realiza para los rótulos WEBVTT. Los campos más allá de TRACE_WEBVTT_REQUEST aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | string | Código de estado HTTP devuelto |
| vtt_uri | string | URL para solicitud |
| inicio | float | Tiempo de inicio dividido (segundos con precisión milisegundos) |
| end | float | Tiempo de finalización dividido (segundos con precisión milisegundos) |

### Registros TRACE_WEBVTT_RESPONSE {#trace-webvtt-response-records}

Registra ``of ``este ``type ``registro ``responses ``del ``manifest ``servidor ``sends ``a ``clients ``en `` `answer` ``a ``requests `` `for` ``WEBVTT ``subtítulos. Los campos más allá de TRACE_WEBVTT_RESPONSE &quot;aparecen en el orden mostrado en la tabla, separadas por `by`fichas.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | string | Código de estado HTTP devuelto |
| response | string | Respuesta codificada en base64 enviada al cliente |

### Registros de TRACE_WEBVTT_SOURCE {#trace-webvtt-source-records}

Registros de este tipo de respuestas de registro a solicitudes que el servidor de manifiesto realiza para subtítulos WEBVTT. Los campos más allá de TRACE_WEBVTT_SOURCE aparecen en el orden que se muestra en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | string | Código de estado HTTP devuelto |
| source | string | Contenido de VTT original codificado en base64 |


### Registros de TRACE_MISC {#trace-misc-records}

Los registros de este tipo permiten que el servidor de manifiesto registre eventos e información que no se haya planificado de otro modo cuando ingesta publicidades. El campo más allá de TRACE_MISC consiste en una cadena de mensaje. Los mensajes que podrían aparecer incluyen lo siguiente:

* Anuncio omitido:AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*segundos*, ignore=*ignore*, redirectAd=*redirectAd*, priority=*prioridad*
* La colocación de la publicidad devolvió un valor nulo.
* La publicidad se ha vinculado correctamente.
* Error en la llamada de publicidad: *mensaje de error*.
* Añadiendo User-Agent para recuperar el manifiesto sin procesar: *user-agent*.
* Añadiendo cookie para recuperar el manifiesto sin procesar: [cookie]
* Mensaje de error de URL *solicitada* incorrecta. (No se pudo analizar la URL de variante)
* Dirección URL llamada: La dirección URL *obtuvo retorno: código de respuesta*. (URL en directo)
* Dirección URL llamada: URL *código de retorno: código de respuesta*. (URL de VOD)
* Conflicto encontrado al resolver anuncios: uno de los inicios de rodadura media o uno de los extremos de rodadura media se encuentra dentro de la prerodadura o de la prerodadura incluida en el rollo medio (VOD).
* Excepción no controlada detectada lanzada por el controlador para URI: *URL de solicitud*.
* Finalizó la generación del manifiesto de variante. (Variante)
* Finalizó la generación del manifiesto de variante.
* Excepción en la gestión de redireccionamiento VAST *redireccionamiento de URL *error: *mensaje de error*.
* No se pudo recuperar la lista de reproducción de la publicidad para *URL de manifiesto de publicidad*.
* No se pudo generar el manifiesto de objetivo. (HLSManifestResolver)
* No se pudo analizar la respuesta de la primera llamada de publicidad: *mensaje de error*.
* No se pudo procesar *GET|POST *solicitud de ruta: *URL de solicitud*. (Activo/VOD)
* No se pudo procesar la solicitud de manifiesto activo: *URL de solicitud*. (Activo)
* Error al devolver un manifiesto de variante: *mensaje de error*.
* No se pudo validar la ID del grupo: *id. de grupo*.
* Obteniendo manifiesto sin procesar: *dirección URL de contenido*. (Activo)
* Redirección VAST siguiente: *dirección URL de redireccionamiento*.
* Se han encontrado recursos vacíos. (VOD)
* Se encontró *número *anuncios. (VOD)
* Solicitud HTTP recibida. (Muy primer mensaje)
* Se ignora el anuncio porque la diferencia entre la duración de la respuesta del anuncio (*duración de la respuesta del anuncio *s) y la duración real del anuncio (*duración real *s) es mayor que el límite. (HLSManifestResolver)
* Omitiendo el valor de avail que no proporcionó ningún valor de ID. (GroupAdResolver.java)
* Omitiendo el valor de tiempo promedio que proporcionó un valor de tiempo no válido: *time *for availId = *ID de avail*.
* Omitiendo el valor de duración promedio que proporcionó un valor de duración no válido: *duration *para availId = *ID de avail*.
* Inicialice una nueva sesión. (Variante)
* Método HTTP no válido. Debe ser un GET. (VOD)
* Método HTTP no válido. La solicitud de seguimiento debe ser una GET. (Activo)
* Dirección URL *solicitada no válida. Mensaje de error de dirección URL*. (Variante)
* Grupo no válido. (HLSManifestResolver)
* Solicitud no válida. El rótulo no es una solicitud de seguimiento válida. (VOD)
* Solicitud no válida. La solicitud de subtítulos debe realizarse después de que se establezca la sesión. (VOD)
* Solicitud no válida. La solicitud de seguimiento debe realizarse después de que se establezca la sesión. (VOD)
* Instancia de servidor no válida para el identificador de grupo de sobrecarga: *id. de grupo*. (Activo)
* Se ha alcanzado el límite de redirecciones VAST: *número*.
* Realizar llamada de publicidad: *dirección URL de llamada de publicidad*.
* No se encontró ningún manifiesto para: *dirección URL de contenido*. (Activo)
* No se encontró ningún valor coincidente para el ID de avail: *ID de avail*. (HLSManifestResolver)
* No se encontró ninguna sesión de reproducción. (HLSManifestResolver)
* Procesando solicitud de VOD para la dirección URL de contenido *de manifiesto*.
* Procesando variante.
* Procesando solicitud de rótulo para la dirección URL de contenido *de manifiesto*.
* Procesando solicitud de seguimiento. (VOD)
* La respuesta de anuncio de redireccionamiento está vacía. (VASTStAX)
* Solicitud: *URL*.
* Devolviendo la respuesta de error para la solicitud de GET porque no se encontró ninguna sesión de reproducción. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET debido a un error interno del servidor.
* Devolviendo la respuesta de error para la solicitud de GET que especifica un recurso no válido: *ID de solicitud de publicidad*. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET que especifica un ID de grupo no válido o vacío: *id. de grupo*. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET que especifica un valor de posición de seguimiento no válido. (VOD)
* Devolviendo la respuesta de error para la solicitud de GET con sintaxis no válida: *URL de solicitud*. (Activo/VOD)
* Devolviendo respuesta de error para la solicitud con método HTTP no admitido: *GET|POST*. (Activo/VOD)
* Devolviendo el manifiesto desde la caché. (VOD)
* El servidor está sobrecargado. Continúe sin la solicitud de punteado de publicidad. (Variante)
* Inicio que genera el manifiesto objetivo. (HLSManifestResolver)
* Manifiesto de variante que genera inicios de: *dirección URL de contenido*. (Variante)
* Inicio de poner los anuncios en manifiesto. (VODHLSResolver)
* Intentando unir publicidad a `HH:MM:SS`: AdPlacement \[adManifestURL=*dirección URL del manifiesto de publicidad*, durationSeconds=*segundos*, ignore=*ignore*, redirectAd=*anuncio de redirección*, priority=*prioridad&lt;a 10/>.\]\*
* No se pueden obtener publicidades debido a una cronología de tiempo no válida; se devolvió el contenido sin publicidades. (VOD)
* No se pueden obtener publicidades: se devolvió el contenido sin publicidades. (VOD)
* No se pudo obtener la consulta de la publicidad y no se proporcionó ninguna dirección URL de contenido. (VOD)
* Se recibió una dirección URL válida. (VOD/Variant)
* No se encontró la variante M3U8. (Variante)

### Registros de TRACE_TRACKING_URL {#trace-tracking-url-records-1}

El servidor de manifiesto genera registros de este tipo después de llamar a una URL de seguimiento durante el flujo de trabajo de seguimiento del lado del servidor. Los campos más allá de TRACE_TRACKING_URL aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| pt | number | Tiempo de PTS dentro del flujo |
| ad_system | string | Sistema publicitario del anuncio (audiencia o rueda libre) |
| url | string | Ping de URL |
| state | string | Código de estado HTTP |

### TRACE_PLAYBACK_PROGRESS registra {#trace-playback-progress-records}

El servidor de manifiesto genera registros de este tipo cuando recibe una señal sobre el progreso de la reproducción durante el flujo de trabajo de seguimiento del lado del servidor. Los campos más allá de TRACE_PLAYBACK_PROGRESS aparecen en el orden mostrado en la tabla, separados por tabuladores.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | string | Código de estado HTTP |
| ancho de banda | integer | Ancho de banda del flujo |
| pt | integer | Tiempo de PTS dentro del flujo |
| ms_time | integer | Hora en que el servidor de manifiesto generó la dirección URL de seguimiento |
| url | string | Dirección URL de redireccionamiento |
| header_user_agent | string | Encabezado HTTP User-Agent |
| header_dnt | integer | Encabezado HTTP no rastrear |
| effective_remote_address | string | Dirección remota efectiva IPv4 |
| remote_address | string | Dirección remota IPv4 |

>[!NOTE]
>
>Los cuatro últimos campos son opcionales.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Información y soporte de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).