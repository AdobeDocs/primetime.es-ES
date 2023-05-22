---
title: Herramienta de depuración del servidor de manifiestos
description: Herramienta de depuración del servidor de manifiestos
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# Herramienta de depuración del servidor de manifiestos {#manifest-server-debugging-tool}

La herramienta de depuración permite a los editores investigar problemas de inserción de publicidad potencialmente costosos examinando la información de depuración devuelta en tiempo real por el servidor de manifiesto en encabezados HTTP o, cuando se necesita información más detallada, examinando los registros de sesión después del hecho. Los socios de Adobe como Akamai pueden utilizar la herramienta para depurar sus integraciones con Primetime y Decisioning.

La herramienta admite problemas de depuración e inserción en cualquiera de las configuraciones de servidor de manifiesto y seguimiento principales:

* Seguimiento del lado del cliente con un reproductor basado en TVSDK.
* Seguimiento del lado del cliente con un reproductor no basado en TVSDK.
* Seguimiento del lado del servidor.

Para admitir todos estos casos, la herramienta no requiere ni utiliza códigos de editor del reproductor.

Al iniciar una sesión de servidor de manifiesto, puede establecer un parámetro en la dirección URL de la solicitud para solicitarle que registre la información de depuración. Si utiliza valores diferentes de ese parámetro, también puede pedir al servidor de manifiesto que devuelva información de depuración especificada en encabezados HTTP, pero los encabezados sólo pueden contener una cantidad limitada de información. Puede obtener las credenciales de la Adobe para acceder a los archivos de registro completos, que el servidor de manifiesto guarda periódicamente (por ejemplo, cada hora) en un servidor de archivo. Una vez que tenga credenciales para ese servidor, puede acceder a él directamente en cualquier momento.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Opciones de herramienta de depuración {#debugging-tool-options}

Al invocar la herramienta de depuración, tiene varias opciones para la información que devuelve el servidor de manifiesto en los encabezados HTTP. Las opciones no afectan a lo que el servidor de manifiesto coloca en los archivos de registro.

### Especificar ptdebug {#specifying-ptdebug}

Al iniciar el registro de depuración para una sesión del servidor de manifiesto, puede agregar el parámetro ptdebug a la dirección URL de la solicitud para especificar las siguientes opciones para la información que devuelve el servidor de manifiesto en los encabezados HTTP:

* ptdebug=true Todos los registros excepto `TRACE_HTTP_HEADER` y la mayoría `call/response data` de `TRACE_AD_CALL` registros.
* ptdebug=Solo AdCall TRACE_AD_*type* (por ejemplo, TRACE_AD_CALL).
* ptdebug=Sólo encabezado Registros TRACE_HTTP_HEADER.

Las opciones no afectan a lo que el servidor de manifiesto coloca en los archivos de registro. No tiene control sobre eso, pero los archivos de registro son archivos de texto, por lo que puede aplicar una amplia variedad de herramientas para extraer y reformatear la información que le interese.

Este es un ejemplo del encabezado HTTP devuelto cuando `ptdebug=Header`. Algunas cadenas largas de dígitos hexadecimales se sustituyen por `. . .` para mayor claridad.

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

## Formatos de los registros de registro {#formats-of-log-records}

Cada registro tiene un tipo y un conjunto de campos, algunos de los cuales pueden ser opcionales. Los campos de todos los registros hasta el tipo de registro son los mismos. Proporcionan una marca de tiempo e información sobre la sesión. El tipo de registro identifica el tipo de evento que se registra y los campos siguientes proporcionan información sobre el evento registrado.

La estructura de un registro es la siguiente:

`datetime request_id session_id zone_id record_type` *otros campos.*

| Campo | Tipo | Descripción |
|--- |--- |--- |
| datetime | cadena | Marca de tiempo |
| request_id | cadena | ID de solicitud utilizado por el servidor de manifiesto (marca de tiempo Unix) |
| session_id | cadena | ID de sesión utilizado por el servidor de manifiesto |
| zone_id | entero | ID de zona |
| record_type | cadena | Tipo de evento que se registra |
| otros campos | *** | Depender del tipo de evento |

### Registros de TRACE_REQUEST_INFO {#trace-request-info-records}

Los registros de este tipo registran los resultados de las solicitudes HTTP. Los campos que se encuentran más allá de TRACE_REQUEST_INFO aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | cadena | Código de estado HTTP devuelto |
| request_method | cadena | Método HTTP (GET o POST) |
| request_uri | cadena | URI de solicitud HTTP (sin host) |
| request_length | entero | Longitud de la solicitud (bytes) |
| response_length | entero | Longitud de la respuesta (bytes) |
| delta | entero | Tiempo (milisegundos) para procesar la solicitud |
| module_type | cadena | Variante, Flujo o VOD |
| remote_address_aud_client_ip | cadena | (consulte la nota) |
| dirección_remota_x_fwd_for_hdr_key | cadena | (consulte la nota) |
| puerto_host_remoto | cadena | (consulte la nota) |

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

Los registros de este tipo registran los encabezados HTTP intercambiados durante las llamadas HTTP entre el servidor de manifiesto y el cliente, el servidor de publicidad o el servidor de contenido. Los campos que se encuentran más allá de TRACE_HTTP_HEADER aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| request_type | cadena | Tipo de solicitud (PRINCIPAL o DESCONOCIDA) |
| request_response | cadena | Encabezado de respuesta (solicitud o respuesta) |
| header_name | cadena | Nombre del encabezado HTTP |
| header_value | cadena | Valor de encabezado HTTP codificado en Base64 |

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

Los registros de este tipo registran los resultados de las solicitudes de anuncios del servidor de manifiesto. Los campos que se encuentran más allá de TRACE_AD_CALL aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | cadena | Código de estado HTTP devuelto |
| request_duration | entero | Tiempo (milisegundos) desde la solicitud hasta la respuesta |
| ad_server_query_url | cadena | URL para la llamada de anuncio, incluidos los parámetros de consulta |
| ad_system_id | cadena | Sistema de publicidad, desde la respuesta del servidor de publicidad (Audiencia si no se especifica) |
| avail_id | cadena | ID de la ventaja, de la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| avail_duration | número | Duración (segundos) de la disponibilidad, desde la señal de anuncio en el archivo de manifiesto de contenido (N/D para VOD) |
| ad_server_response | cadena | Respuesta codificada en Base64 del servidor de publicidad |

Un ejemplo:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### Registros TRACE_AD_INSERT, TRACE_AD_RESOLVE y TRACE_AD_REDIRECT {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

Los registros de este tipo registran los resultados de las solicitudes de publicidad indicadas por el tipo de registro. Los campos que se encuentran más allá del tipo de registro aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | cadena | Código de estado HTTP devuelto |
| avail_id | cadena | ID del dispositivo, de la señal de anuncio en el archivo de manifiesto de contenido (activo) o del servidor de manifiesto (VOD) |
| ad_type | cadena | Tipo de anuncio (DIRECTO o REDIRECCIONAL) |
| ad_duration | entero | Duración (segundos) de la respuesta del anuncio, del servidor de publicidad |
| ad_content_url | cadena | URL del archivo de manifiesto del anuncio, desde la respuesta del servidor de publicidad |
| ad_content_url_actual | cadena | URL del archivo de manifiesto del anuncio insertado. Vacío para TRACE_AD_REDIRECT. |
| ad_system_id | cadena | Sistema de publicidad, desde la respuesta del servidor de publicidad (Audiencia si no se especifica) |
| ad_id | cadena | ID del anuncio, de la respuesta del servidor de publicidad |
| creative_id | cadena | ID del creativo, desde el nodo de publicidad, desde la respuesta del servidor de publicidad |
| ad_call_id | cadena | No se usa. Reservado para uso futuro. |
| delta | entero | Tiempo (milisegundos) empleado por este evento |
| varios | cadena | Motivo por el que se omitió el anuncio |

>[!NOTE]
>
>Los campos ad_content_url_actual, ad_call_id y misc son opcionales.

Para TRACE_AD_RESOLVE y TRACE_AD_INSERT, la URL del campo ad_content_url_actual es para el anuncio transcodificado si hay uno disponible. De lo contrario, el campo está vacío para TRACE_AD_RESOLVE o es el mismo que ad_content_url para TRACE_AD_INSERT.

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

### Registros TRACE_TRACKING_URL {#trace-tracking-url-records}

Los registros de este tipo registran los resultados de las solicitudes de anuncios del servidor de manifiesto. Los campos que se encuentran más allá de TRACE_TRACKING_URL aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| pts | número | Marca de tiempo del programa. Tiempo en el vídeo para llamar a la dirección URL. |
| ad_system | cadena | Sistema de publicidad (audiencia o rueda libre) |
| url | cadena | URL ping |
| status | cadena | Estado HTTP devuelto por el ping |

Un ejemplo:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### Registros TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE {#trace-transcoding-no-media-to-transcode-records}

Los registros de este tipo registran la falta de creatividad publicitaria. El único campo más allá de TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE aparece en la tabla.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| ad_id | cadena | ID de anuncio completo `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` PROTOCOLO: AUDITUDE, VAST) |

