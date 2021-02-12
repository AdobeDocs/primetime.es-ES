---
title: Parámetros de consulta del servidor de manifiesto
description: Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen determinados formatos o valores aceptables.
seo-title: Parámetros de consulta del servidor de manifiesto
seo-description: Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen determinados formatos o valores aceptables.
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---


# Parámetros de consulta del servidor de manifiesto {#ms-query-params}

Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen determinados formatos o valores aceptables.

La dirección URL completa consta de la dirección URL base seguida de un signo de interrogación y, a continuación, `parameterName=value` argumentos, separados por ampersands: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parámetros reconocidos {#section_072845B7FA94468C8068E9092983C9E6}

El servidor de manifiesto reconoce los siguientes parámetros. Los procesa o los pasa, junto con todos los parámetros no reconocidos, al servidor de publicidad.

| Clave | Descripción | Requerido | Valores válidos |
|---|---|---|---|
| `__sid__` | ID única que utiliza el servidor de manifiesto para generar el ID de sesión. | Sí | Alfanumérico |
| g | Tipo de dispositivo cliente | Cuando las reglas de objetivo dependen del tipo de dispositivo | Consulte la lista en [Tipos de cliente](https://adobeprimetime.zendesk.com). Requiere acceso a Zendesk. |
| k | Palabras clave para la segmentación de publicidad personalizada | No | Cadena segura para URL en formato `key1=value1;key2=value2;. . .` |
| u | ID de recurso de inserción de anuncios en Primetime. | Sí | Valor de hash MD5 |
| z | Id. de zona de inserción de Primetime para el recurso. | Sí | Entero |
| enableC3 | El cliente está en una ventana C3. Si el valor es true, reemplace sólo los valores locales disponibles; de lo contrario, sustituya todos los elementos disponibles. | No | Booleano |
| live | Indica si el contenido es un flujo en directo o VOD (vídeo a petición). | Akamai Ad Scaler o iOS Safari. | Booleano |
| `pabimode` | [Habilite la compatibilidad con la ](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) inserción parcial de pausa publicitaria. <br> Active esta opción si es true o inicio.<br> Deshabilitar si es false. | No (el valor predeterminado está desactivado) | inicio, verdadero o falso |
| `ptadwindow` | Duración (segundos) de la ventana de vinculación de publicidad: cuánto tiempo atrás para buscar anuncios cuando un usuario de DVR se une al flujo. | No (predeterminado = 1800) | 0 a 1800 |
| `ptassetid` | ID única del contenido que el editor asigna y mantiene. | Akamai Ad Scaler | Cadena segura para URL |
| `ptcdn` | Lista de uno o más CDN para alojar recursos transcodificados. Consulte [Compatibilidad con múltiples CDN](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | No (predeterminado=Akamai) | Ejemplo: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | Nombre del formato de señal de anuncio personalizado presente en M3U8. | No | DPISimple, DPIScte35, Elemental,NBC, NFL o Turner |
| `ptfailover` | Indica al servidor de manifiesto que identifica los flujos principales y de conmutación por error especificados en la lista de reproducción maestra y que los trata como conjuntos desunidos. Esto facilita la conmutación por error y evita errores de temporización. (Solo para dispositivos Apple HLS). Consulte [Facilitación de la conmutación del reproductor HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | No | true |
| `ptmulticall` | Si se establece en true, se realizan varias llamadas de publicidad de Auditude para FER; uno para cada pausa publicitaria. Si no se encuentra o se establece en false, se realiza una llamada de publicidad a la audiencia para FER. | No | Booleano <br> **Nota**: Los siguientes requisitos: <ul><li>`ptcueformat` debe configurarse en nbc</li><li>se omite el parámetro pttimeline.</li></ul> |
| `ptplayer` | Jugador que realiza la solicitud. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Generado automáticamente por inserción de publicidad y utilizado por Akamai. No agregue ni elimine. | Akamai Ad Scaler |  |
| `pttagds` | Habilitar etiquetas [EXT-X- DISCONTINUITY- SECUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | No | true - manifest server incluye una etiqueta de secuencia antes del contenido en cada archivo m3u8 que envía; si el parámetro no está presente o no es true, manifest server no incluye una etiqueta de secuencia. |
| `pttimeline` | Una cadena que contiene la línea de tiempo deseada para la ubicación y el contenido de la publicidad, que anula los saltos de publicidad en el flujo de contenido. | No | [Línea de tiempo de VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Habilitar tokens de autorización de segmentos de TS.<br> **Nota**: Solo se admiten tokens CDN de Akamai | Para tokens de autorización de segmentos de TS | Booleano |
| `pttrackingmode` | Habilitar el seguimiento de publicidad; cliente personalizado (simple), servidor (sstm) o híbrido (simple). | No | simple, sstm o simple.<br> **Nota**: Si no se incluye este parámetro, se inserta el #EX-X-MARKER en el manifiesto. Consulte [Directiva EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Indica al servidor de manifiesto que devuelva sólo la información de seguimiento de publicidad. No especifique este parámetro en la solicitud de arranque. | Seguimiento del lado del cliente | Nota alfanumérica:  El servidor de manifiesto ignora todos los valores pasados. Sin embargo, si se pasa una cadena nula o vacía, el servidor de manifiesto devuelve el M3U8 en lugar de la información de seguimiento. |
| `pttrackingversion` | Versión de formato de la información de seguimiento del lado del cliente. | Seguimiento del lado del cliente | v1, v2, v3 o vmap |
| `scteTracking` | Busque M3U8 antes de que la información de seguimiento de SCTE se pueda recuperar en el sidecar JSON V2. <br>Este parámetro indica al servidor de manifiesto que el reproductor que busca el M3U8 necesita recuperar la información de la etiqueta SCTE. | No (predeterminado: false) | true o false. <br> **Nota**: Los datos de SCTE-35 se devuelven en el sidecar JSON con la siguiente combinación de valores de parámetro de consulta: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | Número de segmentos desde el punto activo El desplazamiento previo al lanzamiento se configura mediante: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**:  Solo en directo/lineal | No (predeterminado:  3.0) | Flotante |
| `vebufferLength` | El número de segundos desde el punto activo. **Nota**: Solo en directo/lineal. | No (predeterminado: 3.0) | Flotante |