---
title: Parámetros de consulta del servidor de manifiesto
description: Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen formatos o valores aceptables específicos.
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# Parámetros de consulta del servidor de manifiesto {#ms-query-params}

Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen formatos o valores aceptables específicos.

La dirección URL completa consiste en la dirección URL base seguida de un signo de interrogación. `parameterName=value` argumentos, separados por el símbolo &quot;et&quot;: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parámetros reconocidos {#section_072845B7FA94468C8068E9092983C9E6}

El servidor de manifiestos reconoce los siguientes parámetros. Las procesa o las pasa, junto con todos los parámetros no reconocidos, al servidor de publicidad.

| Clave | Descripción | Requerido | Valores válidos |
|---|---|---|---|
| `__sid__` | ID único que utiliza el servidor de manifiesto para generar el ID de sesión. | Sí | Alfanumérico |
| g | Tipo de dispositivo del cliente | Cuando las reglas de segmentación dependen del tipo de dispositivo | Consulte la lista en [Tipos de cliente](https://adobeprimetime.zendesk.com). Requiere acceso a Zendesk. |
| k | Palabras clave para la segmentación de anuncios personalizada | No | Cadena segura para URL con formato `key1=value1;key2=value2;. . .` |
| u | ID de recurso de inserción y Primetime. | Sí | Valor hash MD5 |
| z | ID de zona de inserción y Primetime para el recurso. | Sí | Entero |
| enableC3 | El cliente está en una ventana C3. Si es true, reemplace solo las disponibilidades locales; de lo contrario, reemplace todas las disponibilidades. | No | Booleano |
| live | Indica si el contenido es un flujo en directo o VOD (vídeo bajo demanda). | Akamai Ad Scaler o cliente de iOS Safari. | Booleano |
| `pabimode` | [Habilitar la inserción parcial de un salto de publicidad](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) soporte. <br> Habilite si es true o start.<br> Deshabilite esta opción si es falsa. | No (el valor predeterminado está deshabilitado) | start, true o false |
| `ptadwindow` | Duración (segundos) de la ventana de vinculación de anuncios: cuánto se retrocede para buscar anuncios cuando un usuario de DVR se une al flujo. | No (valor predeterminado = 1800) | 0 a 1800 |
| `ptassetid` | ID único del contenido que el editor asigna y mantiene. | Escalador de anuncios de Akamai | Cadena segura para URL |
| `ptcdn` | Lista de una o más CDN para alojar recursos transcodificados. Consulte [Compatibilidad con varias CDN](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | No (predeterminado=Akamai) | Ejemplo: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | Nombre del formato personalizado de referencia de anuncio presente en el M3U8. | No | DPISimple, DPIScte35, Elemental, NBC, NFL o Turner |
| `ptfailover` | Indica al servidor de manifiesto que identifique los flujos de conmutación por error y principales especificados en la lista de reproducción principal y que los trate como conjuntos separados. Esto facilita la conmutación por error y evita errores de temporización. (solo para dispositivos HLS de Apple). Consulte  [Facilitación del cambio de reproductor HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | No | true |
| `ptmulticall` | Si se establece en true, se realizan varias llamadas de anuncio de Auditude para FER; una para cada pausa publicitaria. Si está ausente o se establece en falso, se realiza una llamada de anuncio a la audiencia de FER. | No | Booleano <br> **Nota**: los siguientes requisitos: <ul><li>`ptcueformat` el parámetro debe establecerse en nbc</li><li>se ignora el parámetro pttimeline.</li></ul> |
| `ptplayer` | Reproductor que realiza la solicitud. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Generado automáticamente por inserción de publicidad y utilizado por Akamai. No agregue ni elimine. | Escalador de anuncios de Akamai |  |
| `pttagds` | Activar [EXT-X- DISCONTINUIDAD- SECUENCIA](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) etiquetas | No | true: el servidor de manifiesto incluye una etiqueta de secuencia antes del contenido en cada archivo m3u8 que envía; si el parámetro no está presente o no es true, el servidor de manifiesto no incluye una etiqueta de secuencia. |
| `pttimeline` | Cadena que contiene la cronología deseada para la ubicación y el contenido del anuncio, que anula los saltos de anuncio en el flujo de contenido. | No | [Cronología de VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Habilite los tokens de autorización de segmentos TS.<br> **Nota**: solo se admiten tokens de CDN de Akamai | Para tokens de autorización de segmentos TS | Booleano |
| `pttrackingmode` | Habilite el seguimiento de anuncios; ya sea personalizado del lado del cliente (simple), del lado del servidor (sstm) o híbrido (simplesstm). | No | simple, sstm o simplesstm.<br> **Nota**: si no se incluye este parámetro, el #EX-X-MARKER se inserta en el manifiesto. Consulte [DIRECTIVA EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Indica al servidor de manifiesto que devuelva únicamente información de seguimiento de anuncios. No especifique este parámetro en la solicitud de arranque. | Seguimiento del lado del cliente | Nota alfanumérica: El servidor de manifiesto ignora todos los valores pasados. Sin embargo, si pasa una cadena nula o vacía, el servidor de manifiesto devuelve el M3U8 en lugar de la información de seguimiento. |
| `pttrackingversion` | La versión de formato de la información de seguimiento del lado del cliente. | Seguimiento del lado del cliente | v1, v2, v3 o vmap |
| `scteTracking` | Busque M3U8 antes de poder recuperar la información de seguimiento SCTE en el sidecar JSON V2. <br>Este parámetro indica al servidor de manifiesto que el reproductor que recupera el M3U8 necesita recuperar la información de etiqueta SCTE. | No (predeterminado: false) | true o false. <br> **Nota**: los datos SCTE-35 se devuelven en el sidecar JSON con la siguiente combinación de valores de parámetros de consulta: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | El número de segmentos desde el punto activo El desplazamiento previo a la emisión se configura con: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**: solo activo/lineal | No (predeterminado: 3.0) | Flotante |
| `vebufferLength` | El número de segundos desde el punto activo. **Nota**: solo activo/lineal. | No (predeterminado: 3.0) | Flotante |