### Registros TRACE_TRANSCODING_REQUESTED {#trace-transcoding-requested-records}

Los registros de este tipo registran los resultados de las solicitudes de transcodificación que el servidor de manifiesto envía a CRS. Los campos que se encuentran más allá de TRACE_TRANSCODING_REQUESTED aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| ad_id | cadena | ID de anuncio completo |
| ad_manifest_url | cadena | URL del archivo de manifiesto del anuncio, desde la respuesta del servidor de publicidad |
| creative_type | cadena | Tipo de medios |
| banderas | cadena | ID3 indica si la solicitud de transcodificación incluye una solicitud para agregar una etiqueta ID3 |
| target_duration | cadena | Duración de destino (segundos) del creativo transcodificado |

### Registros de TRACE_TRACKING_REQUEST {#trace-tracking-request-records}

Los registros de este tipo indican una solicitud para realizar el seguimiento del lado del servidor. Los campos que se encuentran más allá de TRACE_TRACKING_REQUEST aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| tracking_url_count | entero | Número de URL de seguimiento |
| start | float | Tiempo de inicio del fragmento PTS (segundos con precisión de milisegundos) |
| fin | float | Tiempo de finalización del fragmento PTS (segundos con precisión de milisegundos) |

### Registros de TRACE_TRACKING_REQUEST_URL {#trace-tracking-request-url-records}

