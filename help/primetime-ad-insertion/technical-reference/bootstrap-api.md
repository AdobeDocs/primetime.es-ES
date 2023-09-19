---
title: API de Bootstrap
description: API de Bootstrap
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# API de Bootstrap {#bootstrap-api}

La API de Bootstrap suele ser la dirección URL que se envía a las API de cliente/reproducción de vídeo.  Para ver las opciones y los parámetros que se pueden configurar, consulte la [Parámetros de API de Bootstrap](#bootstrap-api-parameters).

## Enviar un comando al servidor de manifiestos {#send-a-command-to-the-manifest-server}

1. Enviar un `HTTP GET` solicitud de una URL de bootstrap construida con el siguiente patrón:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **Extensión de archivo** Definido. `.m3u8` si el manifiesto de destino es HLS, `.mpd` si los manifiestos de destino están en el GUIÓN.

   * **PublisherAssetID** Requerido. ID único del publicador para el contenido específico.

   * **URL de contenido** Requerido. URL del archivo de contenido M3U8, codificado en Base64 para que sea seguro dentro de la URL del servidor de manifiesto. La dirección URL de contenido debe señalar a un archivo de variante M3U8, aunque solo haya una secuencia de velocidad de bits.

   * **Parámetros de consulta** Estos constituyen la parte más variada de la solicitud. Indican al servidor de manifiesto qué tipo de cliente realiza la solicitud y qué desea que haga el servidor de manifiesto.

   Por ejemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Solicitudes HTTP o HTTPS**

   El servidor de manifiestos crea direcciones URL utilizando el mismo protocolo HTTP de la solicitud del cliente. Si un reproductor realiza una solicitud HTTP (http) no segura, el servidor de manifiestos devuelve las direcciones URL de manifiesto y las direcciones URL de seguimiento del Auditude con el protocolo http. Si un reproductor realiza una conexión HTTP segura (https), un servidor de manifiesto, devuelve direcciones URL de manifiesto y direcciones URL de seguimiento del Auditude con el protocolo https.

   >[!NOTE]
   >
   >El servidor de manifiestos no puede cambiar el protocolo (HTTP o HTTPS) de las señalizaciones de seguimiento de terceros. Debe ponerse en contacto con los proveedores de contenido y de publicidad de terceros para que configuren los protocolos deseados.  Los protocolos de URL de los segmentos se pueden cambiar; sin embargo, de forma predeterminada, se utilizan los mismos protocolos definidos en los manifiestos de destino.

## Parámetros de API de Bootstrap {#bootstrap-api-parameters}

Los parámetros de consulta indican al servidor de manifiesto qué tipo de cliente envió la solicitud y qué desea que haga el servidor de manifiesto. Algunos son obligatorios y otros tienen formatos o valores aceptables específicos.
La dirección URL completa consiste en la dirección URL base seguida de un signo de interrogación. `parameterName=value` argumentos separados por un símbolo et. Por ejemplo, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

El servidor de manifiestos reconoce los siguientes parámetros. Toda la cadena de consulta\
Los parámetros de se pasan al servidor de publicidad.

| parámetro | description | formatos |
|---|---|---|
| _sid_ | ID único que el servidor de manifiesto utilizará para generar el ID de sesión. | Necesario para GUIÓN/HLS |
| live | Notifica al Ad Insertion de Primetime que el elemento de contenido transmitido es una emisión en directo.  Si no se pasa este parámetro, Primetime Ad insertion realizará una solicitud secundaria en la llamada de manifiesto inicial para determinar si el manifiesto está activo o es vod.<br>Valores posibles:<br>true para contenido en directo<br>false para el contenido de vod<br>omitir para la detección automática | Opcional para HLS.  Necesario para DASH |
| z | ID de zona del recurso que debe proporcionarse al Ad Insertion de Primetime. Proporcionado por el administrador técnico de cuentas de Adobe. | Necesario para GUIÓN/HLS |
| pabimodo | Habilita [inserción de pausa publicitaria parcial](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) para emisiones en directo.<br>Valores posibles:<br>true para habilitar<br>omitir para deshabilitar (predeterminado deshabilitado) | HLS/GUIÓN |
| ptadtimeout | Permite limitar el tiempo de resolución general del anuncio si los proveedores posteriores tardan demasiado en responder.  Las respuestas de larga duración pueden causar problemas con la reproducción, lo que permite a Primetime DAI forzar una respuesta en un límite de tiempo específico.<br>Valores posibles:<br>cadena numérica en milisegundos.<br>omitir para deshabilitar (predeterminado deshabilitado) | HLS/GUIÓN |
| ptadwindow | Duración (en segundos) de la ventana retrospectiva y de toma de decisiones: cuánto tiempo atrás buscará el Ad Insertion de Primetime las señales de anuncio cuando un usuario de DVR se una al flujo. Un valor de cero deshabilita la emisión de anuncio durante la emisión en el manifiesto inicial, y la toma de decisiones solo se reanuda después de la primera actualización. Este parámetro es útil para deshabilitar la inserción de anuncios en sesiones que solo pueden durar unos segundos (también conocido como volteo de canal).<br>Valores posibles:<br>cadena numérica 0-1800 (valor predeterminado 1800) | Solo HLS |
| ptassetid | ID único del contenido que el editor asigna y mantiene.  Necesario cuando se utiliza junto con el escalador de anuncios de Akamai. | HLS/GUIÓN |
| ptcdn | Lista de una o más CDN para alojar recursos transcodificados. Para obtener más información, consulte [Entrega y almacenamiento](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Valores posibles:<br>akamai, level3, lnw (red de foco), comcast.<br>De forma predeterminada, se utilizan las CDN del Ad Insertion de Primetime. | HLS/GUIÓN |
| ptcueformat | El formato de etiquetas especificado para realizar la toma de decisiones de anuncios (por ejemplo, scte35).<br>Valores posibles:<br>dpisimple, dpiscte35, elemental<br>Para obtener formatos de referencia personalizados, póngase en contacto con su representante de cuentas técnico para conocer el valor que utilizará en su caso de uso | HLS/GUIÓN |
| ptfailover | Indica al servidor de manifiesto que identifique los flujos de conmutación por error y principales especificados en la lista de reproducción principal y que los trate como conjuntos separados. Esto facilita la conmutación por error y evita errores de temporización. (Solo para dispositivos HLS de Apple). Para obtener más información, consulte [Facilitación del cambio de reproductor HLS](hls-switching-to-failover.md) | Solo HLS |
| ptmulticall | Si está habilitado, se realiza una solicitud de publicidad independiente para cada recurso que se encuentre en un recurso de VOD.  De forma predeterminada, el Ad Insertion de Primetime intentará recopilar toda la información disponible y enviarla al servidor de publicidad en una única solicitud. Valores posibles:true para habilitar, <br>omitir para deshabilitar (predeterminado deshabilitado) | HLS/GUIÓN |
| ptparallelstream | Permite a los clientes con reproductores que solicitan secuencias de audio o vídeo desmuxadas de CMAF en paralelo garantizar que los anuncios en las pistas de audio y vídeo sean coherentes. | Solo HLS |
| ptprotoswitch | Habilita las reglas de reescritura de manifiestos con nombre y las reglas de recuperación de anuncios, que suele configurar el representante de asistencia técnica.<br>Ejemplo: adfetch_fw, cdn_akm | HLS/GUIÓN |
| pttagds | Permite la inyección de etiquetas EXT-X-DISCONTINUITY-SEQUENCE en encabezados HLS.Valores posibles:true para habilitar, omita deshabilitar (valor predeterminado deshabilitado) | Solo HLS |
| pttimeline | Cadena que contiene la cronología deseada para la ubicación y el contenido del anuncio, que anula los saltos de anuncio en el flujo de contenido. [Consulte Formato de línea de tiempo de VOD] | HLS/GUIÓN |
| pttoken | Habilita los esquemas de protección de token de autorización de fragmentos/segmentos de contenido para CDN<br>Valores posibles:<br>akamai, lnw (limelight), ctl (centurylink) (la tokenización predeterminada está desactivada) | HLS/GUIÓN |
| pttrackingmode | Habilite los esquemas de seguimiento de anuncios.<br>Valores posibles:<br>sencillo para el seguimiento de anuncios del lado del cliente<br>sstm para el seguimiento de anuncios del lado del servidor<br>simplesstm para el seguimiento de anuncios de cliente/servidor híbrido (de forma predeterminada, no se realiza ningún seguimiento de anuncios) | HLS/GUIÓN |
| pttrackingposition | Indica al servidor de manifiesto que devuelva únicamente información de seguimiento de anuncios. No especifique este parámetro en la solicitud de arranque.<br>Nota: El servidor de manifiestos ignora todos los valores pasados. Sin embargo, si pasa una cadena nula o vacía, el servidor de manifiesto devuelve el M3U8 | HLS/GUIÓN<br>Seguimiento del lado del cliente |
| pttrackingversion | Establece la versión de formato que se va a devolver.<br>Valores posibles:<br>v1, v2, v3 o vmap | HLS/GUIÓN<br>Seguimiento del lado del cliente |
| scteTracking | Este parámetro indica al servidor de manifiesto que el reproductor que recupera el M3U8 necesita recuperar la información de etiqueta SCTE.<br>Valores posibles:<br>true o false (valor predeterminado false)<br>Nota: Los datos SCTE-35 se devuelven en el sidecar JSON con la siguiente combinación de valores de parámetros de consulta:<br>ptcueformat=turner | elemental | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | Solo HLS |
| vetargetmultiplicer | El número de segmentos desde el punto activo El desplazamiento previo a la emisión se configura con: ( vetargetmultiplicer * targetduration ) + vebufferlength<br>Nota: Este parámetro se aplica solo a flujos HLS activos/lineales<br>Valores posibles:<br>flotante numérico<br>(predeterminado: 3.0 - igual que la especificación de HLS) | Solo HLS |
| vebufferLength | El número de segundos desde el punto de activación, utilizado junto con vetargetmultiplicer.<br>Nota: Este parámetro se aplica solo a flujos HLS activos/lineales<br>Valores posibles:<br>flotante numérico<br>(predeterminado: 3.0) | Solo HLS |
