---
title: Notas de la versión de TVSDK 2.7 para Android™
description: Las notas de la versión de TVSDK 2.7 para Android™ describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de los dispositivos en TVSDK Android™ 2.7
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: d64f0ef2-60a9-43a1-b2f9-44764a570538
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '4037'
ht-degree: 0%

---

# Notas de la versión de TVSDK 2.7 para Android™ {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 2.7 para Android™ describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de los dispositivos en TVSDK Android™ 2.7

## TVSDK Android™ 2.7 {#tvsdk-android}

El reproductor de referencia Android™ se incluye con Android™ TVSDK en el directorio samples/ de su distribución. El archivo README&lt;.md que lo acompaña explica cómo crear el reproductor de referencia.

>[!NOTE]
>
>Para crear correctamente el reproductor de referencia, tal como se describe en README.md distribuido con la versión, asegúrese de hacer lo siguiente:
>
>1. Descargar VideoHeartbeat.jar desde [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (VideoHeartbeat Library para Android™ v2.0.0)
>1. Extraiga VideoHeartbeat.jar en la carpeta libs/ .

>


## Nuevas funciones {#new-features}

TVSDK 2.7 para Android™ incluye todas las funciones de la versión 1.4, excepto las que no se admiten en la lista [Matriz de funciones](#feature-matrix).

**Android™ TVSDK 2.7**

* **Compatibilidad con la resolución de anuncios en paralelo**

TVSDK 2.7 admite la resolución simultánea de todas las solicitudes de publicidad en una pausa publicitaria, en lugar de la resolución secuencial.

### Nuevas funciones de las versiones anteriores {#new-features-previous-releases}

**Versión 2.5.6**

* **TVSDK 2.5 es compatible con Android™ P**
* **Habilitación del audio de fondo**

   Para activar la reproducción de audio cuando la aplicación pasa del primer plano al segundo plano, la aplicación debe llamar a la API enableAudioPlaybackInBackground de MediaPlayer con true como argumento cuando el reproductor está en estado PREPARADO.

* **alwaysUseAudioOutputLatency(boolean val) en la clase MediaPlayer**

Cuando esté configurado, utilice la latencia de salida en el cálculo de la marca de tiempo del audio.
Parámetros booleanos val - True utiliza la latencia de salida de audio en el cálculo de la marca de tiempo del audio.

* **Optimizado para obtener la mejor experiencia de reproducción incluso si la velocidad de ancho de banda se reduce repentinamente.**
TVSDK ahora cancela la descarga del segmento en curso, si es necesario, y cambia dinámicamente a la representación adecuada. Esto se hace cambiando sin problemas entre las velocidades de bits sin interrupciones.

**Versión 2.5.5**

* **Inserción parcial de Ad-Break**

   Experiencia parecida a la televisión de unirse en medio de un anuncio sin activar el seguimiento del anuncio parcialmente visto.\
   Ejemplo: El usuario se une en el medio (a los 40 segundos) de una pausa publicitaria de 90 segundos que consta de tres anuncios de 30 segundos. Pasarán 10 segundos desde el segundo anuncio de la pausa.
   * El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.
   * Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Se activan los rastreadores solo del tercer anuncio.

* **Carga de publicidad segura a través de HTTPS**

   Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad primetime y CRS sobre https.

* **AdSystem e Creative Id añadidos a solicitudes CRS**

   * Ahora se incluye `AdSystem` y `CreativeId` como nuevos parámetros en las solicitudes 1401 y 1403.

* **API setEncodeUrlForTracking en la clase NetworkConfiguration eliminada** ya que los caracteres no seguros de una URL deben codificarse.

**Versión 2.5.4**

Android™ TVSDK v2.5.4 ofrece las siguientes actualizaciones y cambios en la API:

* Cambios en el valor predeterminado de `WebViewDebbuging`

   La variable `WebViewDebbuging` el valor se establece en _False_ de forma predeterminada. Para habilitarlo, llame a `setWebContentsDebuggingEnabled` a _True_ en la aplicación.

* Actualización de la versión de OpenSSL y Curl `libcurl` a v7.57.0 y OpenSSL a v1.0.2k.
* Acceso a nivel de aplicación para el objeto de respuesta VAST Se ha introducido una nueva API NetworkAdInfo::getVastXml() que proporciona acceso al objeto de respuesta VAST a la aplicación.

**Versión 2.5.3**

Android™ TVSDK v2.5.3 ofrece las siguientes actualizaciones y cambios en la API.

* Se recomienda a todos los clientes de TVSDK que utilicen CRS que actualicen sus aplicaciones con TVSDK 2.5.3.85 o la última versión en Android™. Este es un reemplazo de la implementación de aplicación existente. Después de la actualización de TVSDK, compruebe las solicitudes de URL creativas de CRS en una herramienta proxy (por ejemplo: Charles) y confirme que el nombre de host y la versión de la ruta de acceso se reflejan como en la estructura de URL de ejemplo a continuación.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente de usuario de TVSDK personalizable: hemos añadido algunas API nuevas para personalizar los agentes de usuario.

   * `setCustomUserAgent`(Valor de cadena)
   * `getCustomUserAgent`()

* Comparta cookies entre la aplicación Android™ y TVSDK: Ahora, Android™ TVSDK admite el acceso a cookies entre la capa Java™ (almacenada en CookieStore de la aplicación Android™) y la capa C++ TVSDK. Ahora, es posible configurar y/o modificar las cookies en la capa nativa C++ a medida que se exponen al almacén de cookies de Java™.
* Cambios en la API:

   * Se agrega un nuevo Event CookiesUpdatedEvent . El reproductor de medios lo envía cuando se actualiza su cookie.
   * Se agrega una nueva API a `NetworkConfiguration::set/ getCustomUserAgent()` para usar un agente de usuario personalizado.
   * Se agrega una nueva API a `NetworkConfiguration::set/ getEncodedUrlForTracking` para forzar la codificación de caracteres no seguros.
   * Se agrega una nueva API a `NetworkConfiguration::getNetworkDownVerificationUrl()` para establecer una URL de verificación de red si hay una conmutación por error.
   * Se agrega una nueva propiedad a TextFormat::trateSpaceAsAlphaNum, que define si se tratará el espacio como alfanumérico mientras se muestran los rótulos.

* Cambios en `SizeAvailableEvent`: Anteriormente, los métodos getHeight() y getWidth() de `SizeAvailableEvent` en la versión 2.5.2 se utilizaba para devolver la altura y la anchura del marco del fotograma, que se devolvía en el formato de medios. Ahora devuelve la altura de salida y el ancho de salida respectivamente devueltos por el decodificador.
* Cambios en el comportamiento del almacenamiento en búfer: Se cambia el comportamiento del almacenamiento en búfer. Depende del desarrollador de la aplicación lo que desea hacer si hay búfer vacío. 2.5.3 utiliza el tamaño del búfer de reproducción en una situación vacía de búfer.

**Versión 2.5.2**

Android™ TVSDK v2.5.2 ofrece importantes correcciones de errores y algunos cambios en la API.

**Versión 2.5.1**

Las nuevas funciones importantes lanzadas en Android™ 2.5.1.

* **Mejoras en el rendimiento** La nueva arquitectura TVSDK 2.5.1 aporta varias mejoras de rendimiento. Basándose en las estadísticas de un estudio de evaluación comparativa de terceros, la nueva arquitectura ofrece una reducción de 5 veces en el tiempo de inicio y de 3,8 veces menos en los fotogramas perdidos en comparación con el promedio del sector:

   * **Instantáneo para VOD y live -** Cuando activa instantáneamente, el TVSDK inicializa y almacena en el búfer los medios antes de que se inicie la reproducción. Como puede iniciar varias instancias de MediaPlayerItemLoader simultáneamente en segundo plano, puede almacenar en búfer varias secuencias. Cuando un usuario cambia el canal y el flujo se almacena en el búfer correctamente, la reproducción en el nuevo canal se inicia inmediatamente. TVSDK 2.5.1 también es compatible con Instant On para **live** también. Los flujos en directo se vuelven a almacenar en búfer cuando se mueve la ventana en directo.

      * **Lógica ABR mejorada -** La nueva lógica ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que el ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúe y también optimiza el número de veces que el interruptor de velocidad de bits se produce controlando la velocidad a la que cambia la longitud del búfer.
      * **Descarga parcial de segmentos / Subsegmentación -** TVSDK reduce aún más el tamaño de cada fragmento para iniciar la reproducción lo antes posible. El fragmento ts debe tener un fotograma clave cada dos segundos.
      * **Resolución de anuncios diferida -** TVSDK no espera a la resolución de los anuncios no previos al inicio de la reproducción, lo que reduce el tiempo de inicio. Las API como la búsqueda y el truco siguen sin estar permitidas hasta que se resuelvan todos los anuncios. Esto es aplicable a los flujos de VOD utilizados con CSAI. Las operaciones como la búsqueda y el avance rápido no están permitidas hasta que se complete la resolución del anuncio. Para las transmisiones en directo, esta función no se puede habilitar para la resolución de anuncios durante un evento en directo.
      * **Conexiones de red persistentes -** Esta función permite a TVSDK crear y almacenar una lista interna de conexiones de red persistentes. Estas conexiones se reutilizan para varias solicitudes, en lugar de abrir una nueva conexión para cada solicitud de red y luego destruirla posteriormente. Esto aumenta la eficacia y disminuye la latencia del código de red, lo que da como resultado un rendimiento de reproducción más rápido.
Cuando TVSDK abre una conexión, solicita al servidor una *keep-live* conexión. Es posible que algunos servidores no admitan este tipo de conexión, en cuyo caso TVSDK vuelve a establecer una conexión para cada solicitud de nuevo. Además, aunque las conexiones persistentes están activadas de forma predeterminada, TVSDK ahora tiene una opción de configuración para que las aplicaciones puedan desactivar las conexiones persistentes si lo desean.
      * **Descarga paralela:** La descarga de vídeo y audio en paralelo en lugar de en serie reduce los retrasos de inicio. Esta función permite reproducir archivos HLS Live y VOD, optimiza el uso de ancho de banda disponible desde un servidor, reduce la probabilidad de entrar en situaciones de búfer en ejecución y minimiza el retraso entre descarga y reproducción.
      * **Descargas de anuncios en paralelo -** TVSDK recupera previamente los anuncios en paralelo a la reproducción del contenido antes de llegar a las pausas publicitarias, lo que permite una reproducción perfecta de los anuncios y el contenido.

* **Reproducción**

   * **Reproducción de contenido de MP4:** Los clips cortos MP4 no necesitan ser retranscodificados para reproducirse dentro de TVSDK.
Nota: La conmutación ABR, la reproducción de trucos, la inserción de anuncios, el enlace de audio tardío y la subsegmentación no son compatibles con la reproducción de MP4.
   * **Reproducción trucada con velocidad de bits adaptable (ABR) -** Esta función permite que TVSDK cambie entre flujos de iFrame mientras se encuentra en modo de reproducción asistida. Puede utilizar perfiles que no sean iFrame para hacer la reproducción mediante trucos a velocidades más bajas.
   * **Suavizar juego de trucos -** Estas mejoras mejoran la experiencia del usuario:

          * Selección de velocidad de bits adaptable y velocidad de fotogramas durante la reproducción de trucos, según el perfil de búfer y ancho de banda
          * Uso del flujo principal en lugar del flujo IDR para obtener una reproducción rápida de hasta 30 fps.
      
* **Protección de contenido**

   * **Protección de salida basada en resolución -** Esta función vincula las restricciones de reproducción con resoluciones específicas, proporcionando controles DRM más precisos.

* **Compatibilidad con flujos de trabajo**

   * **Integración de facturación directa -** Esto envía métricas de facturación al back-end de Adobe Analytics, que Adobe Primetime certifica para las emisiones que utiliza el cliente.
TVSDK recopila automáticamente métricas, de acuerdo con el contrato de ventas del cliente, para generar los informes de uso periódicos necesarios a efectos de facturación. En cada evento de inicio de flujo, TVSDK utiliza la API de inserción de datos de Adobe Analytics para enviar métricas de facturación como el tipo de contenido, los indicadores habilitados para la inserción de anuncios y los indicadores habilitados para drm (según la duración del flujo facturable) al grupo de informes propiedad de Adobe Analytics Primetime. Esto no interfiere con los grupos de informes de Adobe Analytics ni las llamadas al servidor del cliente, ni se incluye en ellos. Si se solicita, este informe de uso de facturación se envía a los clientes periódicamente. Esta es la primera fase de la función de facturación que solo admite la facturación de uso. Se puede configurar en función del contrato de ventas mediante las API descritas en la documentación. Esta función está habilitada de forma predeterminada. Para desactivar esta función, consulte el ejemplo del reproductor de referencia.
   * **Soporte de conmutación por error mejorado -** Se han implementado estrategias adicionales para continuar con la reproducción ininterrumpida, a pesar de los errores de los servidores host, los archivos de listas de reproducción y los segmentos.

* **Publicidad**

   * **Integración de Moat -** Compatibilidad con la medición de la capacidad de visualización de anuncios de Moat.
   * **Banners complementarios -** Los banners adjuntos se muestran junto a un anuncio lineal y, a menudo, se siguen mostrando en la vista una vez finalizado el anuncio. Estos banners pueden ser de tipo html (un fragmento de HTML) o iframe de tipo (una dirección URL a una página de iframe).

* **Analytics**

   * **VHL 2.0 -** Esta es la última integración optimizada de Video Heartbeats Library (VHL) para la recopilación automática de datos de uso para Adobe Analytics. La complejidad de las API se ha reducido a para facilitar la implementación. Descargar la biblioteca VHL [v2.0.0 para Android™](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) y extraiga el archivo JAR en la carpeta libs.

* **SizeAvaliableEventListener**
   * Los métodos getHeight() y getWidth() de SizeAvailableEvent ahora devolverán la salida en altura y anchura respectivamente. La relación de aspecto de la visualización se puede calcular de la siguiente manera:

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookies**

   * Android™ TVSDK ahora es compatible con el acceso a las cookies Java™ almacenadas en CookieStore de la aplicación Android™. Se proporciona una API de devolución de llamada (onCookiesUpdated) para que se registre cada vez que una nueva cookie aparece como parte del encabezado de respuesta &quot;Set-Cookie&quot;. Estas cookies están disponibles como una lista de HttpCookie(s) que se utiliza para un URI o dominio diferente al establecer estos valores de cookies en ese URI o dominio particular mediante CookieStore. Del mismo modo, los valores de cookies en TVSDK se actualizan mediante la API de adición de CookieStore.

## Matriz de funciones {#feature-matrix}

TVSDK para Android™ es compatible con varias funciones que puede implementar para agregar funcionalidad a sus aplicaciones de vídeo.

En las tablas de características siguientes, una &quot;Y&quot; indica que la función es compatible con la versión actual.

| Función | Tipo de contenido | HLS |
|---|---|---|
| Reproducción general (Reproducir, Pausar, Buscar) | VOD + Activo | Y |
| FER: Reproducción general (reproducción, pausa, llamada a otro punto del contenido) | FER VOD | Y |
| Buscar cuando se está reproduciendo un anuncio | VOD + Activo | No admitido |
| AC3 | VOD + Activo | No admitido |
| MP3 | VOD | No admitido |
| Reproducción de contenido de MP4 | VOD | Y |
| Lógica de cambio de velocidad de bits adaptable | VOD + Activo | Y |
| Reproducción solo de audio | VOD + Activo | Y |
| Compatibilidad con varias CDN | VOD + Activo | No admitido |
| Reproducción de anuncios con medios solo de audio | VOD + Activo | No admitido |
| Subtítulos - 608/708 | VOD + Activo | Y |
| Subtítulos - WebVTT | VOD + Activo | Y |
| Error de manifiesto | VOD + Activo | Y |
| Failover avanzado | VOD + Activo | Y |
| Notificaciones de QoS y del reproductor | VOD + Activo | Y |
| Compatibilidad con encabezados de cookie | VOD + Activo | Y |
| Compatibilidad con encabezados HTTP personalizados | VOD + Activo | Y (se requiere inclusión en la lista de permitidos) |
| Establecer parámetros de control de búfer | VOD + Activo | Y |
| Establecer controles de velocidad de bits adaptables | VOD + Activo | Y |
| Etiquetas de manifiesto personalizadas | VOD + Activo | Y |
| Enlace de audio tardío | VOD + Activo | Y |
| 302 Redireccionamiento | VOD + Activo | Y |
| Reproducción con desplazamiento | VOD + Activo | Y |
| Reproducción solo de audio | VOD + Activo | Y |
| Reproducción complicada | VOD + Activo | Y |
| Movimiento lento en reproducción de truco | VOD + Activo | No admitido |
| Reproducción suave (con ABR) | VOD + Activo | Y |
| Análisis de ID3 | VOD + Activo | Y |
| Bloqueo de anuncios | VOD + Activo | No admitido |
| Instantáneo activado | VOD + Activo | No admitido |
| Compatibilidad con el marcador de discontinuidad | VOD + Activo | Y |
| 302 Adhesividad de redireccionamiento | VOD + Activo | Y |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Reproducción general, anuncios habilitados | VOD + Activo | Y |
| Contenido FER con anuncios habilitados | VOD | Y |
| Comportamientos de publicidad predeterminados | VOD + Activo | Y |
| VAST 2.0/3.0 | VOD + Activo | Y |
| VMAP 1.0 | VOD + Activo | Y |
| Anuncios de MP4 | VOD + Activo | Y (de CRS) |
| Reproducción trucada con anuncios habilitados | VOD + Activo | Y |
| Solo publicidad | VOD | Y |
| Parámetros de objetivo | VOD + Activo | Y |
| Parámetros personalizados | VOD + Activo | Y |
| Comportamientos de publicidad personalizados | VOD + Activo | Y |
| Etiquetas de publicidad personalizadas | Activo | Y |
| Resolvidores de publicidad personalizados | VOD + Activo | Y |
| Resolver publicidad personalizada a Freewheel | VOD | Y |
| C3 | VOD + Activo | No admitido |
| Resolución de publicidad diferida | VOD | Y |
| Compatibilidad con marcadores de discontinuidad - SSAI | VOD + Activo | Y |
| Anuncios Companion, Anuncios tipo titular y Anuncios en los que se puede hacer clic | VOD + Activo | Y |
| VPAID 2.0 | VOD + Activo | Y (JS) |
| Salida de publicidad anticipada | Activo | Y |
| Prioridad creativa basada en reglas | VOD + Activo | Y |
| Reglas CRS | VOD + Activo | Y |
| Resolución de anuncios JSON | VOD + Activo | No admitido |
| Integración de Moat | VOD + Activo | Y |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Cifrado AES | VOD + Activo | Y |
| Ejemplo de cifrado AES | VOD + Activo | Y |
| Emisiones con token | VOD + Activo | Y |
| DRM | VOD + Activo | Solo DRM de Primetime (futuro: Widevine) |
| Reproducción externa (RBOP) | VOD + Activo | Solo DRM de Primetime |
| Rotación de licencia | VOD + Activo | Solo DRM de Primetime |
| Rotación clave | VOD + Activo | Solo DRM de Primetime |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Integración de VHL de Adobe Analytics | VOD + Activo | Y |
| Facturación | VOD + Activo | Y |

## Problemas resueltos {#resolved-issues}

Cuando la resolución está asociada a un problema registrado, se muestra una referencia de Zendesk, por ejemplo ZD#xxxx

**Android™ TVSDK 2.7**

En esta sección se ofrece un resumen del problema resuelto en la versión de TVSDK 2.7.

* ZD#37166 - La llamada de seguimiento de errores se activa incluso cuando el anuncio se reproduce correctamente.
* ZD#37134 : se devuelven ID de anuncio incorrectos, en caso de que el anuncio esté presente con varios anuncios en la respuesta VMAP.

**Android™ TVSDK 2.5.6**

* ZD #34992 - El idioma está vacío en los subtítulos.
   * Se ha corregido un caso en el que TVSDK no analizaba #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS desde el manifiesto principal para obtener los detalles del seguimiento de rótulos.
* ZD #35078 - Validación de Android P.
   * TVSDK 2.5.6 se ha validado con las últimas versiones beta de Android™ P. No se encontraron problemas debido al nuevo sistema operativo Android™.
* ZD #34149 : El reproductor sigue solicitando manifiestos aunque se encuentren errores.
   * Se ha corregido el caso en el que TVSDK realizaba llamadas repetitivas incluso cuando todos los perfiles estaban inactivos (error 404).
* ZD #31533 - Reproducir audio en Android™ después de que la aplicación se haya enviado al fondo.
   * Se ha añadido `enableAudioPlaybackInBackground` API de MediaPlayer a la que se debe llamar con &quot;True&quot; como argumento (cuando el reproductor está en estado PREPARADO) para habilitar la reproducción de audio cuando la aplicación está en segundo plano.

**Android™ TVSDK 2.5.5**

* ZD #21647 : Android TVSDK notifica 640x368 cuando el tamaño real del vídeo es 640x360.
   * Debido a que la variable m_nOutputHeight (dentro de AndroidMCVideoDecoder) se actualiza con la altura del marco en lugar de con la altura de salida real. Se han realizado cambios importantes en la función getVideoFrame para calcular m_nOutputHeight correctamente.
* ZD #26614 - Urgente — servicio de publicidad de terceros/programático — fracaso en servir impresiones.
   * Se ha mejorado la corrección anterior al gestionar el caso en el análisis de XML donde el problema se podía reproducir cuando &quot;espacio&quot; estaba antes del signo &quot;igual&quot; como &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android: Agregue AdSystem y el ID creativo a las solicitudes CRS.
   * Ahora se incluyen &quot;AdSystem&quot; y &quot;CreativeId&quot; como nuevos parámetros en las solicitudes 1401 y 1403.
* ZD #33062 - TVSDK se bloquea al producirse caracteres de barra vertical en la respuesta VAST en el nodo CDATA
   * La API setEncodeUrlForTracking en la clase NetworkConfiguration se ha eliminado como caracteres no seguros en una URL que se va a codificar.
* ZD #33063 - Se rompió la lógica de selección de archivos CRS - TVSDK no enviaba la solicitud CRS para el formato web sino que la enviaba para archivos 3gpp en su lugar.
   * Se ha corregido la lógica ahora. Al utilizar archivos multimedia con formato webm y 3gpp, la solicitud CRS se envía para webm. Y al usar ambos archivos multimedia con formato 3gpp, la solicitud CRS para ser enviada para el archivo 3gpp de velocidad de bits más alta.
* ZD #33125 - La aplicación de Android se bloquea con una etiqueta DoubleClick específica dentro del VMAP.
   * Se ha corregido el escenario para evitar el bloqueo.
* ZD #32256 - Problema de rotación de licencias y rotaciones clave - Acceso al Adobe.
   * Se ha corregido la inicialización de segmentos con los metadatos DRM para el contenido de SampleAES. Funciona bien con contenido de AES128.
* ZD #33619 - Reenvío rápido de un creciente contenido de la lista de reproducción atascado en estado de almacenamiento en búfer cerca del punto de lanzamiento.
   * Se ha gestionado el caso al cruzar el punto activo en el modo de reproducción de trucos.
* ZD #34151 - Objetos TimedMetadata desordenados.
   * Dos eventos TimedMetadata aparecían en orden aleatorio si pertenecían a la misma hora en la cronología. Mantuvieron su orden original en manifiesto.
* ZD #34189 - Problema al intentar el comienzo de la pausa publicitaria.
   * El problema era con los anuncios de SSAI que se vinculan mediante discontinuidad. Y la causa fue un comportamiento cuando buscamos el principio de esos anuncios, buscamos un fotograma clave y no lo encontramos. La razón era que la marca de tiempo de audio mínima del anuncio era anterior a la marca de tiempo mínima del vídeo. Por lo tanto, terminamos buscando un fotograma clave en los datos de fragmentDump incorrectos. Corregido ahora.
* ZD #34528 - La resolución de vídeo no se actualiza más allá de las 640x360 en la llave de tercera generación de FireTV.
   * Se ha mejorado la corrección para incluir las últimas actualizaciones de firmware.
* ZD #34793 - TVSDK 2.5.x solía bloquearse con la resolución de contenido personalizado a veces cuando VideoEngine supuso que auditudeSettings estaba disponible y que no lo estaba.
   * El bloqueo se producía debido a una llamada de función en un puntero compartido nulo (auditudeSettings). Se ha añadido una comprobación condicional en VideoEngineTimeline::placeToSourceTimeline() para asegurarse de que auditudeSettings esté disponible antes de llamar a cualquier cosa en ese objeto.
* ZD #32584 - No se puede acceder a la información completa presente en el &lt;extensions> nodo de una respuesta VAST.
   * Se ha corregido el problema en el análisis de XML y ahora NetworkAdInfo proporciona la información completa presente en la variable &lt;extensions> nodo .
* ZD #35086 : no se obtienen datos de extensión completos del reproductor si hay respuestas VMAP específicas.
   * El problema era específico de la extensión xml, ya que el análisis XML no funcionaba si la extensión xml tenía comillas dobles dentro del valor de atributo. Se ha corregido el problema.

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 - Sesión de reproducción que habilita la depuración remota de webview.
   * WebViewDebuging está establecido en False de forma predeterminada. Para habilitar la depuración, configúrela como true a través de la aplicación, usando setWebContentsDebuggingEnabled(true).
* ZenDesk#33011 - La cronología del anuncio no se resuelve si hay una solicitud CRS fallida.
   * Cuando falla una solicitud CRS a un anuncio, la cronología se resuelve y se reproducen los anuncios restantes.
* ZenDesk#34528 - La resolución de vídeo no se actualiza más allá de las 640x360 en la llave de la tercera generación de FireTV.
   * La resolución de vídeo se activa como conmutadores de velocidad de bits.
* ZenDesk#33192 - AudioTrack tiene un nombre nulo cuando se recupera la pista a través de AudioUpdatedEventListener::onAudioUpdated.
   * En algunos casos en FireTV Stick, el evento onAudioUpdate se activaba cuando no había ninguna actualización de audio. Esto se ha solucionado ahora.

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - La suscripción de etiquetas personalizadas TimedMetadata no funciona.
   * Devolvemos datos de ID3 como una matriz de bytes (para admitir datos de APIC o genéricos) al cliente, mientras que en la cadena de retorno 1.4. La matriz de bytes no gestiona el propio carácter terminado nulo, por lo que estaba mostrando un carácter especial al cliente. Este problema se ha solucionado ahora.
* Zendesk#32670 - El reproductor no falla en una lista de reproducción redundante
   * Esto está funcionando bien ahora y setNetworkDownVerifyUrl está funcionando como se esperaba.
* Zendesk#32369 - El subtítulo muestra diferentes colores de basura o artefactos.
   * El problema con los problemas de CC se ha corregido en la última versión
* Zendesk#25590 - Mejora: Almacén de cookies TVSDK (C++ a Java™)
   * Ahora, Android™ TVSDK admite el acceso a cookies entre la capa Java™ (almacenada en CookieStore de la aplicación Android™) y la capa C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 no parece tener la corrección para PTPLAY-20269 Este problema se ha corregido e integrado en la rama 2.5.2.
* Zendesk#31806 - Los palos de Auditude en PREPARING Player se quedaron en estado Preparando porque el xml de respuesta tenía una etiqueta vacía. Ahora el problema está solucionado.
* Zendesk#31727 - Los caracteres de subtítulos optativos de TVSDK 2.5 se eliminan o se escriben mal.
   * El problema se ha solucionado y no estamos soltando/escribiendo mal ningún carácter.
* Zendesk#31485 - DrmManager en 2.5
   * Hubo algún problema en Creación de DrmManager a través del nuevo DrmManager(Context context). Se ha implementado la clase DRMService que proporcionaría DRMManager.
* El flujo de resolución Zendesk#32794- 1080P no se reproduce en Android™.
   * Hemos cambiado SizeAvailableEvent. Anteriormente, `getHeight()` y `getWidth()` los métodos SizeAvailableEvent de la versión 2.5 se utilizaban para devolver la altura y la anchura del marco del marco, que el formato de medios devolvía. Ahora devuelve la altura de salida y el ancho de salida respectivamente devueltos por el decodificador.
* El Flash Player de Zendesk #19359 se bloquea debido a la posición del atributo #EXT-X-FAXS-CM en el manifiesto de nivel de conjunto.
   * La etiqueta #EXT-X-FAXS-CM siempre debe aparecer en la lista de reproducción superior antes de que la velocidad de bits o los segmentos individuales aparezcan en la lista de reproducción.

**Android™ TVSDK 2.5.2**

* Zendesk#17305 Artefactos en subtítulos cerrados con fondo no opaco.
Se expone la propiedad setTreatSpaceAsAlphaNum en TextFormat. De forma predeterminada, la propiedad es False. Establezca la propiedad como True en un cliente para resolver el problema del espacio oscuro.

* Zendesk#25097 CC muestra artefactos visuales con ajustes CC.
Se expone la propiedad setTreatSpaceAsAlphaNum en TextFormat. De forma predeterminada, la propiedad es False. Establezca la propiedad como True en un cliente para resolver el problema del espacio oscuro.

* Zendesk #31620 La cadena del agente de usuario que sale del reproductor TVSDK está truncada.
La cadena del agente de usuario ya no se truncará después de 128 caracteres.
La cadena de versión de Adobe Primetime se agrega al agente de usuario del sistema.

* El evento SEEK_END que falta en Zendesk #30809 evita que la aplicación pase a estar en estado de reproducción.
* El color &#39;cian&#39; de Zendesk #30415 de subtítulo es ahora un tono azul más oscuro (turquesa), en comparación con las versiones anteriores de TVSDK de Primetime.

   El color cambia de DarkCyan a cian.

* Los anuncios de VOD de Zendesk #30727 no se descargan ni resuelven.

   En VMAP XML si hay una etiqueta VAST vacía sin una etiqueta de cierre explícita (&quot;&lt;/vast>&#39;) y sin un carácter de nueva línea después de él, el XML VMAP no se analiza correctamente y es posible que no se reproduzcan anuncios.

**Android™ TVSDK 2.5.1**

* Bloqueo específico del dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA con Auditude y haga clic en los anuncios.
* VHL: se envían llamadas de Heartbeat incorrectas al iniciar contenido desde un desplazamiento.
* Cuando se reproducen anuncios VPAID, VHL Heartbeat invoca un evento:type:falta el anuncio de reproducción.
* Después de entrar en el estado COMPLETE , el reproductor vuelve al estado PLAYING con SKIP adBreakPolicy para anuncios posteriores a la emisión.
* Las cookies no se adjuntan a las llamadas de retorno de anuncios salientes.
* Los puntos de referencia de anuncios no están visibles.
* HLS con seguimiento SAP EAC3 independiente no se cargará.
* El reproductor se bloquea cuando TVSDK recibe una pantalla en la que se activa una vez restaurado el Media Player.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* TVSDK 2.7 admite resolución simultánea de hasta cinco anuncios.
* En el caso de una respuesta de VMAP, las llamadas de anuncio en una sola pausa publicitaria se dirigen simultáneamente y las pausas publicitarias se resuelven secuencialmente.
* En el caso de un FER, las llamadas de anuncio en cada oportunidad se resuelven simultáneamente.

### Problemas y limitaciones conocidos en las versiones anteriores{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* No se admiten varias pausas publicitarias VMAP al mismo tiempo.

**Android™ TVSDK 2.5.3**

Esta versión tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja o condiciones de red deficientes.
* Para los flujos FER, virtualTime y localTime pueden diferir. También FER con desplazamiento no funciona.
* La reproducción puede quedar atascada cuando se busca el contenido del audio de enlace tardío.
* De forma intermitente, los subtítulos webVTT pueden no estar sincronizados con el contenido en directo.
* De forma intermitente, se puede ver una reproducción rápida de unos pocos fotogramas después de salir de una pausa publicitaria.
* A veces, se produce un error 303 en Triple Wrapper Ad Break, aunque se reproduzcan los anuncios.

**Android™ TVSDK 2.5.2**

Esta versión tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja.
* La reproducción puede bloquearse a veces al buscar el final del contenido de VOD.
* Para los flujos FER, virtualTime y localTime pueden diferir. Además, FER con desplazamiento no funciona.

**Android™ TVSDK 2.5.1**

Esta versión de TVSDK tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja.
* Para los flujos FER, virtualTime y localTime pueden diferir. Además, FER con desplazamiento no funciona.
* En VMAP XML, si hay una etiqueta VAST vacía sin una etiqueta de cierre explícita (&lt;/vast>), y sin una nueva línea después de ella, el XML VMAP no se analiza correctamente y es posible que los anuncios no se reproduzcan.
* No se admiten las versiones posteriores a la emisión de VPAID.

## Recursos útiles {#helpful-resources}

* [Requisitos del sistema](/help/programming/tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md)
* [Guía del programador de TVSDK 2.7 para Android™](/help/programming/tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-prod-audience-guide.md)
* [TVSDK Android™ Javadoc para referencia de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [Documento de la API de TVSDK Android™ C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) - Cada clase Java™ tiene una clase C++ correspondiente, y la documentación de C++ contiene material más explicativo que los documentos Java™, por lo que consulte la documentación de C++ para conocer mejor la API de Java™.
* [Guía de migración de TVSDK 1.4 a 2.5 para Android™ (Java™)](/help/migration-guides/tvsdk-14-25-android.md)
* Para controlar los escenarios de encendido/apagado de la pantalla, consulte la sección `Application_Changes_for_Screen_On_Off.pdf` incluido en la compilación.
* Consulte la documentación de ayuda completa en [Información y asistencia de Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