Los registros de este tipo proporcionan una dirección URL de seguimiento para el seguimiento del lado del servidor. Los campos que se encuentran más allá de TRACE_TRACKING_REQUEST_URL aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| timestamp | float | Tiempo (segundos, con precisión 0,001) dentro de la sesión de reproducción para hacer ping a la URL de seguimiento |
| ad_system | cadena | Sistema de publicidad (por ejemplo, audiencia) |
| url | cadena | URL para ping |

### Registros de TRACE_WEBVTT_REQUEST {#trace-webvtt-request-records}

Registros de este tipo registran solicitudes que el servidor de manifiesto realiza para subtítulos WEBVTT. Los campos que se encuentran más allá de TRACE_WEBVTT_REQUEST aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | cadena | Código de estado HTTP devuelto |
| vtt_uri | cadena | URL para la solicitud |
| start | float | Tiempo de inicio dividido (segundos con precisión de milisegundos) |
| fin | float | Tiempo de fin de división (segundos con precisión de milisegundos) |

### Registros de TRACE_WEBVTT_RESPONSE {#trace-webvtt-response-records}

Registros ``of ``esta ``type ``registro ``responses ``el ``manifest ``server ``sends ``hasta ``clients ``in `` `answer` ``hasta ``requests `` `for` ``WEBVTT ``subtítulos. Los campos que se encuentran más allá de TRACE_WEBVTT_RESPONSE aparecen en el orden mostrado en la tabla, separados `by`pestañas.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | cadena | Código de estado HTTP devuelto |
| respuesta | cadena | Respuesta codificada en Base64 enviada al cliente |

### Registros de TRACE_WEBVTT_SOURCE {#trace-webvtt-source-records}

Los registros de este tipo registran las respuestas a las solicitudes que realiza el servidor de manifiesto para los subtítulos WEBVTT. Los campos que se encuentran más allá de TRACE_WEBVTT_SOURCE aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | cadena | Código de estado HTTP devuelto |
| origen | cadena | Contenido VTT original con codificación Base64 |


