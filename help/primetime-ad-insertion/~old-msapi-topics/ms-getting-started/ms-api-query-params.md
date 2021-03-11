---
title: Parámetros de consulta del servidor de manifiesto
description: Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen formatos o valores aceptables específicos.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# Parámetros de consulta del servidor de manifiesto {#ms-query-params}

Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen formatos o valores aceptables específicos.

La dirección URL completa consiste en la dirección URL base seguida de un signo de interrogación y, a continuación, `parameterName=value` argumentos, separados por el signo ampersands: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parámetros reconocidos {#section_072845B7FA94468C8068E9092983C9E6}

El servidor de manifiesto reconoce los siguientes parámetros. Los procesa o los pasa, junto con todos los parámetros no reconocidos, al servidor de publicidad.

| Clave | Descripción | Requerido | Valores válidos |
|---|---|---|---|
| `__sid__` | ID único que utiliza el servidor de manifiesto para generar el ID de sesión. | Sí | Alfanumérico |
| g | Tipo de dispositivo de cliente | Cuando las reglas de segmentación dependen del tipo de dispositivo | Consulte la lista en [Tipos de cliente](https://adobeprimetime.zendesk.com). Requiere acceso a Zendesk. |
| k | Palabras clave para la segmentación de anuncios personalizada | No | Cadena segura para URL con el formato `key1=value1;key2=value2;. . .` |
| u | ID del recurso de inserción de publicidad de Primetime. | Sí | Valor hash MD5 |
| z | ID de zona de inserción de Primetime para el recurso. | Sí | Número entero |
| enableC3 | El cliente está en una ventana C3. Si es true, reemplace solo las bibliotecas locales; de lo contrario, reemplace todas las opciones disponibles. | No | Booleano |
| live | Indica si el contenido es una emisión en directo o VOD (vídeo bajo demanda). | Escalador de anuncios de Akamai o cliente Safari para iOS. | Booleano |
| `pabimode` | [Habilite la compatibilidad con la ](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) inserción de pausa publicitaria parcial. <br> Habilitar si es true o start.<br> Deshabilite si es false. | No (el valor predeterminado está desactivado) | start, true o false |
| `ptadwindow` | Duración (segundos) de la ventana de vinculación de anuncios: cuánto tiempo atrás para buscar anuncios cuando un usuario de DVR se une al flujo. | No (predeterminado = 1800) | 0 a 1800 |
| `ptassetid` | ID única del contenido que el editor asigna y mantiene. | Escalador de anuncios de Akamai | Cadena segura de URL |
| `ptcdn` | Lista de una o más CDN para alojar recursos transcodificados. Consulte [Compatibilidad con varias CDN](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | No (predeterminado=Akamai) | Ejemplo: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | Nombre del formato de señal de anuncio personalizado presente en M3U8. | No | DPISimple, DPIScte35, Elemental, NBC, NFL o Turner |
| `ptfailover` | Indica al servidor de manifiesto que identifique las emisiones principales y de conmutación por error especificadas en la lista de reproducción maestra y que las trate como conjuntos de separación. Esto facilita el failover y evita errores de temporización. (solo para dispositivos Apple HLS). Consulte [Facilitación del cambio del reproductor HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | No | true |
| `ptmulticall` | Si se establece en true, se realizan varias llamadas de anuncio de Auditude para FER; uno para cada pausa publicitaria. Si no existe o se establece en false, se realiza una llamada de anuncio a la audiencia para FER. | No | Booleano <br> **Nota**: Los requisitos siguientes: <ul><li>`ptcueformat` debe establecerse en nbc</li><li>se ignora el parámetro ptlínea-tiempo.</li></ul> |
| `ptplayer` | Jugador que realiza la solicitud. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Generado automáticamente por inserción de anuncios y utilizado por Akamai. No agregue ni elimine. | Escalador de anuncios de Akamai |  |
| `pttagds` | Habilitar etiquetas [EXT-X- DISCONTINUITY- SECQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | No | true - manifest server incluye una etiqueta de secuencia antes del contenido en cada archivo m3u8 que envía; si el parámetro no está presente o no es verdadero, manifest server no incluye una etiqueta de secuencia. |
| `pttimeline` | Cadena que contiene la cronología deseada para la ubicación y el contenido de la publicidad, que anula los saltos de publicidad en el flujo de contenido. | No | [Cronología de VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Habilitar tokens de autorización de segmentos de TS.<br> **Nota**: Solo se admiten tokens de CDN de Akamai | Para tokens de autorización de segmentos TS | Booleano |
| `pttrackingmode` | Habilitar el seguimiento de anuncios; ya sea del lado del cliente personalizado (simple), del lado del servidor (sstm) o híbrido (simplesstm). | No | simple, stm o simple.<br> **Nota**: Si este parámetro no está incluido, el #EX-X-MARKER se inserta en el manifiesto. Consulte [Directiva EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Indica al servidor de manifiesto que devuelva solo la información de seguimiento de anuncios. No especifique este parámetro en la solicitud de arranque. | Seguimiento del lado del cliente | Nota alfanumérica:  El servidor de manifiesto ignora todos los valores pasados. Sin embargo, si pasa una cadena nula o vacía, el servidor de manifiesto devuelve el M3U8 en lugar de rastrear la información. |
| `pttrackingversion` | Versión de formato de la información de seguimiento del lado del cliente. | Seguimiento del lado del cliente | v1, v2, v3 o vmap |
| `scteTracking` | Buscar M3U8 antes de que la información de seguimiento SCTE se pueda recuperar en el sidecar JSON V2. <br>Este parámetro indica al servidor de manifiesto que el reproductor que recupera el M3U8 necesita que se recupere la información de la etiqueta SCTE. | No (predeterminado: false) | true o false. <br> **Nota**: Los datos de SCTE-35 se devuelven en el sidecar JSON con la siguiente combinación de valores de parámetros de consulta: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | El número de segmentos desde el punto activo El desplazamiento previo a la emisión se configura mediante: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**:  Solo en directo/lineal | No (predeterminado:  3.0) | Flotante |
| `vebufferLength` | El número de segundos desde el punto activo. **Nota**: Solo en directo/lineal. | No (predeterminado: 3.0) | Flotante |
