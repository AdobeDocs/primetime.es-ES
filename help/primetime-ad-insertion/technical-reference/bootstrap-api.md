---
title: API de Bootstrap
description: 'API de Bootstrap '
translation-type: tm+mt
source-git-commit: bf99c76bbbb67560adc675cf84297b8d3b04e19d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# API de Bootstrap {#bootstrap-api}

La API de Bootstrap suele ser la URL que se envía a las API de reproducción de cliente/vídeo.  Para ver las opciones y los parámetros que se pueden configurar, consulte los [parámetros de API de Bootstrap](#bootstrap-api-parameters).

## Enviar un comando al servidor de manifiesto {#send-a-command-to-the-manifest-server}

1. Envíe una solicitud `HTTP GET` para una URL de arranque construida con el siguiente patrón:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **Extensión** de archivoDefinido. `.m3u8` si el manifiesto de destinatario es HLS,  `.mpd` si los manifiestos de destinatario están en el DASH.

   * **** PublisherAssetIDRrequerido. ID única del editor para el contenido específico.

   * **Content** URLRequired. URL del archivo M3U8 de contenido, codificado en Base64 para ser seguro dentro de la URL del servidor de manifiesto. La dirección URL de contenido debe apuntar a un archivo M3U8 de variante, aunque solo haya un flujo de velocidad de bits.

   * **Parámetros de** consultaConstituyen la parte más variada de la solicitud. Indican al servidor de manifiesto qué tipo de cliente realiza la solicitud y qué desea que haga el servidor de manifiesto.

   Por ejemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Peticiones HTTP vs. HTTPS**

   El servidor de manifiesto crea direcciones URL utilizando el mismo protocolo HTTP de la solicitud del cliente. Si un reproductor realiza una solicitud HTTP (http) no segura, el servidor de manifiesto devuelve direcciones URL de manifiesto y URL de seguimiento de Auditude con el protocolo http. Si un reproductor realiza una conexión HTTP (https) segura, servidor de manifiesto, devuelve direcciones URL de manifiesto y direcciones URL de seguimiento de Auditude con el protocolo https.

   >[!NOTE]
   >
   >El servidor de manifiesto no puede cambiar el protocolo (HTTP o HTTPS) de las señalizaciones de seguimiento de terceros. Debe ponerse en contacto con el contenido y los proveedores de publicidad de terceros para que éstos configuren los protocolos deseados.  Los protocolos URL de los segmentos se pueden cambiar, pero de forma predeterminada, utilizan los mismos protocolos definidos en los manifiestos de destinatario.

## Parámetros de API de Bootstrap {#bootstrap-api-parameters}

Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen determinados formatos o valores aceptables.
La dirección URL completa consiste en la dirección URL base seguida de un signo de interrogación y, a continuación, `parameterName=value` argumentos separados por un signo de interrogación. Por ejemplo, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

El servidor de manifiesto reconoce los siguientes parámetros. Toda la cadena de consulta\
los parámetros se pasan al servidor de publicidad.

| parámetro | description | formatos |
|---|---|---|
| _sid_ | ID única que usará el servidor de manifiesto para generar la identificación de sesión. | Necesario para DASH/HLS |
| live | Notifica al Ad Insertion de Primetime que el elemento de contenido pasado es un flujo en directo.  Si no se pasa este parámetro, la inserción de publicidad Primetime realizará una solicitud secundaria en la llamada de manifiesto inicial para determinar si el manifiesto está activo o válido.<br>Valores posibles:<br>true para el <br>contenido activo false para el <br>contentomit de vod para la detección automática | Opcional para HLS.  Necesario para DASH |
| z | Id. de zona del recurso que debe proporcionarse a Primetime Ad Insertion. Proporcionado por el administrador de cuentas técnico de Adobe. | Necesario para DASH/HLS |
| pabimode | Habilita [inserción parcial de pausa publicitaria](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) para flujos en vivo.<br>Valores posibles:<br>true para <br>habilitar la deshabilitación (predeterminado desactivado) | HLS/DASH |
| ptadtimeout | Permite limitar el tiempo total de resolución de publicidad, si los proveedores intermedios tardan demasiado en responder.  Las respuestas de larga ejecución pueden causar problemas con la reproducción, lo que permite a Primetime DAI forzar una respuesta dentro de un límite de tiempo específico.<br>Valores posibles:cadena <br>numérica en milisegundos.<br>omitir para deshabilitar (deshabilitado de forma predeterminada) | HLS/DASH |
| ptadwindow | Duración (en segundos) de la ventana retrospectiva y de toma de decisiones: cuánto tiempo atrás el Ad Insertion de Primetime buscará señales publicitarias cuando un usuario de DVR se una al flujo. Un valor de cero deshabilitará la toma de decisiones de anuncio en el manifiesto inicial, y la decisión se reanudará solo después de la primera actualización. Este parámetro es útil para desactivar la inserción de anuncios en sesiones que solo pueden durar unos segundos (es decir, voltear canal).<br>Valores posibles:cadena <br>numérica 0-1800 (valor predeterminado 1800) | Sólo HLS |
| ptassetid | ID única del contenido que el editor asigna y mantiene.  Necesario cuando se utiliza junto con el escalador de anuncios de Akamai. | HLS/DASH |
| ptcdn | Lista de uno o más CDN para alojar recursos transcodificados. Para obtener más información, consulte [Envío y almacenamiento](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Valores posibles: <br>akamai, nivel3, lnw (redes limelight), comcast.<br>De forma predeterminada, se utilizan CDN de Ad Insertion Primetime. | HLS/DASH |
| ptcueformat | Formato especificado de las etiquetas para realizar la toma de decisiones de publicidad (por ejemplo, scte35).<br>Valores posibles:<br>dpisimple, dpiscte35, <br>elementalPara los formatos de referencia personalizados, póngase en contacto con el representante de cuentas técnico para conocer el valor que se usará en el caso de uso | HLS/DASH |
| ptfailover | Indica al servidor de manifiesto que identifica los flujos principales y de conmutación por error especificados en la lista de reproducción maestra y que los trata como conjuntos desunidos. Esto facilita la conmutación por error y evita errores de temporización. (Solo para dispositivos Apple HLS). Para obtener más información, consulte [Facilitación de la conmutación del reproductor HLS](hls-switching-to-failover.md) | Sólo HLS |
| ptmulticall | Si se habilita, se realiza una solicitud de publicidad independiente para cada valor encontrado en un recurso de VOD.  De forma predeterminada, el Ad Insertion de Primetime intentará recopilar toda la información disponible y enviarla al servidor de publicidad en una solicitud. Valores posibles:true para habilitar, <br>omit para deshabilitar (predeterminado deshabilitado) | HLS/DASH |
| ptparallelstream | Permite a los clientes con reproductores que solicitan flujos de audio o vídeo CMAF desactivados en paralelo para garantizar que los anuncios de las pistas de audio y vídeo sean coherentes. | Sólo HLS |
| ptprotoswitch | Habilita las reglas de reescritura de manifiesto con nombre y las reglas de recuperación de publicidad, que normalmente serán configuradas por el representante de asistencia técnica.<br>Ejemplo: adfetch_fw, cdn_akm | HLS/DASH |
| pttagds | Permite la inyección de etiquetas EXT-X-DISCONTINUITY-SEQUENCE en encabezados HLS.Valores posibles:true para habilitar la deshabilitación (deshabilitado de forma predeterminada) | Sólo HLS |
| ptlínea | Una cadena que contiene la línea de tiempo deseada para la ubicación y el contenido de la publicidad, que anula los saltos de publicidad en el flujo de contenido. [ Consulte Formato de línea de tiempo VOD  ] | HLS/DASH |
| pttoken | Habilita esquemas de protección de token de autorización de fragmento/segmento de contenido para CDN<br>Valores posibles:<br>akamai, light (limelight), ctl (centurylink) (la tokenización predeterminada está deshabilitada) | HLS/DASH |
| pttrackingmode | Habilite los esquemas de seguimiento de publicidad.<br>Valores posibles:<br>simple para el <br>seguimiento de anuncios del lado del cliente para el <br>seguimiento de anuncios del lado del servidor simple para el seguimiento de anuncios híbridos del cliente/servidor (de forma predeterminada, no se realiza ningún seguimiento de anuncios) | HLS/DASH |
| pttrackingposition | Indica al servidor de manifiesto que devuelva sólo la información de seguimiento de publicidad. No especifique este parámetro en la solicitud de arranque.<br>Nota: El servidor de manifiesto ignora todos los valores pasados. Sin embargo, si se pasa una cadena nula o vacía, el servidor de manifiesto devuelve el M3U8 | HLS/DASH<br>Seguimiento del cliente |
| pttrackingversion | Define la versión de formato que se va a devolver.<br>Valores posibles:<br>v1, v2, v3 o vmap | HLS/DASH<br>Seguimiento del cliente |
| scteTracking | Este parámetro indica al servidor de manifiesto que el reproductor que busca el M3U8 necesita recuperar la información de la etiqueta SCTE.<br>Valores posibles:<br>true o false (predeterminado false)<br>Nota: Los datos de SCTE-35 se devuelven en el sidecar JSON con la siguiente combinación de valores de parámetro de consulta:<br>ptcueformat=turner | elemental | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | Sólo HLS |
| vetargetmultiplier | Número de segmentos desde el punto activo El desplazamiento previo al lanzamiento se configura mediante: ( vetargetmultiplier * targetduration ) + vebufferlength<br>Nota: Este parámetro solo se aplica a los flujos HLS interactivos/lineales<br>Valores posibles:<br>float numérico<br>(predeterminado: 3.0: igual que la especificación HLS) | Sólo HLS |
| vebufferLength | Número de segundos desde el punto activo, utilizado junto con vetargetmultiplier.<br>Nota: Este parámetro se aplica a los flujos HLS interactivos/lineales <br>solamenteValores posibles:float<br> <br>numérico(predeterminado: 3.0) | Sólo HLS |