### Registros TRACE_MISC {#trace-misc-records}

Los registros de este tipo permiten que el servidor de manifiesto registre eventos e información que no se planea de otra manera cuando ingiere anuncios. El campo situado más allá de TRACE_MISC consiste en una cadena de mensaje. Los mensajes que pueden aparecer son los siguientes:

* Anuncio ignorado :AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*segundos*, omitir=*pasar por alto*, redirectAd=*redirectAd*, priority=*priority*
* La ubicación del anuncio devolvió un valor nulo.
* Anuncio vinculado correctamente.
* Error de llamada de anuncio: *mensaje de error*.
* Agregando el agente de usuario para recuperar el manifiesto sin procesar: *user-agent*.
* Agregando cookie para recuperar manifiesto sin procesar: [cookie]
* URL incorrecta *mensaje de error de URL solicitado*. (Error al analizar la URL de variante)
* URL llamada: URL *obtenido devolución: código de respuesta*. ( Dirección URL activa)
* URL llamada: URL *código de retorno: código de respuesta*. ( URL de VOD)
* Se ha encontrado un conflicto al resolver los anuncios: uno de los siguientes: inicio durante la emisión o final durante la emisión está dentro del anuncio previo a la emisión o del anuncio previo a la emisión contenido en el anuncio durante la emisión (VOD).
* Se ha detectado una excepción no controlada producida por el controlador para el URI: *URL de solicitud*.
* Finalizó la generación del manifiesto de variante. (Variante)
* Finalizó la generación del manifiesto de variante.
* Excepción al gestionar el redireccionamiento de VAST *URL de redireccionamiento *error: *mensaje de error*.
* Error al recuperar la lista de reproducción del anuncio para *URL de manifiesto de anuncio*.
* Error al generar manifiesto de destino. (HLSManifestResolver)
* Error al analizar la primera respuesta de llamada de anuncio: *mensaje de error*.
* Error al procesar la solicitud del GET POST para la ruta: *URL de solicitud*. (Activo/VOD)
* Error al procesar la solicitud de manifiesto activa: *URL de solicitud*. (Activo)
* Error al devolver un manifiesto de variante: *mensaje de error*.
* Error al validar el ID de grupo: *ID de grupo*.
* Obteniendo manifiesto sin procesar: *URL de contenido*. (Activo)
* Después del redireccionamiento VAST: *URL de redirección*.
* Se han encontrado disponibilidades vacías. (VOD)
* Se ha encontrado *número *anuncios. (VOD)
* Solicitud HTTP recibida. (Primer mensaje)
* Se ignora el anuncio porque la diferencia entre la duración de la respuesta del anuncio (*duración de la respuesta del anuncio *s) y la duración del anuncio real (*duración real *s) es mayor que el límite. (HLSManifestResolver)
* Se ignoran las variables que no proporcionaron ningún valor de ID. (GroupAdResolver.java)
* Se omitirá la variable que proporcionó un valor de tiempo no válido: *time *for availId = *ID de dispositivo*.
* Se omitirá la variable que proporcionó un valor de duración no válido: *duration *for availId = *ID de dispositivo*.
* Inicializar nueva sesión. (Variante)
* Método HTTP no válido. Debe ser un GET. (VOD)
* Método HTTP no válido. La solicitud de seguimiento debe ser una GET. (Activo)
* URL no válida *mensaje de error de URL solicitado*. (Variante)
* Grupo no válido. (HLSManifestResolver)
* Solicitud no válida. El pie de ilustración no es una solicitud de seguimiento válida. (VOD)
* Solicitud no válida. La solicitud de rótulo debe realizarse una vez establecida la sesión. (VOD)
* Solicitud no válida. La solicitud de seguimiento debe realizarse después de establecer la sesión. (VOD)
* Instancia de servidor no válida para el ID de grupo de sobrecarga: *ID de grupo*. (Activo)
* Se alcanzó el límite de redirecciones VAST - *número*.
* Realización de una llamada de anuncio: *URL de llamada de anuncio*.
* No se ha encontrado ningún manifiesto para: *URL de contenido*. (Activo)
* No se ha encontrado ninguna disponibilidad coincidente para el ID de disponibilidad: *ID de dispositivo*. (HLSManifestResolver)
* No se ha encontrado ninguna sesión de reproducción. (HLSManifestResolver)
* Procesando solicitud de manifiesto de VOD *URL de contenido*.
* Variante de procesamiento.
* Procesando solicitud de rótulo para manifiesto *URL de contenido*.
* Procesando solicitud de seguimiento. (VOD)
* Respuesta de anuncio de redirección vacía. ( VASTStAX)
* Solicitando: *URL*.
* Devolviendo respuesta de error para la solicitud de GET porque no se encontró ninguna sesión de reproducción. (VOD)
* Devolver la respuesta de error para la solicitud de GET debido a un error interno del servidor.
* Devolviendo respuesta de error para la solicitud de GET que especifica un recurso no válido: *ID de solicitud de anuncio*. (VOD)
* Devolver la respuesta de error para la solicitud de GET que especifica un ID de grupo no válido o vacío: *ID de grupo*. (VOD)
* Devolviendo respuesta de error para la solicitud de GET que especifica un valor de posición de seguimiento no válido. (VOD)
* Devolviendo respuesta de error para solicitud de GET con sintaxis no válida - *URL de solicitud*. (Activo/VOD)
* Devolviendo respuesta de error para la solicitud con método HTTP no compatible: *GET|POST*. (Activo/VOD)
* Devolviendo manifiesto de la caché. (VOD)
* Servidor sobrecargado. Continuar sin solicitud de vinculación de publicidad. (Variante)
* Inicie la generación del manifiesto de destino. (HLSManifestResolver)
* Comience a generar el manifiesto de variante desde: *URL de contenido*. (Variante)
* Empiece a vincular anuncios al manifiesto. (VODHLSResolver)
* Intentando unir el anuncio en `HH:MM:SS`: AdPlacement \[adManifestURL=*URL de manifiesto de anuncio*, durationSeconds=*segundos*, omitir=*pasar por alto*, redirectAd=*anuncio de redireccionamiento*, priority=*priority*.\]
* No se pueden obtener anuncios debido a un pttimeline no válido; se ha devuelto el contenido sin anuncios. (VOD)
* No se han podido obtener los anuncios - ha devuelto el contenido sin anuncios. (VOD)
* No se pudo obtener la consulta del anuncio y no se proporcionó ninguna dirección URL de contenido. (VOD)
* URL válida recibida. (VOD/Variante)
* No se ha encontrado la variante M3U8. (Variante)

