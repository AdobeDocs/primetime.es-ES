---
title: Notas de la versión de TVSDK 2.4 del explorador
description: Las notas de la versión de TVSDK 2.4 del explorador describen las funciones nuevas, admitidas y no admitidas, así como los problemas conocidos en el SDK 2.4 del explorador.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 83fdf530-5cbb-41d9-ab2a-28e117f04488
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# Notas de la versión de TVSDK 2.4 del explorador {#browser-tvsdk-release-notes}

Las notas de la versión de TVSDK 2.4 del explorador describen las funciones nuevas, admitidas y no admitidas, así como los problemas conocidos en el SDK 2.4 del explorador.

## Introducción {#introduction}

El SDK de explorador es un kit de herramientas que le permite añadir funcionalidad avanzada de reproducción de vídeo, protección de contenido y publicidad a sus aplicaciones de reproductor de vídeo basadas en navegador.

El explorador TVSDK 2.4 proporciona API de JavaScript para crear aplicaciones de vídeo basadas en navegador e incluye compatibilidad con la reproducción en los siguientes modos:

* solo HTML5
* HTML5 con reserva de flash automático
* Flash siempre

Esta versión incluye la siguiente información:

・ [Documentación de la API TVSDK del explorador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ [Guía de programación del TVSDK del explorador](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ [Guía de migración de TVSDK para DHLS 1.4 al explorador TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

・ [Conversión de Browser TVSDK 2.4.6 a la versión 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ Una implementación de referencia, que se incluye en la compilación.

>[!NOTE]
>
>*Para obtener una lista completa de las consideraciones de seguridad de esta versión, consulte Consideraciones de seguridad.

## Novedades y funciones compatibles {#what-s-new-and-supported-features}

Esta versión de TVSDK del explorador proporciona nuevas funciones que puede utilizar para mejorar sus aplicaciones de vídeo.

**Novedades de la actualización 2.4.12 (compilación 204)**

La siguiente adición está disponible como parte de la actualización de TVSDK 2.4.12 del explorador (compilación 204):

* La implementación de la API de volumen de AdobePSDK.MediaPlayer se ha cambiado para permitir la reproducción automática en iOS cuando la reproducción está silenciada.

・ Una nueva API, `auditudeSettings.ignoreVPAIDAds`, se agrega para permitir ignorar las publicidades VPAID recibidas del servidor de Auditude. La API no funciona para la reserva de Flash.

**Versión 2.4.11**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.11 del SDK de explorador:

・ El failover de segmentos HLS Live es compatible con los modos de MSE y Flash de reserva.

・ Soporte para `AuditudeSettings.creativeRepackagingDomain` La API de también está disponible para MSE. Anteriormente solo se admitía con el modo de reserva de Flash.

・ La versión contiene correcciones para problemas críticos con los clientes. Consulte *Problemas solucionados* una lista.

**Versión 2.4.10**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.10 del SDK de explorador:

・ TVSDK proporciona enableLogging() para habilitar o deshabilitar el registro. Consulte la [Documentación de API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)para uso.

・ TVSDK ya no es compatible con los capítulos predeterminados al usar Adobe Analytics. Defina y administre Capítulos con su aplicación.

・ La versión contiene correcciones para problemas críticos con los clientes. Consulte *Problemas corregidos *una lista.

**Versión 2.4.9**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.9 del SDK de explorador:

・ Los flujos HLS VOD y Live con discontinuidad horaria pero sin marcadores de discontinuidad son compatibles.

・ Los fotogramas ID3 v2.4.0 son compatibles con la etiqueta de vídeo Safari para los flujos VOD y en directo HLS.

・ La implementación de carga segura de anuncios garantiza que las llamadas al servidor de publicidad se actualicen a HTTP seguro según la configuración de la API. Para obtener más información, consulte las clases AdobePSDK.AdvertisingMetadata y AdobePSDK.ForceHttpsAdConfiguration . Esta función no se admite en el modo de reserva de Flash.

・ La información del ID de anuncio y la información de extensión asociada con las respuestas VAST 3.0 ahora están disponibles para la aplicación por parte de TVSDK y pueden utilizarse para implementar la integración de Moat para las mediciones de anuncios. Para obtener más información, consulte API de AdobePSDK.NetworkAdInfo . Esto no se admite en el modo de reserva de Flash.

・ La clase AdobePSDK.ForceHttpsConfiguration ya no está disponible. Se completa con

Clase AdobePSDK.ForceHttpsAdConfiguration.

・ Ahora hay disponible una nueva API, AdobePSDK.optimizeFlashCalls, para optimizar las llamadas y mejorar la experiencia de reproducción de HLS en el modo de reserva de Flash. Esta opción está desactivada de forma predeterminada.

**Novedades en la actualización 2.4.8 (compilación 6002)**

Esta actualización contiene correcciones para problemas críticos con los clientes. Consulte *Problemas solucionados*, para la lista.

**Versión 2.4.8**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.8 del SDK de explorador:

・ El SDK ahora es compatible con Chrome EME y los cambios de prácticas recomendadas disponibles a partir de Chrome v58. Para obtener más información, consulte [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ El marco de IU ahora es compatible con HLS Access DRM en el Flash, solo publicidad y flujo de trabajo de información de objetivo.

・ La API setDRMAuthenticateData se agrega al marco de IU. Para reproducir flujos protegidos con DRM de acceso a Adobe, invoque esta API. Alternativamente, el atributo drmAuthenticateData se puede especificar en el reproductor. Consulte [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)para obtener más información.

**Versión 2.4.7**

Las siguientes funciones son nuevas en la versión 2.4.7:

・ Adición del configurador de IU en el marco de IU

Puede configurar el reproductor de una de las siguientes maneras:

・ Uso de un objeto JSON

・ Uso de API

Para ayudar a generar el objeto JSON, el SDK de explorador proporciona una herramienta **Configurador de interfaz de usuario **.

En esta herramienta, puede seleccionar varias opciones de configuración, hacer clic en **Probar configuración **para comprobar las opciones de configuración y hacer clic en **Descargar configuración **para descargar las opciones de configuración. Después de descargar el archivo, puede pasar el contenido de este archivo como objeto JSON a la API ptp.videoPlayer.

・ Adición de la API MediaPlayerItemConfig al marco de IU

A través de MediaPlayerItemConfig se pueden configurar varias funciones, como advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration. Para obtener más información, consulte la documentación de AdobePSDK.MediaPlayerItemConfig en la [API de TVSDK de navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [documentación](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

En la interfaz de usuario de Framework, se ha modificado la forma de pasar configuraciones de red a través de la configuración del reproductor.

**Versión 2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**Versión 2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* Compatibilidad con los flujos de trabajo de DRM y Analytics en el marco de la interfaz de usuario

Las configuraciones de DRM y el seguimiento de Analytics se pueden habilitar mediante el marco de IU.

* Adición de `AdobePSDK.embedSWFinFullScreenDiv` API

Esta nueva API proporciona flexibilidad a la aplicación del reproductor para seleccionar el div en el que puede incrustar el archivo FlashFallback.swf.

* Reemplazado `getVersion`API de `AdobePSDK.MediaPlayer` class con `AdobePSDK.Version` clase para información relacionada con la versión de TVSDK. Para obtener más información, consulte `AdobePSDK.Version` API [here](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versión 2.4.6**

Las siguientes funciones son nuevas en la versión 2.4.6:

* **Explorar compatibilidad**

Browserify le permite utilizar los módulos de estilo node.js en el explorador. Puede definir las dependencias y Examinar agrupa todo en un archivo JavaScript.

* **Facturación**

Con la ayuda de la facturación, el SDK de explorador puede recopilar métricas de uso del reproductor para facturar a los clientes de Primetime.

>[!NOTE]
>
>La enumeración obsoleta MediaPlayer.Events y las constantes obsoletas de Enum PSDKErrorCode se han eliminado en la versión 2.4.6. Para obtener más información, consulte [Conversión de Browser TVSDK 2.4.5 a la versión 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versión 2.4.5**

Las siguientes funciones son nuevas en la versión 2.4.5:

* **Revistas de eventos completos y anuncios**

   Los flujos de reproducción de eventos completos (FER) de HLS ahora son compatibles con la resolución de anuncios y los comportamientos publicitarios. Para habilitar esta compatibilidad, establezca el modo de señalización de publicidad en `MANIFEST_CUES` al crear la variable `MediaPlayerItemConfig` objeto.

* **Compatibilidad con la directiva de escala de MediaPlayerView**

   Los desarrolladores de aplicaciones ahora pueden especificar un scalePolicy diferente para la vista mediante la propiedad scalePolicy de MediaplayerView .

* **Compatibilidad con contenido anamórfico**

   Ahora se admite la reproducción de contenido anamórfico al utilizar MSE y la reproducción de Flash.

* **Aplicación selectiva de`withCredentials`**

When `withCredentials` se establece en true, la variable `Access-Control-Allow-Origin` no se puede establecer en comodines. Según la respuesta del servidor, el TVSDK del explorador establecerá de forma selectiva la variable `withCredentials` atributo. Para obtener más información sobre esta compatibilidad, consulte [Documentos de API de TVSDK del explorador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versión 2.4.4**

Las siguientes funciones fueron nuevas en la versión 2.4.4:

* **Aplicación de ejemplo de Chromecast**

Esta versión es compatible con una aplicación de remitente y receptor que muestra la reproducción de flujos de VOD DASH y flujos de Widevine DASH con inserción de anuncios del lado del cliente.

* **Compatibilidad avanzada con failover**

Esta versión contiene soporte para casos de uso de failover avanzado (failover de segmentos y servidores) para flujos VOD HLS.

**Versión 2.4.3**

Las siguientes funciones fueron nuevas en la versión 2.4.3:

* **Etiquetas personalizadas para DASH VOD**

   Las etiquetas personalizadas en línea (eventos) se pueden suscribir y recibir como objeto TimedMetadata .

* **Reproducción de emisiones sin extensiones**

   Ahora se admiten los flujos HLS y DASH sin extensiones. Para el archivo de manifiesto, se debe especificar resourceType al cargar el recurso. Para segmentos y archivos VTT, el encabezado de respuesta Content-Type se utiliza para determinar el tipo de contenido.

**Versión 2.4.2**

Las siguientes funciones fueron nuevas en la versión 2.4.2:

* **Paridad de API**

Para obtener una lista completa de la paridad de API, consulte la [Guía de migración de TVSDK para DHLS 1.4 al explorador TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Compatibilidad con AES de muestra**

   Esta versión añade compatibilidad con la reproducción de contenido cifrado de Sample-AES en MSE y la reserva de Flash. Se ha eliminado el requisito de alojar contenido AES en un origen seguro en Google Chrome.

* **Compatibilidad con contenedores AAC**

   Ahora se admite la reproducción de archivos con la extensión .aac. Pueden ser emisiones solo de audio o audio alternativo.

   >[!NOTE]
   >
   >Los códecs AC3 y AC3 mejorados aún no son compatibles.

* **Reproducción de flujo con token**

Los flujos HLS que se entregan a través de una red de entrega de contenido (CDN) a veces pueden utilizar tokens de autenticación en el manifiesto y las solicitudes de segmento para la verificación, y estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookies. Ahora se admite la reproducción de estos flujos.

**Versión 2.4.1**

Las siguientes funciones fueron nuevas en la versión 2.4.1:

* **Marco de la interfaz de usuario**

Este marco de trabajo, diseñado para acelerar el desarrollo de la IU para aplicaciones de reproductor de vídeo basadas en JavaScript, consta de API para incluir controles básicos como reproducción/pausa y volumen, y para añadir o eliminar fácilmente elementos como estados de barras de desplazamiento y ajustes de subtítulos. Puede especificar el comportamiento asociado a los controles, crear controles personalizados y aplicar piel a la IU del reproductor. Todo esto sucede a través del marco de trabajo, sin necesidad de manipular la estructura DOM directamente.

* **Mejoras de reproducción de HLS para emisiones en directo**

Esta versión admite las interrupciones causadas por la inserción de anuncios. Utiliza la etiqueta EXT-PROGRAM-DATE-TIME seguida de la etiqueta EXT-MEDIA-SEQUENCE para sincronizar entre perfiles de velocidad de bits adaptables para una reproducción sin problemas.

* **Compatibilidad con VPAID 2.0**

La definición de interfaz de servicio de publicidad (VPAID) del reproductor de vídeo, versión 2.0, ofrece una experiencia de medios enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo. Esta versión es compatible con las publicidades VPAID de JavaScript lineales para contenido de vídeo bajo demanda (VOD).

* **Etiquetas HLS personalizadas**

Los flujos de contenido pueden incluir metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto. El SDK del explorador le permite especificar y suscribirse a etiquetas adicionales y recibir notificaciones cuando esas etiquetas aparezcan en el manifiesto.

* **Marcadores de anuncio mostrados en la cronología del reproductor**

Esta versión admite la visualización de marcadores de anuncios en la cronología del reproductor tanto para VOD como para contenido en directo. Puede ver este comportamiento en el reproductor de referencia.

**Compatible con 2.4**

Las siguientes funciones estaban disponibles en la versión 2.4:

* **Reproducción de audio MP3**

   Esta versión es compatible con la reproducción de audio MP3 en exploradores con extensiones de fuente de medios (MSE) y con la etiqueta de vídeo Safari.

* **Reproducción de vídeo MP4**

   Se admiten las siguientes funciones:

   * Reproducción de un solo flujo
   * Anuncios previos y posteriores a la emisión de MP4 con comportamientos y seguimiento de anuncios
   * Anuncios HLS pre-roll y post-roll con comportamientos y seguimiento de anuncios
   * Anuncios DASH pre-roll y post-roll con comportamientos y seguimiento de anuncios

## Plataformas compatibles {#supported-platforms}

El SDK de explorador tiene requisitos específicos para los niveles de plataformas y software en los que debe ejecutarse. Se admiten las siguientes plataformas y niveles de software:

### Configuraciones de escritorio {#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* Apple OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### Configuraciones web móviles {#mobile-web-configurations}

* Android 4.4

   * Explorador nativo
   * Chrome 33+

* Android 5.0

   * Explorador nativo
   * Chrome 33+

* Android 6.0

   * ・ Chrome 33+

* Apple iOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast (segunda generación; solo para reproducción de DASH)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Tecnología</strong> </p> </td> 
   <td><p><strong>Etiqueta de vídeo TVSDK del explorador</strong><sup>1</sup></p> </td> 
   <td><p><strong>MSE de TVSDK del explorador</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>Tecnología predeterminada</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>Etiqueta de vídeo</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS y DASH</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>Etiqueta de vídeo</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS y DASH</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS y DASH</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS, DASH</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de funciones {#feature-matrix}

Esta es una lista de las funciones compatibles y no compatibles con esta versión:

* *Funciones de audio MP3: reproducción principal*
* *Funciones de vídeo MP4: reproducción principal*
* *Funciones de vídeo MP4: Ad Insertion principal*

>[!NOTE]
>
>*En las tablas de matriz de características que aparecen a continuación, una &quot;Y&quot; significa que la función es compatible con la versión actual.*

### Funciones de audio MP3 {#mp-audio-features}

**Tabla 1: Reproducción principal{#table-core-playback}**

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD MP3 | Reproducción general (reproducción, pausa, llamada a otro punto del contenido) | No admitido | Y | Y |

1 La etiqueta de vídeo TVSDK del explorador no admite flujo continuo y DRM. La compatibilidad con códec y contenedor no es la misma en todos los navegadores.

2 El valor predeterminado de Firefox es Flash Player para la versión 41 o anterior.

### Funciones de audio MP4 {#mp-audio-features-1}

**Tabla 2: Reproducción principal**

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD MP4 | Reproducción general (reproducción, pausa, llamada a otro punto del contenido) | No admitido | Y | Y |

**Tabla 3: Ad Insertion principal**

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD MP4 | Anuncio previo a la emisión (MP4) | No admitido | Y | Y |
| Ad Insertion | VOD MP4 | Anuncio (MP4) | No admitido | Y | Y |

Para obtener más información sobre la compatibilidad con funciones HLS o DASH, consulte a continuación.

## Matriz de funciones HLS {#hls-feature-matrix}

Esta es la matriz de características de las funciones HLS en el SDK de TVSDK de navegador.

* *Reproducción principal de HLS*
* *HLS Funciones de reproducción avanzadas*
* *Funciones de protección de contenido HLS*
* *Funciones de inserción de anuncios principales de HLS*
* *HLS Funciones avanzadas de inserción de anuncios*
* *Integraciones HLS*

>[!NOTE]
>
>*En las tablas de matriz de características que aparecen a continuación, una &quot;Y&quot; significa que la función es compatible con la versión actual.*

### Funciones HLS {#hls-features}

Se admiten las siguientes funciones:

**Tabla 4: Reproducción principal de HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Reproducción general (reproducción, pausa, búsqueda)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Reproducción general (reproducción, pausa y búsqueda)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Tasa de bits adaptable</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Subtítulos 608/708</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Solo VOD</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Error de manifiesto</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Failover avanzado</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Notificaciones de QoS y del reproductor</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Compatibilidad limitada con QoS</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Compatibilidad con encabezados de cookie</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Configuración de parámetros de control de búfer</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Establecer adaptable</p> <p>controles de velocidad de bits</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Etiquetas personalizadas</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td>Audio de enlace tardío</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>302 redireccionamiento</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 5: Funciones de reproducción avanzadas de HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción con desplazamiento</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción solo de audio</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción complicada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción suave y difícil</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Análisis de ID3</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Compatibilidad con el marcador de discontinuidad</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Transmisiones con token</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Facturación</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 6: Funciones de protección de contenido HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Ejemplo-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Acceso a Adobe</p> </td> 
   <td><p>No admitido</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 7: Funciones de inserción de anuncios principales de HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Antelación (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Mid-roll (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anuncio (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Resolución y comportamientos de los anuncios</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Política de publicidad predeterminada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Reempaquetado creativo (MP4 a HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 8: HLS Funciones avanzadas de inserción de anuncios**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo publicidad</p> </td> 
   <td><p>No admitido</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Parámetros de objetivo</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Parámetros personalizados</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Política de publicidad personalizada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Carga de publicidad diferida</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>No admitido</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anuncios complementarios, anuncios tipo titular, anuncios en los que se puede hacer clic</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 9: Integraciones HLS{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integraciones</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Integración de VHL de Adobe Analytics</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de funciones DASH {#dash-feature-matrix}

Esta es la matriz de funciones para las funciones DASH en el SDK de TVSDK del explorador.

・ *Funciones de reproducción principal de DASH*

・ *Funciones de reproducción avanzadas de DASH*

・ *Funciones de protección de contenido DASH*

・ *Funciones de inserción de anuncios principales de DASH*

・ *Funciones avanzadas de inserción de anuncios de DASH*

・ *Integraciones de DASH*

>[!NOTE]
>
>En las tablas de matriz de características que aparecen a continuación, un Y significa que la función es compatible con la versión actual.

### Funciones de DASH {#dash-features}

Se admiten las siguientes funciones:

**Tabla 10: Funciones de reproducción principal de DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Reproducción general (reproducción, pausa, búsqueda)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Reproducción general (reproducción, pausa y búsqueda)</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Tasa de bits adaptable</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Subtítulos 608/708</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Failover</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Notificaciones de QoS y del reproductor</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Compatibilidad con encabezados de cookie</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Configuración de parámetros de control de búfer</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Establecer controles de velocidad de bits adaptables</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Etiquetas personalizadas (EventStream)</p> </td> 
   <td><p>Solo VOD (en línea)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Audio enlazado tarde</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>302 redireccionamiento</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 11: Funciones de reproducción avanzadas de DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción con desplazamiento</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción solo de audio</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción complicada</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción suave y difícil</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Análisis de ID3</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Compatibilidad con varios períodos</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Transmisiones con token</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Facturación</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 12: Funciones de protección de contenido DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Ejemplo-AES</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Widevine on Chrome, Firefox 47 y posteriores, y Chromecast</p> <p>・ PlayReady en Internet Explorer en Windows 8.1 y Edge</p> <p>・ Primetime DRM para Windows Firefox (solo vídeo)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 13: Funciones de inserción de anuncios principales de DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Antelación (MP4/DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anuncio (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Resolución de anuncios y comportamientos</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Política de publicidad predeterminada</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Reempaquetado creativo (MP4 a DASH)</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 14: Funciones avanzadas de inserción de anuncios de DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo publicidad</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parámetros de objetivo</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parámetros personalizados</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Política de publicidad personalizada</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Carga de publicidad diferida</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anuncios complementarios, anuncios tipo titular, anuncios en los que se puede hacer clic</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 15: Integraciones de DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integraciones</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Integración de VHL de Adobe Analytics</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemas solucionados {#issues-fixed}

**Problemas corregidos en la actualización 2.4.12 (compilación 204)**

Los siguientes problemas se solucionan en la actualización de la versión 2.4.12 del SDK de TVSDK del explorador (compilación 204):

・ **21647**: TVSDK debe permitir la reproducción automática de vídeo en dispositivos iOS cuando el audio está silenciado.

・ **21465**- Error Key System Access Denied se recibe al reproducir un flujo DASH protegido por DRM después de reproducir un flujo en directo DASH.

・ **21442**: habilite la reproducción automática del contenido en la web de iOS después de que el anuncio previo se reproduzca con un gesto del usuario.

・ **21240**: API proporcionada para filtrar anuncios VPAID analizados desde Auditude/VMAP.

**Problemas corregidos en la versión 2.4.11**

Los siguientes problemas se han corregido en la versión 2.4.11 del SDK de TVSDK para navegadores:

**Funciones principales de reproducción:**

・ **19192**: TVSDK ahora implementa TextFormat:bottomInset y TextFormat:safeArea. Debido a estas mejoras, se pueden volver a colocar los subtítulos si la barra de control se muestra en la pantalla.

・ **21009**: Los subtítulos permanecen en la pantalla en caso de búsqueda a través de la discontinuidad hasta que aparecen nuevos subtítulos.

・ **21141**: La llamada de retorno se rechaza debido a una condición de carrera durante la adición de segmentos.

・ **21142**: Disponibilidad de intervalos de reproducción buscables cuando el reproductor está en estado INITIALIZADO. Debido a estos cambios, ahora se admite el inicio de sesión en la posición .

・ **21363**: Los subtítulos cerrados 608/708 no están sincronizados después de la inserción de anuncios para flujos DASH.

**Funciones de inserción de publicidad:**

・ **21179**: Los problemas relacionados con mid-roll (pausas largas, marcos negros) con contenido de VOD ahora se resuelven estableciendo correctamente la propiedad ad.primaryAsset.adParameters .

・ **21257**: El archivo MP4 con la tasa de bits más alta se selecciona para la transcodificación si MP4 no es un tipo mime válido y la función de reempaquetado creativo está habilitada.

・ **21361**: TVSDK ahora pasa el sistema de publicidad y el ID creativo de la respuesta VAST como parámetros de consulta en la solicitud de paquete creativo para admitir reglas de normalización adicionales.

**Problemas corregidos en la versión 2.4.10**

Los siguientes problemas se han corregido en la versión 2.4.10 del SDK de TVSDK para navegadores:

**Funciones principales de reproducción:**

・ **21060**: Error de códec no válido generado con flujos HLS que contienen discontinuidad y los cuadros ISO BMFF se ejecutan al final del flujo.

・ **21045**: La reproducción automática no funciona en iOS después de completar la primera reproducción de vídeo en una lista de reproducción.

・ **20975**: El proveedor de QoS devuelve la velocidad de fotogramas como NaN en el explorador Chrome.

・ **20823**: Error de códec no admitido generado en segmentos de encuentro sin datos.

・ **20769**: El SDK ahora comienza con la velocidad de bits actual en la búsqueda en lugar de cambiar inmediatamente según la política ABR.

・ **20031**: Cuando se encuentra en modo vertical en IE11 (Windows 8.1), la pantalla de vídeo se vuelve pequeña. Función de protección de contenido:

・ **19316**: Omita los segmentos que fallan en el descifrado en el caso de flujos HLS AES-128.

**Problemas corregidos en la versión 2.4.9**

Los siguientes problemas se han corregido en la versión 2.4.9 del SDK de TVSDK para navegadores:

**Funciones principales de reproducción:**

・ **13407**: Los flujos DASH pueden paralizarse si Firefox deja de enviar el evento &quot;ontimeupdate&quot; durante la reproducción.

・ **16380**: Durante la reproducción de contenido de vídeo de audio mixto de segmentos que tienen tiempos de inicio no coincidentes a través de MSE, el error de sincronización de audio entre representaciones se acumula en los conmutadores ABR, lo que finalmente resulta en un error (problema de cromo #663686).

・ **17985**: Al reproducir un flujo ISO-BMFF específico en el navegador Firefox, la reproducción se atasca (problema de Firefox #1342913). Esto se ha solucionado desde Firefox v53.

・ **19141**: Error de referencia no capturado (en promesa): la anchura no está definida.

・ **18997, 1929**: Problema con el parpadeo del vídeo en el límite del segmento. Esto ocurría porque el SDK no calculaba correctamente el desplazamiento de tiempo de composición de la última muestra.

・ **19780**: La reproducción no comienza con el contenido de HLS ni con el anuncio de HLS en Firefox v53 (número de Firefox 354653).

・ **20046**: La hora del programa se recibe como clave en lugar de valor cuando se recibe como objeto de metadatos temporizados.

・ **20047**: useDefaultResizeHandler genera un error con la reserva de Flash.

・ **20179**: La reserva de Flash no funciona con el Flash Player v25.0.0.171.

・ **20293**: Firefox deja de almacenar en búfer los datos de ciertos flujos HLS que llevan a la paralización.

・ **20626**: El reproductor genera un error de descodificación de medios en Chrome debido a la administración incorrecta de muestras de vídeo de duración cero.

・ **20078**: La reproducción se detiene en el error del explorador &quot;Se excedió la cuota&quot;.

・ **18639**: En HLS Live stream 608 CC el texto a veces aparece como mal escrito.

・ **20028**: El parámetro de tamaño ClosedCaptions no cambia el tamaño de fuente.

・ **20613**: Los cuadros de subtítulos se superponen entre sí, por lo que son ilegibles.

**Funciones del Ad Insertion principal (CSAI):**

・ **20043**: Falta las llamadas de impresión y seguimiento de anuncios con varios anuncios y redirecciones de terceros.

・ **2004**: Al utilizar el reempaquetado creativo, es necesario volver a empaquetar todas las publicidades de la pausa publicitaria correctamente. De lo contrario, la pausa publicitaria se descarta completamente.

・ **20097**: La reproducción del anuncio se omite y el contenido principal se reanuda inmediatamente, en lugar de esperar un tiempo de espera de 20 segundos si el manifiesto del anuncio no está disponible.

**Problemas corregidos en la actualización de la versión 2.4.8 (compilación 6002)**

Los siguientes problemas se solucionan en la actualización de la versión 2.4.8 del SDK de TVSDK del explorador (compilación 6002):

・ **14126:** La reproducción puede paralizarse en Firefox (problema #1316024) debido a una brecha interna en el búfer de origen de MSE. Intente buscar para reanudar la reproducción

・ **19608:** Corrección para honrar el valor de compensación horaria de la respuesta VMAP de Auditude.

・ **19635:** Corrige la detención de vídeo en Internet Explorer 11 en Windows 10.

・ **19761:** Correcciones de problemas de ABR con HLS.

・ **19780:** Corrige la reproducción del anuncio con contenido HLS dañado en Mozilla Firefox v53.

・ **19877 y 1974:** Los problemas corrigen la incoherencia al seleccionar la velocidad de bits después de una operación de búsqueda. Ahora, la selección de velocidad de bits en la búsqueda es el valor inferior de la velocidad de bits actual y la velocidad de bits en el inicio.

・ **19881:** La reproducción atascada y la superposición de almacenamiento en búfer aparecen durante un tiempo infinito después de que la llamada a otro punto del contenido se realice de 3 a 4 veces.

・ **1984:** Confirme el cumplimiento de los requisitos de Chrome 59 Beta Verified Media Path (VMP). bTVSDK pudo reproducir contenido Widevine DRM con Chrome 59 Beta.

・ **19916:** Se interrumpió la reproducción de DRM en la interfaz de usuario del marco. Ahora, invoca acquisitionLicense incluso si no hay ninguna política en los metadatos.

**Problemas corregidos en la versión 2.4.8**

Los siguientes problemas se han corregido en la versión 2.4.8 del SDK de explorador:

・ **10075**: Al buscar antes de la línea de tiempo, el evento de finalización de reproducción no se recibía en Firefox ni Chrome y el evento de búsqueda no se recibía en Firefox.

・ **15775**: Reproducir el evento completo no recibido en Windows 8.1 Internet Explorer.

・ **17306**: Para flujos SSAI, se admite la reproducción. No se admite el seguimiento de la publicidad vinculada.

・ **19142**: A veces, rebobinar hace que el reproductor de vídeo permanezca en estado de almacenamiento en búfer para siempre.

・ **19218**: Los marcadores de anuncio no están disponibles a través del marco de IU.

・ **19219**: La reproducción solo de anuncios no funciona a través del marco de IU.

・ **1922**: La clave AES-128 se solicita una vez para una lista de reproducción y las solicitudes posteriores se proporcionan desde la caché. Anteriormente, se solicitaba para cada segmento.

・ **19597**: &quot;Error de tipo no capturado: No se puede leer la propiedad &quot;log&quot; de undefined&quot; se vio con las compilaciones de Chrome canary.

・ **19 605**: adRequestDomain no estaba disponible en el modo de reserva de Flash.

・ **19 608**: Los anuncios VMAP no se insertaban para las transmisiones en directo de HLS. El SDK ahora considera los marcadores de referencia y no se basa en los valores de compensación de tiempo en las respuestas VMAP.

・ **19637**: La reproducción de los anuncios solo produce un error de secuencia de comandos al final del anuncio.

・ **19732**: Las solicitudes de la lista de reproducción CRS fallaban con el error 404. Las solicitudes 1401 y 1403 del Explorador TVSDK ahora se actualizan para encargarse de ello.

・ **19762**: se solía llamar a acquisitionLicense antes de setAuthenticationToken porque se devolvió una licencia válida independientemente de la validez del token. Esto se corrige ahora y acquisitionLicense solo se llama después de la respuesta setAuthenticationToken .

**Problemas corregidos en la versión 2.4.7**

En la versión 2.4.7 se corrigieron los siguientes problemas:

・ **8397**: Es posible que las transmisiones en directo de HLS generadas a través de Adobe Medium Server no se reproduzcan si los segmentos no comienzan con un fotograma de clave.

・ **13606**: Se han corregido varios problemas relacionados con la llamada a otro punto del contenido en el flujo HLS en el navegador Chrome.

・ **14807**: En el navegador Chrome, si la llamada a otro punto del contenido se activa inmediatamente después de play(), la reproducción puede detenerse con el error DOMException: La solicitud play() fue interrumpida por una llamada ...(Problema de cromo nº 593273).

・ **19085**: Los parámetros de MediaPlayer como volume, abrControlParameters y ccStyle no se establecen como Predeterminados al restablecer el reproductor.

**Problemas corregidos en la versión 2.4.6**

Se ha corregido el siguiente problema en la versión 2.4.6:

・ **18093**: Cuando se utiliza la versión 24 de Flash Player en el modo de reserva de Flash, se devuelven TimedMetadata para la etiqueta situada junto a la etiqueta suscrita.

**Problemas corregidos en la versión 2.4.4**

En la versión 2.4.4 se corrigieron los siguientes problemas:

・ **8711**: Con MSE, los subtítulos 608/708 se dejan justificados de forma predeterminada.

・ **13934**: La configuración de ABR para los anuncios no se aplica cuando se reproduce con transmisiones HLS Live.

・ **14079**: La longevidad de los flujos HLS Live con una ventana baja de DVR puede fallar, ya que la reproducción puede quedar retrasada debido a problemas de latencia de la red. Haga clic en el punto activo para reanudar la reproducción.

・ **15037**: Los ejemplos enviados con la interfaz de usuario del reproductor no funcionan en Microsoft Internet Explorer 10 en Windows 7.

・ **15913**: Para las emisiones de VOD HLS, en Chrome, la emisión no se reproducirá si la respuesta del manifiesto no se modifica como 304. Esto se ha solucionado desde Chrome v55 (problema de Chromium 633696).

・ **16103**: En Android Chrome, en condiciones de ancho de banda bajo, la reproducción puede paralizarse con el TypeError no capturado: No se puede leer la propiedad &quot;programDateTime&quot; de error no definido.

・ **16265**: Para los flujos VOD y en directo de HLS, la búsqueda entre discontinuidades no funciona.

・ **16709**: La reanudación del flujo en directo de HLS con PDT y el marcador de discontinuidad puede provocar que el reproductor se atasque en el almacenamiento en búfer.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

A continuación se mencionan las limitaciones y los problemas conocidos del SDK de explorador.

**Tabla 16: Funciones principales de reproducción**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Reproducción general (reproducción, pausa, llamada a otro punto del contenido)</td> 
   <td><p>・ Los formatos multimedia que no sean HLS no son compatibles.</p> <p>8799: La alternativa de Flash no se ocupa del contenido mixto y, por lo tanto, es necesario asegurarse de que el contenido, los anuncios y otras direcciones URL no conduzcan a contenido mixto (contenido seguro y no seguro juntos).</p> <p>・ 19271: La reproducción de varias utilidades a través de la interfaz de usuario no se admite en el modo de reserva de Flash.</p> <p>・ La alternativa de Flash no funciona en Microsoft Internet Explorer 8 y 9 en Windows 7, ya que estas versiones no son compatibles con el SDK.</p> <p>・ 20262: La reserva de Flash agrega parámetros personalizados a la lista de información de segmentación. También el orden de prioridad de los parámetros personalizados es diferente en el caso de Flash y MSE.</p> <p>・ 20653:La reserva de Flash TVSDK del explorador no funciona en Win10 con la actualización de Creadores.</p> <p>・ Flash Fallback funciona con Flash Player versión 23 y posterior.</p> <p>・ 20087 - Chrome 59 Beta con</p> <p>Flash 25.0.0.171</p> <p>Beta (predeterminado), la reproducción de HLS no funciona en el modo de reserva de Flash. Funciona bien en Canary.</p> </td> 
   <td><p>・ 12563: Las emisiones Dash con códec de audio mp4a.40.02 no se reproducen en Firefox debido a una cadena de códec de audio no compatible en MPD. Se admite el códec de audio mp4a.40.2.</p> <p>15029: Al cambiar entre vídeos en multiView en la interfaz de usuario de Framework, el botón de reproducción/pausa no se actualiza en consecuencia.</p> <p>・ 16034:En Windows 8.1 IE, llamar a reset() genera un error de tipo MIME desconocido. Vuelva a cargar el contenido para reanudar la reproducción.</p> <p>・ 18235: Algunos problemas de búsqueda se observan con los flujos de vod de DASH con anuncios.</p> <p>・ 18727: La API de error no es compatible con MSE</p> <p>18750: Los eventos de cambio de estado pueden estar desordenados en algunos casos tanto para el SDK como para el marco de interfaz de usuario, y en el marco de interfaz de usuario, es posible que falten eventos IDLE e Initialization StatusChange para los oyentes de eventos agregados después de cargar el recurso.</p> <p>・ 18889: Si MediaPlayer está en estado ERROR, no se devuelve el objeto view.</p> <p>・ 19039: Si AdobePSDK. MediaPlayer. seekToLocal() se utiliza con un valor bueno que EOF, entonces la reproducción comienza desde el principio en el caso de MSE.</p> <p>・ 19049: No se notifica ningún estado de error en el Flash Player de Chrome, IE o Firefox cuando el vídeo está bloqueado durante la reproducción.</p> <p>・ 17205: La reproducción de vídeo se detiene durante varias horas mientras se reproduce el audio (problema con Chromium# 664033).</p> <p>・ 12308: Los flujos DASH con composición_ tiempo_offset especificado pueden tener un tiempoStampOffset aplicado en el navegador Chrome que da lugar a una hora de descodificación negativa y, por lo tanto, un error MEDIA_ERR_ SRC_NOT_ SUPPORTED (Problema de Chromium #398141).</p> <p>・ 14126: La reproducción puede paralizarse en Firefox (número de problema 1316024) debido a una brecha interna en el búfer de origen de MSE. Intente buscar para reanudar la reproducción.</p> <p>・ 19115: MS Edge e IE 11 (Win 8.1 y 10) no establece Origin como nulo en el redireccionamiento CORS y, sin embargo, falla porque el encabezado no es nulo y provoca un error de reproducción.</p> <p>・ 19861: Problema con el comportamiento de adición en el búfer de origen para los medios ya reproducidos. Chrome rechaza el fragmento anexado, incluido moov, lo que provoca el siguiente error de descodificación. (Problema de cromo #735335)</p> <p>19921: La reproducción se detiene para cierto contenido HLS aunque su almacenamiento en búfer se haya realizado correctamente (problema de Chromium #713540)</p> <p>・ 20444:La búsqueda del final del rango en búfer en IE y Edge puede causar que la reproducción se detenga.</p> <p>・ 20511: A veces, el rechazo de la búsqueda se puede observar para flujos HLS con o sin anuncios.</p> <p>・ 20743: En Windows 10 Chrome, el flujo en directo de HLS se reproduce durante unos segundos antes de la reproducción previa a la emisión de MP4.</p> <p>・ 21043: Es posible que la dimensión de vídeo no sea correcta durante la carga inicial debido a la falta de metadatos.</p> <p>・ 21115: El gesto del usuario de Android es necesario para iniciar la reproducción si el anuncio previo a la emisión está disponible para vídeos en una lista de reproducción.</p> <p>・ HLS Live no admite el rollover de la marca de tiempo.</p> <p>・ El audio AAC-SSR no es compatible.</p> <p>Los códecs de audio AC3 y AC3 mejorado no son compatibles.</p> <p>・ Para flujos con discontinuidad de marca de tiempo pero sin marcadores de discontinuidad</p> <p>・ La reproducción puede tener problemas y la búsqueda incorrecta debido a los saltos.</p> <p>・ Es posible que la duración del contenido y la duración de la reproducción no coincidan.</p> <p>・ Las interrupciones entre representaciones y representaciones deben coincidir con otras circunstancias, lo que puede provocar problemas de sincronización y paralización.</p> <p>・ Es posible que los subtítulos y WebVTT no aparezcan cerca del final de la emisión.</p> <p>・ Los cambios en el códec de audio no son compatibles con los saltos de marca de tiempo.</p> <p>・ No se admite la inserción de anuncios.</p> <p>・ El modo de truco de reenvío rápido puede provocar un bucle de reproducción en Win 8.1 IE 11 (número de MS 12446268).</p> <p>DASH:</p> <p>・ Para emisiones en directo: se admite el perfil en directo con tipo dinámico.</p> <p>・ Para flujos VoD: se admite el perfil en directo con tipo estático.</p> <p>Para los flujos VoD, el perfil bajo demanda no está certificado para los flujos de trabajo de publicidad.</p> </td> 
   <td><p>・ No se admiten los flujos de DASH Live y DASH Video on Demand.</p> <p>・ La reproducción de vídeo PIP (Picture in Picture) no es compatible con iOS en modo de pantalla completa.</p> <p>En Safari (etiqueta de vídeo), la extensión menos manifiesto sin tener un encabezado de tipo de contenido correcto no funciona.</p> </td> 
   <td><p>・ el applicationID de la aplicación del remitente debe ser el mismo que se generó al registrar la URL del receptor como una aplicación del receptor personalizado.</p> <p>・ El reproductor de referencia está certificado para los flujos de trabajo DASH. El marco de IU no está certificado.</p> <p>Para obtener una lista de los códecs de medios compatibles, consulte <a href="https://developers.google.com/cast/docs/media"><em>here</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Reproducción general (reproducción, pausa, llamada a otro punto del contenido)</td> 
   <td> </td> 
   <td>18098: Algunos problemas de búsqueda se observan con el flujo FER de HLS LBA.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Velocidad de bits adaptable</td> 
   <td><p>・ 20079: Reescritura del búfer en la búsqueda dentro del intervalo de almacenamiento en búfer.</p> <p>20080: El comportamiento del Flash ABR es coherente con el MSE.</p> </td> 
   <td><p>・ La variante de reserva de solo audio en un flujo ABR se ignora debido a limitaciones relacionadas con el búfer.</p> <p>・ 12289: Los parámetros de control ABR no se aplican para audio en el caso de transmisiones HLS/DASH no mezcladas.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Subtítulos 608/708</td> 
   <td> </td> 
   <td><p>・ 7810: En Android 4.4.4, Chrome no parece ser compatible con las familias de fuentes CSS básicas utilizadas por el reproductor y, por lo tanto, la función de cambio de estilo de fuente no funciona.</p> <p>・ Los canales CC no se pueden cambiar en el caso de 608 subtítulos.</p> <p>・ Las funciones de estilo avanzado no son compatibles con los 608 subtítulos.</p> <p>Se admiten subtítulos incrustados (608/708), marcados mediante la etiqueta de accesibilidad.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>・ 5206: El reproductor ignora las etiquetas de región del archivo WebVTT al mostrar los rótulos.</p> <p>・ DASH: Los archivos VTT fragmentados o segmentados no son compatibles.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Failover de manifiesto</td> 
   <td>21056: Con la reserva de Flash, la conmutación por error no se produce para la emisión en directo si la emisión principal devuelve un error 404 durante la reproducción.</td> 
   <td>La conmutación por error de manifiesto solo es aplicable para contenido y no para anuncios.</td> 
   <td>La conmutación por error de la lista de reproducción que falta funciona en Safari solo para el código de error HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Failover avanzado</td> 
   <td> </td> 
   <td><p>・ La conmutación por error de segmento no admite saltos de segmentos no disponibles y reproducción continua.</p> <p>20533: Los segmentos que faltan en una lista de reproducción deben tratarse como una discontinuidad y la reproducción debe reanudarse desde el siguiente segmento disponible.</p> <p>21267: El cambio de flujo debido a un error puede llevar a la descarga de segmentos más antiguos.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Notificaciones de QoS y del reproductor</td> 
   <td>21129: La velocidad de fotogramas no está disponible en caso de Flash de reserva.</td> 
   <td><p>・ 11170:</p> <p>Timed_Event no está disponible para el TVSDK del explorador con MSE, a diferencia del TVSDK del explorador con reserva de Flash.</p> <p>21129: La velocidad de fotogramas no se calcula para emisiones en directo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Compatibilidad con encabezados de cookie</td> 
   <td> </td> 
   <td> </td> 
   <td><p>con el indicador de credenciales y los encabezados de cookies no son compatibles con Safari.</p> <p>21051: Para permitir las cookies en Safari, habilite la configuración "Cookies y datos de sitio web" en Preferencias &gt; Privacidad.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Etiquetas personalizadas</td> 
   <td>14763: No se deben admitir las etiquetas personalizadas que no sean las que empiecen por #. En este momento, el objeto TimedMetadata se crea y se comunica para estas etiquetas durante la reserva de Flash.</td> 
   <td>Los flujos con etiquetas personalizadas dentro de banda no están certificados.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Audio de enlace posterior</td> 
   <td> </td> 
   <td><p>・ La inserción de anuncios no es compatible con los flujos LBA en directo de HLS.</p> <p>・ 17273: Los flujos LBA de VOD HLS cambian a la representación predeterminada en caso de failover y no se pueden volver a seleccionar la última vez que se seleccionó.</p> <p>・ 20251: El flujo de HLS Live LBA puede pararse en la búsqueda.</p> <p>・ 20497: El reproductor permanece en estado de almacenamiento en búfer si los flujos no multados de HLS LBA no tienen fotogramas de audio o vídeo cerca del final del flujo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>302 Redireccionamiento</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>la optimización de redireccionamiento no es compatible con los exploradores windows Edge e IE, ya que no admiten la propiedad responseURL en el objeto XMLHttpRequest .</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 17: Funciones de reproducción avanzadas**

<table> 
 <tbody> 
  <tr> 
   <td>Tipo de contenido</td> 
   <td>Función</td> 
   <td>Flash</td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Reproducción con desplazamiento</td> 
   <td><p>El inicio de la reproducción con un valor de desplazamiento determinado no es compatible con el contenido MP4.</p> </td> 
   <td>20492: Los anuncios intermedios anteriores al desplazamiento se reproducen antes de que el contenido se reanude desde el valor de desplazamiento.</td> 
   <td>iOS no admite la reproducción con la función de desplazamiento.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Reproducción complicada</td> 
   <td>La reproducción continua no funciona para flujos que no tienen representaciones de iFrame.</td> 
   <td><p>・ Las adaptaciones Trick Play no son compatibles con Firefox e Internet Explorer, por lo que el modo de truco inverso no está disponible en estos navegadores.</p> <p>・ La reproducción no está disponible cuando se reproduce contenido junto con anuncios.</p> <p>・ 10435: Durante la reproducción de DASH, el vídeo se bloquea al reproducir el truco de reenvío en Internet Explorer (Win 8.1)</p> <p>de forma intermitente. Esto sucede porque se utiliza la propiedad playRate de los elementos de vídeo sin la adaptación de reproducción de trucos.</p> <p>14182: A veces, durante el rebobinado en el navegador Chrome, es posible que el evento de búsqueda no se reciba y, por lo tanto, el modo de truco no funcionará.</p> <p>・ 14942: Las tasas de reproducción se pueden configurar en Chrome para Android incluso en el caso de emisiones que no sean de reproducción engañosa, pero la configuración no se aplicará y la reproducción continuará a una velocidad normal.</p> <p>・ 17308: La llamada a otro punto del contenido no funciona en el modo de reproducción.</p> <p>・ 17309: En el navegador Chrome, el modo de truco inverso no se puede mantener durante más de 2 segundos.</p> <p>19272: Es posible que la reproducción de trucos no se recupere del almacenamiento en búfer en el explorador Windows 10 Edge en el caso de los flujos DASH.</p> </td> 
   <td>No se admite el modo de truco de rebobinado.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Análisis de ID3</td> 
   <td>20346: El SDK también debe devolver el byte de codificación de texto de los marcos ID3.</td> 
   <td><p>El SDK ignora las etiquetas ID3 disponibles en flujos de transporte de datos de audio (ADTS).</p> <p>・ 12378: Los metadatos temporizados de ID3 se analizan en diferentes momentos en Flash y navegador con compatibilidad con MSE y, por lo tanto, el comportamiento de visualización en la cronología del reproductor de referencia también es diferente.</p> <p>・ 19247: El análisis de ID3 no es compatible con la interfaz de usuario.</p> </td> 
   <td><p>・ 20323: La etiqueta PRIV ID3 utilizada para indicar la marca de tiempo de la primera muestra de un segmento aac no se analiza en Safari (problema de Safari #32422733)</p> <p>・ 20350: En determinados dispositivos (incluido MAC OS X 10.1, iPad10), Safari no proporciona un evento de cambio de señal cuando se encuentra en modo de truco y, por lo tanto, no se reciben fotogramas ID3. (Problema de Safari #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Compatibilidad con el marcador de discontinuidad</td> 
   <td> </td> 
   <td><p>・ La inserción del anuncio del lado del cliente no es compatible con los flujos HLS que contienen discontinuidad.</p> <p>・ No se permite el cambio del códec de audio entre interrupciones en el flujo HLS.</p> <p>・ El interruptor de pista de audio no es compatible con el flujo HLS con marcadores de discontinuidad</p> </td> 
   <td>El número de secuencia de discontinuidad es un requisito para los flujos HLS con discontinuidad para poder reproducirse en Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 18: Funciones de protección de contenido**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>El rango de bytes no es compatible con contenido cifrado AES-128.</td> 
   <td>12324: Los flujos cifrados HLS AES-128 no se reproducen en Safari si no se especifica la etiqueta IV.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>・ 12660: El reproductor HTML5 genera un error interno del servidor para el contenido de guión cifrado PlayReady caducado.</p> <p>・ 16720: El contenido cifrado DASH DRM no funcionará si falta el atributo start en la etiqueta period .</p> <p>・ 18589: La reproducción no es compatible con flujos DRM protegidos Dash VoD Multiperiod con Xlink.</p> <p>・ 18653: La reproducción del contenido multiperiodo Widevine con varias claves se detiene en el primer periodo y no puede cambiar al siguiente periodo.</p> <p>・ 18656: El flujo MultiPeriod de Playready, cifrado con claves diferentes, no se reproducirá.</p> <p>Playready 2.0 para Dash no está certificado.</p> <p> </p> <p> </p> </td> 
   <td>12602: El reproductor HTML5 actualiza repetidamente los metadatos DRM de HLS Fairplay en Safari</td> 
   <td><p>Se puede reproducir el contenido DASH Widevine DRM empaquetado a través de Bento4. El contenido empaquetado a través de Offline Packager y Shaka packager no se reproduce. DASH PlayReady DRM no es compatible.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 19: Funciones principales del Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Pre/Mid/Post</td> 
   <td> </td> 
   <td><p>・ Los anuncios previos con contenido en directo HLS se reproducen en modo de reproductor doble.</p> <p>・ Los anuncios DASH con contenido HLS y los anuncios HLS con contenido DASH no son compatibles.</p> <p>・ 19002: En HTML5 Player con MSE adBreak. insertionType no devuelve el valor correcto para representar el tipo de inserción correcto, es decir, el cliente insertado o el servidor insertado.</p> <p>7794: En dispositivos móviles (iOS, Android con Chrome 33 o un explorador nativo o inferior) en los que la barra de control predeterminada está visible en el modo de pantalla completa, la barra de búsqueda y los botones de reenvío rápido están disponibles cuando Ads Play se reproduce.</p> <p>・ 11048: El cambio de un anuncio a contenido HLS Live no es sencillo en el caso de las extensiones de fuentes de medios.</p> <p>・ 16083: En Android 4.4 Chrome v52, a veces los anuncios HLS con contenido HLS pueden provocar un error de descodificación de la canalización después de una reproducción interrumpida.</p> <p>・ 16097: Los errores encontrados durante la pausa publicitaria no se gestionan, lo que puede hacer que el flujo principal detenga la reproducción.</p> <p>・ 18095: Los anuncios de MP4 no son compatibles con el contenido en directo de HLS.</p> <p>19120: Varias búsquedas en anuncios HLS con contenido HLS pueden hacer que el flujo detenga la reproducción.</p> <p>・ 19131: La superposición de almacenamiento en búfer puede aparecer al cambiar de la pausa publicitaria previa a la emisión a contenido.</p> <p>・ 20296: En el caso de las transmisiones en directo HLS, la búsqueda en la ventana DVR seguida de la búsqueda en las retransmisiones intermedias resueltas puede provocar una interrupción de la reproducción.</p> <p>・ 20298:HLS Transmisiones en directo con rollos medios paran el primer anuncio a mitad de rollo y sale de la ventana DVR.</p> <p>・ 20317: Las transmisiones en directo de HLS pueden paralizarse al cambiar al siguiente anuncio o de un anuncio a otro en caso de que la pausa publicitaria contenga más de un anuncio.</p> 
    <ul> 
     <li>Los anuncios en la ventana DVR de los flujos HLS Live no se resuelven.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>El SDK no respeta el atributo de secuencia dentro de la respuesta VMAP para VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: El SDK no respeta el atributo de secuencia dentro de la respuesta VMAP para VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: No se admite el atributo de repetición VMAP.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Reempaquetado creativo</td> 
   <td> </td> 
   <td>21464: La respuesta de publicidad se descarta por completo si el reempaquetado creativo falla en uno de los anuncios de la pausa publicitaria.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 20: Funciones avanzadas de Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Solo publicidad</td> 
   <td> </td> 
   <td>20056: La propiedad de tecnología del reproductor no es relevante, ya que se basa en el contenido principal que está vacío en el caso de la reproducción de Solo publicidad</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Política de publicidad personalizada</td> 
   <td> </td> 
   <td><p>・ Los comportamientos de los anuncios no son compatibles con los anuncios en MP4 y el contenido en MP4.</p> <p>・ 13973: Comportamientos de publicidad personalizados : la directiva SKIP no genera un evento completo cuando se utiliza con MSE.</p> <p>・ 14939: Las políticas de comportamiento publicitario personalizadas omiten y omiten las pausas publicitarias no funcionan para el contenido de DASH.</p> <p>・ 17131: El primer fotograma del anuncio está visible y, a continuación, el contenido se reanuda en caso de omitir la directiva de pausa publicitaria.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Anuncios/anuncios tipo titular/anuncios en los que se puede hacer clic</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Los anuncios de tipo titular no están visibles al utilizar un reproductor de referencia.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ Los comportamientos de los anuncios no son compatibles con los anuncios VPAID.</p> <p>・ 15032: Los anuncios VPAID en combinación con anuncios MP4 o HLS en una pausa publicitaria no son compatibles.</p> <p>・ 19001: En Android y iOS cuando el anuncio VPAID se reproduce con MP4 como contenido principal, se pueden auditar dos pistas de audio, una de contenido principal y otra de anuncio.</p> <p>・ 20762: Los anuncios VPAID no son compatibles con Imagen en imagen (PIP).</p> <p>・ 21172: El evento de finalización de reproducción no se recibe para el contenido de VOD de HLS con anuncios VPAID.</p> <p>・ 21173: No se recibe onAdBreakCompleteEvent para el contenido de VOD de HLS ni para los anuncios VPAID de anuncio.</p> </td> 
   <td>El reproductor cambia entre el modo normal y el modo de pantalla completa al cambiar entre VPAID y el contenido principal.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 21: Integraciones**

| **Tipo de contenido** | **Función** | **Flash** | **HTML5 en Firefox, IE, Chrome, Android Chrome** | **HTML 5 en Safari, iOS Safari** | **Chromecast (solo reproducción de DASH)** |
|---|---|---|---|---|---|
| VOD + Activo | Integración de VHL de Adobe Analytics |  | 19004: El seguimiento de Video Analytics no está disponible a través de la herramienta de configuración de la interfaz de usuario. |  |  |

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Información y asistencia de Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