### Registros TRACE_TRACKING_URL {#trace-tracking-url-records-1}

El servidor de manifiesto genera registros de este tipo después de llamar a una URL de seguimiento durante el flujo de trabajo de seguimiento del lado del servidor. Los campos que se encuentran más allá de TRACE_TRACKING_URL aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| pts | número | Tiempo de PTS dentro del flujo |
| ad_system | cadena | Sistema de publicidad de (audiencia o rueda libre) |
| url | cadena | URL ping |
| state | cadena | Código de estado HTTP |

### Registros TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

El servidor de manifiesto genera registros de este tipo cuando recibe una señal sobre el progreso de reproducción durante el flujo de trabajo de seguimiento del lado del servidor. Los campos que se encuentran más allá de TRACE_PLAYBACK_PROGRESS aparecen en el orden mostrado en la tabla, separados por tabulaciones.

| Campo | Tipo | Descripción |
|--- |--- |--- |
| status | cadena | Código de estado HTTP |
| ancho de banda | entero | Ancho de banda de la secuencia |
| pts | entero | Tiempo de PTS dentro del flujo |
| ms_time | entero | Hora a la que el servidor de manifiesto generó la URL de seguimiento |
| url | cadena | URL de redireccionamiento |
| header_user_agent | cadena | Encabezado de agente de usuario HTTP |
| header_dnt | entero | Encabezado HTTP do-not-track |
| Effective_remote_address | cadena | Dirección remota efectiva IPv4 |
| remote_address | cadena | Dirección remota IPv4 |

>[!NOTE]
>
>Los últimos cuatro campos son opcionales.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
