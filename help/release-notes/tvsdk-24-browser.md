---
title: Notas de la versión del explorador TVSDK 2.4
seo-title: Notas de la versión del explorador TVSDK 2.4
description: Las notas de la versión del explorador TVSDK 2.4 describen las nuevas funciones admitidas y no admitidas, así como los problemas conocidos en el explorador TVSDK 2.4.
seo-description: Las notas de la versión del explorador TVSDK 2.4 describen las nuevas funciones admitidas y no admitidas, así como los problemas conocidos en el explorador TVSDK 2.4.
uuid: 3a1eb1a5-0e72-4658-beeb-bca8816570e7
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: d71886cb-f34b-47b2-9df7-168686478106
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Notas de la versión del explorador TVSDK 2.4 {#browser-tvsdk-release-notes}

Las notas de la versión del explorador TVSDK 2.4 describen las nuevas funciones admitidas y no admitidas, así como los problemas conocidos en el explorador TVSDK 2.4.

## Introducción {#introduction}

TVSDK de explorador es un juego de herramientas que le permite agregar funcionalidad avanzada de reproducción de vídeo, protección de contenido y publicidad a sus aplicaciones de reproductor de vídeo basadas en explorador.

El explorador TVSDK 2.4 proporciona API de JavaScript para crear aplicaciones de vídeo basadas en explorador e incluye compatibilidad con la reproducción en los modos siguientes:

* Solo HTML5
* HTML5 con reserva de flash automático
* Flash siempre

Esta versión incluye la siguiente información:

・ Documentación [de la API TVSDK del explorador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ Guía [de programación TVSDK del explorador](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ Guía [de migración de](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)TVSDK para 1.4 DHLS a Browser TVSDK 2.4.

・ [Conversión de Browser TVSDK 2.4.6 a la versión 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ Una implementación de referencia, que se incluye en la compilación.

>[!NOTE]
>
>*Para obtener una lista completa de las consideraciones de seguridad de esta versión, consulte Consideraciones de seguridad.

## Novedades y funciones compatibles {#what-s-new-and-supported-features}

Esta versión de TVSDK de explorador proporciona nuevas funciones que puede utilizar para mejorar las aplicaciones de vídeo.

**Nuevo en la actualización 2.4.12 (compilación 204)**

La siguiente adición está disponible como parte de la actualización TVSDK 2.4.12 del explorador (compilación 204):

* Se ha cambiado la implementación de la API de volumen de AdobePSDK.MediaPlayer para permitir la reproducción automática en iOS cuando la reproducción está silenciada.

・ Se agrega una nueva API `auditudeSettings.ignoreVPAIDAds`para permitir ignorar las publicidades VPAID recibidas del servidor de Auditude. La API no funciona para Flash Fallback.

**Versión 2.4.11**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.11 del TVSDK del explorador:

・ El failover de segmentos HLS Live es compatible con los modos de reserva MSE y Flash.

・ Ya está disponible la compatibilidad con `AuditudeSettings.creativeRepackagingDomain` API para MSE. Anteriormente solo se admitía con el modo de reserva Flash.

・ La versión contiene correcciones para problemas críticos con los clientes. Consulte *Problemas solucionados* en una lista.

**Versión 2.4.10**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.10 del TVSDK del explorador:

・ TVSDK proporciona enableLogging() para habilitar o deshabilitar el registro. Consulte la documentación de la [API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)para obtener información sobre su uso.

・ TVSDK ya no admite los capítulos predeterminados al usar Adobe Analytics. Defina y administre capítulos con su aplicación.

・ La versión contiene correcciones para problemas críticos con los clientes. Consulte *Problemas solucionados *una lista.

**Versión 2.4.9**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.9 del TVSDK del explorador:

・ Los flujos HLS VOD y Live con discontinuidad horaria pero sin marcadores de discontinuidad son compatibles.

・ Los fotogramas ID3 v2.4.0 son compatibles con la etiqueta de vídeo Safari para los flujos HLS VOD y Live.

・ La implementación de carga de publicidad segura garantiza que las llamadas al servidor de publicidad se actualicen para proteger HTTP según la configuración de la API. Para obtener más información, consulte las clases AdobePSDK.AdvertisingMetadata y AdobePSDK.ForceHttpsAdConfiguration. Esta función no se admite en el modo de reserva de Flash.

・ TVSDK pone a disposición de la aplicación la información del ID de anuncio y la información de extensión asociada con las respuestas de VAST 3.0, que se pueden utilizar para implementar la integración de Moat para las mediciones de anuncios. Para obtener más información, consulte la API AdobePSDK.NetworkAdInfo. Esto no se admite en el modo de reserva de Flash.

・ La clase AdobePSDK.ForceHttpsConfiguration ya no está disponible. Su éxito es

Clase AdobePSDK.ForceHttpsAdConfiguration.

・ Ahora hay disponible una nueva API, AdobePSDK.optimizedFlashCalls, para optimizar las llamadas y mejorar la experiencia de reproducción de HLS en el modo de reserva de Flash. Esta opción está deshabilitada de forma predeterminada.

**Novedades de la actualización 2.4.8 (compilación 6002)**

Esta actualización contiene correcciones para problemas críticos con los clientes. Consulte Problemas ** fijos para obtener la lista.

**Versión 2.4.8**

Las siguientes mejoras y adiciones están disponibles como parte de la versión 2.4.8 del TVSDK del explorador:

・ El SDK ahora es compatible con Chrome EME y los cambios de prácticas recomendadas disponibles a partir de Chrome v58. Para obtener más información, consulte [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ El marco de interfaz de usuario ahora admite DRM de acceso HLS en Flash, solo publicidad y flujo de trabajo de información de objetivo.

・ La API setDRMAuthenticateData se agrega al marco de interfaz de usuario. Para reproducir flujos protegidos con DRM de Adobe Access, invoque esta API. También se puede especificar el atributo drmAuthenticateData en el reproductor. Consulte [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)para obtener más información.

**Versión 2.4.7**

Las siguientes funciones son nuevas en la versión 2.4.7:

・ Adición del configurador de la interfaz de usuario en el marco de la interfaz de usuario

Puede configurar el reproductor de una de las siguientes maneras:

・ Uso de un objeto JSON

・ Uso de API

Para ayudar a generar el objeto JSON, el SDK de TVSDK del explorador proporciona una herramienta **UI Configurator **Tool.

En esta herramienta, puede seleccionar varios ajustes, hacer clic en **Probar configuración **para comprobar los ajustes y hacer clic en **Descargar configuración **para descargar los ajustes. Después de descargar el archivo, puede pasar el contenido de este archivo como objeto JSON a la API ptp.videoPlayer.

・ Adición de la API MediaPlayerItemConfig al marco de interfaz de usuario

Diversas funciones, incluyendo publicidadMetadata, publicidadFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscripTags, adTags, thumbnailScrubber, facturaciónMetricsConfiguration, se pueden configurar mediante MediaPlayerItemConfig. Para obtener más información, consulte la documentación de AdobePSDK.MediaPlayerItemConfig en la [documentación de la API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * de TVSDK del explorador [](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

En la interfaz de usuario, se ha modificado la forma de pasar configuraciones de red a través de la configuración del reproductor.

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

* Compatibilidad con flujos de trabajo de DRM y Analytics en el marco de interfaz de usuario

Las configuraciones de DRM y el seguimiento de Analytics se pueden habilitar a través de la interfaz de usuario.

* Adición de la `AdobePSDK.embedSWFinFullScreenDiv` API

Esta nueva API proporciona flexibilidad a la aplicación del reproductor para seleccionar el div en el que puede incrustar el archivo FlashFallback.swf.

* Se ha sustituido `getVersion`la API de la `AdobePSDK.MediaPlayer` clase por `AdobePSDK.Version` la clase para la información relacionada con la versión de TVSDK. Para obtener más información, consulte `AdobePSDK.Version` API [aquí](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versión 2.4.6**

Las siguientes funciones son nuevas en la versión 2.4.6:

* **Compatibilidad con la exploración**

Browserify le permite utilizar los módulos de estilo node.js en el explorador. Puede definir las dependencias y Examinar agrupa todo en un archivo JavaScript.

* **Facturación**

Con la ayuda de la facturación, el SDK de TVSDK del explorador puede recopilar métricas de uso del reproductor para facturar a los clientes de Primetime.

>[!NOTE]
>
>La enumeración desaprobada MediaPlayer.Events y las constantes desaprobadas en Enum PSDKErrorCode se han eliminado en la versión 2.4.6. Para obtener más información, consulte [Conversión de Browser TVSDK 2.4.5 a la versión 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versión 2.4.5**

Las siguientes funciones son nuevas en la versión 2.4.5:

* **Revistas completas de eventos y publicidades**

   Los flujos de reproducción de eventos completos (FER) de HLS ahora admiten la resolución de anuncios y los comportamientos publicitarios. Para habilitar esta compatibilidad, establezca el modo de señalización de publicidad en `MANIFEST_CUES` al crear el `MediaPlayerItemConfig` objeto.

* **Compatibilidad con la directiva de escala de MediaPlayerView**

   Los desarrolladores de aplicaciones ahora pueden especificar una scalePolicy diferente para la vista mediante la propiedad scalePolicy de MediaPlayerView.

* **Compatibilidad con contenido anamórfico**

   Ahora se admite la reproducción de contenido anamórfico al utilizar la reproducción de MSE y Flash.

* **Aplicación selectiva de`withCredentials`**

Cuando `withCredentials` se establece en true, el `Access-Control-Allow-Origin` encabezado no se puede establecer en comodines. Según la respuesta del servidor, el TVSDK del explorador establecerá el `withCredentials` atributo de forma selectiva. Para obtener más información sobre esta compatibilidad, consulte Documentos [de API de TVSDK de explorador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versión 2.4.4**

Las siguientes funciones fueron nuevas en la versión 2.4.4:

* **Aplicación de ejemplo de Chromecast**

Esta versión es compatible con una aplicación de remitente y receptor que muestra la reproducción de flujos VOD DASH y flujos Widevine DASH con inserción de anuncios en el lado del cliente.

* **Compatibilidad con failover avanzado**

Esta versión contiene compatibilidad con casos avanzados de uso de failover (failover de segmentos y servidores) para flujos HLS VOD.

**Versión 2.4.3**

Las siguientes funciones fueron nuevas en la versión 2.4.3:

* **Etiquetas personalizadas para DASH VOD**

   Las etiquetas personalizadas en línea (eventos) se pueden suscribir y recibir como objeto TimedMetadata.

* **Reproducción de flujos sin extensiones**

   Ahora se admiten los flujos HLS y DASH sin extensiones. Para el archivo de manifiesto, debe especificarse resourceType al cargar el recurso. Para segmentos y archivos VTT, el encabezado de respuesta Content-Type se utiliza para determinar el tipo de contenido.

**Versión 2.4.2**

Las siguientes funciones fueron nuevas en la versión 2.4.2:

* **Paridad de API**

Para obtener una lista completa de la paridad de API, consulte la Guía [](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)de migración TVSDK para 1.4 DHLS al explorador TVSDK 2.4.

* **Compatibilidad con AES de muestra**

   Esta versión incorpora compatibilidad con la reproducción de contenido cifrado Sample-AES en MSE y Flash fallback. Se ha eliminado el requisito de alojar contenido AES sobre el origen seguro en Google Chrome.

* **Compatibilidad con contenedores AAC**

   Ahora se admite la reproducción de archivos con la extensión .aac. Pueden ser flujos de solo audio o audio alternativo.

   >[!NOTE]
   >
   >Los códecs AC3 y AC3 mejorados aún no son compatibles.

* **Reproducción de flujo con token**

Los flujos HLS que se envían a través de una red de entrega de contenido (CDN) pueden utilizar a veces tokens de autenticación en las solicitudes de manifiesto y segmento para la verificación, y estos tokens pueden proporcionarse como parámetros de URL o como encabezados de cookie. Ahora se admite la reproducción de estos flujos.

**Versión 2.4.1**

Las siguientes funciones fueron nuevas en la versión 2.4.1:

* **Marco de la interfaz de usuario**

Este marco de trabajo, diseñado para acelerar el desarrollo de la interfaz de usuario para aplicaciones de reproductor de vídeo basadas en JavaScript, consta de API para incluir controles básicos como reproducir/pausa y volumen y para agregar o eliminar fácilmente elementos como estados de barra de desplazamiento y ajustes de subtítulos opcionales. Puede especificar el comportamiento asociado con los controles, crear controles personalizados y aplicar máscara a la interfaz de usuario del reproductor. Todo esto ocurre a través del marco de trabajo, sin necesidad de manipular directamente la estructura DOM.

* **Mejoras de reproducción HLS para flujos en directo**

Esta versión admite las interrupciones causadas por la inserción de anuncios. Utiliza la etiqueta EXT-PROGRAM-DATE-TIME seguida de la etiqueta EXT-MEDIA-SEQUENCE para sincronizar entre perfiles de velocidad de bits adaptables para una reproducción suave.

* **Compatibilidad con VPAID 2.0**

La versión 2.0 de la definición de interfaz de servicio de publicidad (VPAID) del reproductor de vídeo proporciona una experiencia multimedia rica para los usuarios y permite a los editores dirigir mejor los anuncios, rastrear las impresiones de publicidad y monetizar el contenido de vídeo. Esta versión admite anuncios VPAID de JavaScript lineales para contenido de vídeo a petición (VOD).

* **Etiquetas HLS personalizadas**

Los flujos de medios pueden incluir metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto. El SDK del explorador le permite especificar y suscribirse a etiquetas adicionales y recibir notificaciones cuando dichas etiquetas aparezcan en el manifiesto.

* **Marcadores de publicidad mostrados en la línea de tiempo del reproductor**

Esta versión admite la visualización de marcadores de publicidad en la línea de tiempo del reproductor tanto para contenido VOD como activo. Puede ver este comportamiento en el reproductor de referencia.

**Compatible con 2.4**

Las siguientes funciones estaban disponibles en la versión 2.4:

* **Reproducción de audio MP3**

   Esta versión admite la reproducción de audio MP3 en navegadores con Media Source Extensions (MSE) y con la etiqueta de vídeo Safari.

* **Reproducción de vídeo MP4**

   Se admiten las siguientes funciones:

   * Reproducción de un solo flujo
   * Anuncios anteriores y posteriores a la publicación de MP4 con comportamientos y seguimiento de anuncios
   * Anuncio previo y posterior de anuncios HLS con comportamientos y seguimiento de anuncios
   * Anuncio previo y posterior de DASH con comportamientos y seguimiento de anuncios

## Plataformas admitidas {#supported-platforms}

El TVSDK del explorador tiene requisitos específicos para los niveles de plataformas y software en los que debe ejecutarse. Se admiten las siguientes plataformas y niveles de software:

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

   * Navegador nativo
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

**Google Chromecast (segunda generación; solo para la reproducción de DASH)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Tecnología</strong> </p> </td> 
   <td><p><strong>Etiqueta</strong><sup>de vídeo TVSDK del explorador 1</sup></p> </td> 
   <td><p><strong>Explorador TVSDK MSE</strong></p> </td> 
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

Esta es una lista de las funciones compatibles y no compatibles de esta versión:

* *Características de audio MP3: Reproducción principal*
* *Características de vídeo MP4: Reproducción principal*
* *Características de vídeo MP4: Inserción de anuncios principales*

>[!NOTE]
>
>*En las tablas de matriz de funciones que se muestran a continuación, una &#39;Y&#39; significa que la función es compatible con la versión actual.*

### Funciones de audio MP3 {#mp-audio-features}

**Tabla 1: Reproducción principal{#table-core-playback}**

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | MP3 VOD | Reproducción general (Reproducir, Pausa, Buscar) | No admitido | Y | Y |

1 La etiqueta de vídeo TVSDK del explorador no admite flujo continuo ni DRM. La compatibilidad con el códec y el contenedor no es la misma en todos los exploradores.

2 Firefox utiliza Flash Player de forma predeterminada para la versión 41 o anterior.

### Funciones de audio MP4 {#mp-audio-features-1}

**Tabla 2: Reproducción principal**

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD MP4 | Reproducción general (Reproducir, Pausa, Buscar) | No admitido | Y | Y |

**Tabla 4: Inserción de anuncios principales**

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Inserción de publicidad | VOD MP4 | Anteposición (MP4) | No admitido | Y | Y |
| Inserción de publicidad | VOD MP4 | Post-roll (MP4) | No admitido | Y | Y |

Para obtener más información sobre la compatibilidad con funciones HLS o DASH, consulte a continuación.

## Matriz de funciones HLS {#hls-feature-matrix}

Esta es la matriz de características de las funciones HLS en el SDK de TVSDK de explorador.

* *Reproducción de HLS Core*
* *Funciones de reproducción avanzadas de HLS*
* *Funciones de protección de contenido HLS*
* *Funciones de inserción de anuncios principales de HLS*
* *HLS Funciones avanzadas de inserción de anuncios*
* *Integraciones HLS*

>[!NOTE]
>
>*En las tablas de matriz de funciones que se muestran a continuación, una &#39;Y&#39; significa que la función es compatible con la versión actual.*

### Funciones de HLS {#hls-features}

Se admiten las siguientes funciones:

**Tabla 4: Reproducción de HLS Core**

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
   <td><p>Reproducción general (reproducir, pausa, buscar)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Reproducción general (reproducir, pausar y buscar)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Velocidad de bits adaptable</p> </td> 
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
   <td><p>Conmutación por error de manifiesto</p> </td> 
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
   <td><p>Notificaciones de QoS y reproductor</p> </td> 
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
   <td>Enlace tardío de audio</td> 
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
   <td><p>Reproducción en desplazamiento</p> </td> 
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
   <td><p>Reproducción de trucos</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción suave de trucos</p> </td> 
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
   <td><p>Compatibilidad con los marcadores de discontinuidad</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Flujos con autentificación</p> </td> 
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
   <td><p>Protección del contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección del contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección del contenido</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe Access</p> </td> 
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
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Anteponer (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Mid-roll (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Resolución y comportamientos de publicidad</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Directiva de publicidad predeterminada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
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
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo publicidad</p> </td> 
   <td><p>No admitido</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Parámetros de objetivo</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Parámetros personalizados</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Directiva de publicidad personalizada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Carga de anuncios diferida</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>No admitido</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Publicidades complementarias, publicidades tipo titular, publicidades en las que se puede hacer clic</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 9: Integraciones HLS{#table-hls-integrations}**

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
   <td><p>Integración VHL de Adobe Analytics</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Tabla de características de DASH {#dash-feature-matrix}

Esta es la matriz de características de las funciones de DASH en el SDK de TVSDK de explorador.

・ Funciones de reproducción *DASH Core*

・ *Funciones de reproducción avanzadas de DASH*

・ *Funciones de protección de contenido de DASH*

・ Funciones de inserción de anuncios *de DASH Core*

・ *DASH Funciones avanzadas de inserción de anuncios*

・ Integraciones *DASH*

>[!NOTE]
>
>En las tablas de matriz de funciones que se muestran a continuación, una Y significa que la función es compatible con la versión actual.

### Características del DASH {#dash-features}

Se admiten las siguientes funciones:

**Cuadro 10: Funciones de reproducción de DASH Core**

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
   <td><p>Reproducción general (reproducir, pausa, buscar)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Reproducción general (reproducir, pausar y buscar)</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Velocidad de bits adaptable</p> </td> 
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
   <td><p>Conmutación por error</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Notificaciones de QoS y reproductor</p> </td> 
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

**Cuadro 11: Funciones de reproducción avanzadas de DASH**

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
   <td><p>Reproducción en desplazamiento</p> </td> 
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
   <td><p>Juego de trucos</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción suave de trucos</p> </td> 
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
   <td><p>Flujos con autentificación</p> </td> 
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

**Cuadro 12: Funciones de protección de contenido DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección del contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección del contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección del contenido</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Widevine on Chrome, Firefox 47 y posterior, y Chromecast</p> <p>・ PlayReady en Internet Explorer en Windows 8.1 y Edge</p> <p>・ Primetime DRM para Windows Firefox (solo vídeo)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 13: Funciones de inserción de anuncios de DASH Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Anteposición (MP4/DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Resolución y comportamientos de publicidad</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Directiva de publicidad predeterminada</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Reempaquetado creativo (MP4 a DASH)</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 14: Funciones avanzadas de inserción de anuncios de DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo publicidad</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parámetros de objetivo</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parámetros personalizados</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Directiva de publicidad personalizada</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Carga de anuncios diferida</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Publicidades complementarias, publicidades tipo titular, publicidades en las que se puede hacer clic</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserción de publicidad</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>No admitido</p> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 15: Integraciones de DASH**

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
   <td><p>Integración VHL de Adobe Analytics</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemas solucionados {#issues-fixed}

**Problemas solucionados en la actualización 2.4.12 (compilación 204)**

Los siguientes problemas se han corregido en la actualización de la versión 2.4.12 del TVSDK del explorador (compilación 204):

・ **21647**- TVSDK debe permitir la reproducción automática de vídeo en dispositivos iOS cuando el audio está silenciado.

・ **21465**- Se recibe el acceso denegado al sistema de claves de error al reproducir un flujo DASH protegido por DRM después de reproducir un flujo en directo DASH.

・ **21442**: habilite la reproducción automática del contenido en la Web de iOS después de que la publicidad previa se reproduzca con un gesto del usuario.

・ **21240**: API proporcionada para filtrar anuncios VPAID analizados desde Auditude/VMAP.

**Problemas solucionados en la versión 2.4.11**

Los siguientes problemas se han solucionado en la versión 2.4.11 del SDK de TVSDK de explorador:

**Funciones principales de reproducción:**

・ **19192**: TVSDK ahora implementa TextFormat:bottomInset y TextFormat:safeArea. Debido a estas mejoras, los subtítulos opcionales se pueden volver a colocar si se muestra la barra de control en la pantalla.

・ **21009**: Los subtítulos cerrados persisten en la pantalla en caso de búsqueda en caso de discontinuidad hasta que aparecen nuevos subtítulos.

・ **21141**: La búsqueda hacia atrás se rechaza debido a una condición de carrera durante la adición de segmentos.

・ **21142**: Disponibilidad de rangos de reproducción que se pueden buscar cuando el reproductor está en estado INITIALIZADO. Debido a estos cambios, la sesión de inicio en la posición ahora es compatible.

・ **21363**: Los subtítulos opcionales 608/708 se están desincronizando después de insertarlos en los flujos DASH.

**Funciones de inserción de publicidad:**

・ **21179**: Los problemas relacionados con el desplazamiento medio (pausas largas, marcos negros) con contenido de VOD ahora se resuelven correctamente estableciendo la propiedad ad.parentAsset.adParameters.

・ **21257**: El archivo MP4 con la velocidad de bits más alta se selecciona para la transcodificación si MP4 no es un tipo de MIME válido y la función de reempaquetado creativo está activada.

・ **21361**: TVSDK ahora pasa el sistema de publicidad y el ID creativo de la respuesta VAST como parámetros de consulta en la solicitud de paquete creativo para admitir reglas de normalización adicionales.

**Problemas solucionados en la versión 2.4.10**

Los siguientes problemas se han solucionado en la versión 2.4.11 del SDK de TVSDK de explorador:

**Funciones principales de reproducción:**

・ **21060**: Error de códec no válido generado con flujos HLS que contienen discontinuidad y los cuadros ISO BMFF se ejecutan al final del flujo.

・ **21045**: La reproducción automática no funciona en iOS después de completar la primera reproducción de vídeo en una lista de reproducción.

・ **20975**: El proveedor de QoS devuelve la velocidad de fotogramas como NaN en el navegador Chrome.

・ **20823**: Se ha producido un error de códec no admitido en los segmentos que no tienen datos.

・ **20769**: El SDK ahora comienza con la velocidad de bits actual en la búsqueda en lugar de cambiar inmediatamente según la directiva ABR.

・ **20031**: Cuando se encuentra en modo vertical en IE11 (Windows 8.1), la pantalla de vídeo es pequeña. Función de protección de contenido:

・ **19316**: Omita los segmentos que no se pueden descifrar en caso de flujos HLS AES-128.

**Problemas solucionados en la versión 2.4.9**

Los siguientes problemas se han corregido en la versión 2.4.9 de TVSDK de explorador:

**Funciones principales de reproducción:**

・ **13407**: Los flujos DASH pueden paralizarse si Firefox deja de enviar el evento &quot;ontimeupdate&quot; durante la reproducción.

・ **16380**: Durante la reproducción de contenido de vídeo de audio mixto de segmentos que tienen tiempos de inicio no coincidentes mediante MSE, el error de sincronización de audio entre representaciones se acumula en los conmutadores ABR, lo que resulta en un error (problema de cromo nº 663686).

・ **17985**: Al reproducir un flujo ISO-BMFF concreto en el navegador Firefox, la reproducción se bloquea (número de Firefox 1342913). Esto se ha solucionado desde Firefox v53.

・ **19141**: ReferenceError (en promesa) no capturado: la anchura no está definida.

・ **1897, 1929**: Problema de parpadeo de vídeo en el límite del segmento. Esto ocurría porque el SDK no calculaba correctamente el desplazamiento de tiempo de composición de la última muestra.

・ **19780**: La reproducción no se inicia para el contenido HLS y el anuncio HLS en Firefox v53 (número de Firefox 354653).

・ **20046**: La fecha y hora del programa se recibe como clave en lugar de valor cuando se recibe como objeto de metadatos temporizados.

・ **20047**: useDefaultResizeHandler genera un error con Flash fallback.

・ **20179**: Flash fallback no funciona con Flash Player v25.0.0.171.

・ **20293**: Firefox deja de almacenar datos en búfer para determinados flujos HLS que llevan a la paralización.

・ **20626**: El reproductor genera un error de descodificación de medios en Chrome debido a un manejo incorrecto de muestras de vídeo con duración cero.

・ **20078**: La reproducción se detiene en el error de explorador &#39;CuotaExceeded&#39;.

・ **18639**: En el flujo en directo HLS 608 CC, el texto aparece en ocasiones como mal escrito.

・ **20028**: El parámetro de tamaño ClosedCaptions no cambia el tamaño de fuente.

・ **20613**: Los cuadros de subtítulos cerrados se superponen entre sí, lo que los hace ilegibles.

**Funciones de inserción de anuncios principales (CSAI):**

・ **20043**: Falta la impresión de publicidad y las llamadas de seguimiento de publicidad con varias publicidades y redirecciones de terceros.

・ **20044**: Al utilizar reempaquetado creativo, todas las publicidades de la pausa publicitaria deben volver a empaquetarse correctamente; de lo contrario, la pausa publicitaria se descarta por completo.

・ **20097**: La reproducción del anuncio se omite y el contenido principal se reanuda inmediatamente en lugar de esperar un tiempo de espera de 20 segundos si el manifiesto del anuncio no está disponible.

**Problemas solucionados en la actualización de la versión 2.4.8 (compilación 6002)**

Los siguientes problemas se han corregido en la actualización de la versión 2.4.8 de TVSDK del explorador (compilación 6002):

・ **14126:** La reproducción puede bloquearse en Firefox (problema nº 1316024) debido a un espacio interno en el búfer de origen de MSE. Intente buscar para reanudar la reproducción

・ **19608:** Corrección para respetar el valor de desplazamiento de tiempo de la respuesta VMAP de Auditude.

・ **19635:** Corrige la detención de vídeo en Internet Explorer 11 en Windows 10.

・ **19761:** Correcciones de problemas de ABR con HLS.

・ **19780:** Corrige la reproducción del anuncio con contenido HLS dañado en Mozilla Firefox v53.

・ **1987 y 1974:** Los problemas corrigen la incoherencia al seleccionar la velocidad de bits después de una operación de búsqueda. Ahora, la selección de velocidad de bits en la búsqueda es el valor inferior de la velocidad de bits actual y la velocidad de bits en el inicio.

・ **1981:** La reproducción atascada y la superposición de almacenamiento en búfer aparece durante un tiempo infinito después de realizar la búsqueda durante 3 o 4 veces.

・ **1984:** Confirme la compatibilidad con los requisitos de Chrome 59 Beta Verified Media Path (VMP). bTVSDK pudo reproducir contenido de DRM Widevine con Chrome 59 Beta.

・ **19916:** Se ha interrumpido la reproducción de DRM en la interfaz de usuario y el módulo. Ahora invoca a acquisitionLicense incluso si no hay ninguna política en los metadatos.

**Problemas solucionados en la versión 2.4.8**

Los siguientes problemas se han corregido en la versión 2.4.8 del TVSDK del explorador:

・ **10075**: Al buscar antes de la línea de tiempo, el evento play complete no se recibía en Firefox y Chrome y el evento search no se recibía en Firefox.

・ **15775**: Reproducir evento completo no recibido en Windows 8.1 Internet Explorer.

・ **17306**: Para flujos SSAI, se admite la reproducción. No se admite el seguimiento de la publicidad vinculada.

・ **19142**: A veces, rebobinar hace que el reproductor de vídeo permanezca en estado de almacenamiento en búfer para siempre.

・ **19218**: Los marcadores de publicidad no están disponibles a través de la interfaz de usuario.

・ **19219**: La reproducción solo de anuncios no funciona a través del marco de la interfaz de usuario.

・ **1922**: La clave AES-128 se solicita una vez para una lista de reproducción y las solicitudes posteriores se envían desde la caché. Anteriormente se solicitaba para cada segmento.

・ **19597**: &quot;Error TypeError no capturado: No se puede leer la propiedad &quot;log&quot; de &quot;undefined&quot; con las compilaciones canarias de Chrome.

・ **19605**: adRequestDomain no estaba disponible en el modo Flash de reserva.

・ **19608**: Las publicidades VMAP no se insertaban en los flujos HLS Live. Ahora, el SDK tiene en cuenta los marcadores de señal y no depende de los valores de desplazamiento de tiempo en las respuestas de VMAP.

・ **19637**: La reproducción de publicidades solamente produce un error de secuencia de comandos al final del anuncio.

・ **19732**: Las solicitudes de lista de reproducción CRS fallaban con el error 404. Las solicitudes 1401 y 1403 del Explorador TVSDK ahora se actualizan para atenderlas.

・ **19762**: acquisitionLicense solía llamarse antes de setAuthenticationToken debido a la cual se devolvía una licencia válida independientemente de la validez del token. Esto se ha solucionado ahora y se llama a acquisitionLicense solo después de la respuesta setAuthenticationToken.

**Problemas solucionados en la versión 2.4.7**

En la versión 2.4.7 se corrigieron los siguientes problemas:

・ **8397**: Es posible que los flujos HLS Live generados a través de Adobe Media Server no se reproduzcan si los segmentos no comienzan con un fotograma clave.

・ **13606**: Se han corregido varios problemas relacionados con la búsqueda para el flujo HLS en el navegador Chrome.

・ **14807**: En el navegador Chrome, si la búsqueda o la pausa se activan inmediatamente después de play(), la reproducción puede detenerse con el error DOMException: La solicitud play() fue interrumpida por una llamada...(Problema de cromo nº 593273).

・ **19085**: Los parámetros de MediaPlayer, como volumen, abrControlParameters y ccStyle, no se establecen en Predeterminados al restablecer el reproductor.

**Problemas solucionados en la versión 2.4.6**

Se ha solucionado el siguiente problema en la versión 2.4.6:

・ **18093**: Los metadatos temporales de la etiqueta situada junto a la etiqueta suscrita se devuelven cuando se utiliza Flash Player versión 24 en el modo de reserva de Flash.

**Problemas solucionados en la versión 2.4.4**

En la versión 2.4.4 se corrigieron los siguientes problemas:

・ **8711**: Con MSE, los subtítulos 608/708 se dejan justificados de forma predeterminada.

・ **13934**: La configuración de ABR para anuncios no se aplica al reproducir con flujos HLS Live.

・ **14079**: La longevidad de los flujos HLS Live con una ventana DVR baja puede fallar, ya que la reproducción puede quedar retrasada debido a problemas de latencia de la red. Haga clic en el punto activo para reanudar la reproducción.

・ **15037**: Los ejemplos enviados con la interfaz de usuario del reproductor no funcionan en Microsoft Internet Explorer 10 en Windows 7.

・ **15913**: En los flujos VOD HLS, en Chrome, el flujo no se reproducirá si la respuesta de manifiesto no se modifica como 304. Esto se ha solucionado desde Chrome v55 (problema de cromo 633696).

・ **16103**: En Android Chrome, en condiciones de ancho de banda bajo, la reproducción puede paralizarse con el error TypeError sin capturar: No se puede leer la propiedad &#39;programDateTime&#39; de error no definido.

・ **16265**: Para los flujos HLS VOD y Live, la búsqueda entre discontinuidades no funciona.

・ **16709**: La reanudación del flujo en directo de HLS con PDT y el marcador de discontinuidad puede provocar que el reproductor se quede atascado en el almacenamiento en búfer.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

A continuación se mencionan las limitaciones y los problemas conocidos del SDK de TVSDK de explorador.

**Cuadro 16: Funciones principales de reproducción**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Reproducción general (Reproducir, Pausa, Buscar)</td> 
   <td><p>・ Los formatos de medios que no sean HLS no son compatibles.</p> <p>8799: La alternativa Flash no se ocupa de los contenidos mixtos y, por lo tanto, es necesario asegurarse de que Contenido, Publicidad y otras direcciones URL no conduzcan a contenidos mixtos (contenido seguro y no seguro juntos).</p> <p>・ 19271: La reproducción de varias visualizaciones mediante el marco de interfaz de usuario no se admite en el modo de reserva de Flash.</p> <p>・ Flash fallback no funciona en Microsoft Internet Explorer 8 y 9 en Windows 7 porque estas versiones no son compatibles con el SDK.</p> <p>・ 20262: Flash fallback agrega parámetros personalizados a la lista de información de objetivos. También el orden de prioridad de los parámetros personalizados es diferente en el caso de Flash y MSE.</p> <p>・ 20653:La reserva Flash TVSDK del explorador no funciona en Win10 con la actualización de creadores.</p> <p>・ Flash Fallback funciona con Flash Player versión 23 y posterior.</p> <p>・ 20087 - Chrome 59 Beta con</p> <p>Flash 25.0.0.171</p> <p>Beta (predeterminado), la reproducción de HLS no funciona en el modo Flash Fallback. Está funcionando bien en Canary.</p> </td> 
   <td><p>・ 12563: Los flujos de Dash con códec de audio mp4a.40.02 no se reproducen en Firefox debido a una cadena de códec de audio no compatible en MPD. Se admite el códec de audio mp4a.40.2.</p> <p>15029: Cuando se cambia entre vídeos en multiView en la interfaz de usuario-marco, el botón de reproducción/pausa no se actualiza de forma acorde.</p> <p>・ 16034:En Windows 8.1 IE, llamar a reset() produce un error de tipo MIME desconocido. Vuelva a cargar el medio para reanudar la reproducción.</p> <p>・ 18235: Algunos problemas de búsqueda se observan con los flujos de vod DASH con los anuncios.</p> <p>・ 18727: No se admite la API de error para MSE</p> <p>18750: Los eventos de cambio de estado podrían estar desordenados en algunos casos tanto para el SDK como para el marco de interfaz de usuario, y en el marco de interfaz de usuario, los eventos IDLE e Initializing StatusChange podrían faltar para los oyentes de eventos agregados después de cargar el recurso.</p> <p>・ 18889: Si MediaPlayer está en estado ERROR, no se devuelve el objeto view.</p> <p>・ 19039: Si AdobePSDK. MediaPlayer. searchToLocal() se utiliza con un valor bueno que EOF y, a continuación, la reproducción comienza desde el principio en el caso de MSE.</p> <p>・ 19049: No se notifica ningún estado de error para Flash Player en Chrome, IE o Firefox cuando el vídeo está bloqueado durante la reproducción.</p> <p>・ 17.205: La reproducción de vídeo se detiene durante algunas horas durante la reproducción de un flujo sin muestrear mientras el audio sigue reproduciéndose (problema de cromo nº 664033).</p> <p>・ 12308: Los flujos DASH con composición_time_offset especificada pueden tener una variable timeStampOffset aplicada en el navegador Chrome que da lugar a un tiempo de descodificación negativo y, por lo tanto, un error MEDIA_ERR_ SRC_NOT_ SUPPORTED (problema de cromo #398141).</p> <p>・ 14126: La reproducción puede bloquearse en Firefox (número 1316024) debido a un espacio interno en el búfer de origen de MSE. Intente buscar para reanudar la reproducción.</p> <p>・ 1915: MS Edge e IE 11 (Win 8.1 y 10) no establece Origin en null en la redirección CORS y, sin embargo, falla porque el encabezado no es nulo y provoca un error de reproducción.</p> <p>・ 19861: Problema con el comportamiento de adición en el búfer de origen para medios ya reproducidos. Chrome rechaza el fragmento anexado, incluido moov, lo que provoca un error de descodificación posterior. (Problema de cromo #735335)</p> <p>19921: La reproducción se detiene para cierto contenido HLS aunque su almacenamiento en búfer se haya realizado correctamente (problema de cromo #713540)</p> <p>・ 20444: Si se busca el final del rango en búfer en IE y Edge, la reproducción puede paralizarse.</p> <p>・ 20511: A veces, se puede observar el rechazo de búsqueda para flujos HLS con o sin anuncios.</p> <p>・ 20743: En Windows 10 Chrome, el flujo en directo de HLS se reproduce durante unos segundos antes de la reproducción previa de MP4.</p> <p>・ 21043: Es posible que la dimensión de vídeo no sea correcta durante la carga inicial debido a la falta de metadatos.</p> <p>・ 21115: El gesto del usuario de Android es necesario para iniciar la reproducción si el anuncio previo está disponible para los vídeos en una lista de reproducción.</p> <p>・ HLS Live no admite el rollover de marca de hora.</p> <p>・ No se admite audio AAC-SSR.</p> <p>Los códecs de audio AC3 y AC3 mejorado no son compatibles.</p> <p>・ Para flujos con discontinuidad de marca de hora pero sin marcadores de discontinuidad</p> <p>・ La reproducción puede tener problemas y la búsqueda incorrecta debido a los saltos.</p> <p>・ Es posible que la duración del contenido y de la reproducción no coincidan.</p> <p>・ Las discontinuidades entre representaciones y representaciones deben coincidir con otras, lo que puede provocar problemas de sincronización y parada.</p> <p>・ Es posible que los subtítulos y WebVTT no aparezcan cerca del final del flujo.</p> <p>・ Los cambios en el códec de audio no se admiten en los saltos de marca de tiempo.</p> <p>・ No se admite la inserción de anuncios.</p> <p>・ El modo de truco de avance rápido puede llevar a un bucle de reproducción en Win 8.1 IE 11 (número de MS 12446268).</p> <p>DASH:</p> <p>・ Para flujos en directo: se admite el perfil en directo con tipo dinámico.</p> <p>・ Para flujos VoD: se admite el perfil en directo con tipo estático.</p> <p>Para flujos de VoD: el perfil bajo demanda no está certificado para flujos de trabajo de publicidad.</p> </td> 
   <td><p>・ No se admiten los flujos de DASH Live y DASH Video on Demand.</p> <p>・ La reproducción de vídeo PIP (Picture in Picture) no es compatible con iOS en modo de pantalla completa.</p> <p>En la extensión Safari (etiqueta de vídeo), no funciona menos el manifiesto sin tener un encabezado de tipo de contenido correcto.</p> </td> 
   <td><p>・ El ID de la aplicación en la aplicación del remitente debe ser el mismo que se genera al registrar la URL del receptor como una aplicación del receptor personalizado.</p> <p>・ El reproductor de referencia está certificado para los flujos de trabajo de DASH. El marco de la interfaz de usuario no está certificado.</p> <p>Para obtener una lista de los códecs de medios admitidos, consulte <a href="https://developers.google.com/cast/docs/media"><em>aquí</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Reproducción general (Reproducir, Pausa, Buscar)</td> 
   <td> </td> 
   <td>18098: Algunos problemas de búsqueda se observan con el flujo FER de HLS LBA.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Velocidad de bits adaptable</td> 
   <td><p>・ 20079: Reescritura del búfer en la búsqueda dentro del rango de almacenamiento en búfer.</p> <p>20080: El comportamiento de Flash ABR es coherente con MSE.</p> </td> 
   <td><p>・ La variante de reserva de solo audio en un flujo ABR se ignora debido a limitaciones relacionadas con el búfer.</p> <p>・ 12289: Los params de control ABR no se aplican para audio en caso de flujos HLS/DASH sin muestrear.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Subtítulos 608/708</td> 
   <td> </td> 
   <td><p>・ 7810: En Android 4.4.4, Chrome no parece ser compatible con las familias de fuentes CSS básicas utilizadas por el reproductor y, por lo tanto, la función de cambio de estilo de fuente no funciona.</p> <p>・ Los canales CC no se pueden cambiar en el caso de 608 subtítulos.</p> <p>・ Las características de estilo avanzadas no son compatibles con los 608 rótulos.</p> <p>Se admiten los rótulos incrustados (608/708), marcados mediante la etiqueta Accesibilidad.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>・ 5206: El reproductor ignora las etiquetas de región del archivo WebVTT al mostrar los rótulos.</p> <p>・ DASH: No se admiten los archivos VTT fragmentados o segmentados.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Failover de manifiesto</td> 
   <td>21056: Con Flash Fallback, la conmutación por error no se produce en el flujo en directo si el flujo principal devuelve un error 404 durante la reproducción.</td> 
   <td>La conmutación por error de manifiesto solo se aplica a contenido y no a anuncios.</td> 
   <td>La conmutación por error de la lista de reproducción que falta funciona en Safari solamente para el código de error HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Failover avanzado</td> 
   <td> </td> 
   <td><p>・ La conmutación por error de segmentos no admite omitir segmentos no disponibles y continuar con la reproducción.</p> <p>20533: Los segmentos que faltan en una lista de reproducción deben tratarse como una discontinuidad y la reproducción debe reanudarse desde el siguiente segmento disponible.</p> <p>21267: El cambio de flujo debido a un error puede llevar a la descarga de segmentos más antiguos.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Notificaciones de QoS y reproductor</td> 
   <td>21129: La velocidad de fotogramas no está disponible en caso de Flash Fallback.</td> 
   <td><p>• 11170:</p> <p>Timed_Event no está disponible para Browser TVSDK con MSE, al contrario que para Browser TVSDK con Flash Fallback.</p> <p>21129: La velocidad de fotogramas no se calcula para los flujos interactivos.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Compatibilidad con encabezados de cookie</td> 
   <td> </td> 
   <td> </td> 
   <td><p>el indicador withCredentials y los encabezados de cookies no son compatibles con Safari.</p> <p>21051: Para permitir las cookies en Safari, habilite la configuración "Cookies y datos del sitio web" en Preferencias &gt; Privacidad.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Etiquetas personalizadas</td> 
   <td>14763: No se deben admitir las etiquetas personalizadas que no sean las que empiecen por #. En este momento, se crea el objeto TimedMetadata y se genera un informe para dichas etiquetas durante Flash Fallback.</td> 
   <td>Los flujos con etiquetas personalizadas dentro de banda no están certificados.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Audio de enlace tardío</td> 
   <td> </td> 
   <td><p>・ La inserción de anuncios no es compatible con los flujos LBA en directo de HLS.</p> <p>・ 17273: Los flujos LBA de VOD de HLS cambian a la representación predeterminada en caso de conmutación por error y no se pueden volver a cambiar a la última vez seleccionada.</p> <p>・ 20251: El flujo LBA en directo de HLS puede detener la búsqueda.</p> <p>・ 20497: El reproductor permanece en el estado de almacenamiento en búfer si los flujos no multados HLS LBA carecen de fotogramas de audio o vídeo cerca del final del flujo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>302 Redirección</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>la optimización de redireccionamiento no es compatible con los exploradores Windows Edge e IE, ya que no admiten la propiedad responseURL en el objeto XMLHttpRequest.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 17: Funciones de reproducción avanzadas**

<table> 
 <tbody> 
  <tr> 
   <td>Tipo de contenido</td> 
   <td>Función</td> 
   <td>Flash</td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Reproducción en desplazamiento</td> 
   <td><p>El inicio de la reproducción con un valor de desplazamiento determinado no es compatible con el contenido MP4.</p> </td> 
   <td>20492: Los anuncios intermedios que preceden al desplazamiento se reproducen antes de que el contenido se reanude a partir del valor de desplazamiento.</td> 
   <td>La reproducción con función de desplazamiento no es compatible con iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Reproducción de trucos</td> 
   <td>La reproducción continua no funciona para flujos que no tienen representaciones de iFrame.</td> 
   <td><p>・ Las adaptaciones de reproducción de trucos no son compatibles con Firefox e Internet Explorer y, por lo tanto, el modo de truco inverso no está disponible en estos exploradores.</p> <p>・ La función Trickplay no está disponible cuando se reproduce contenido junto con anuncios.</p> <p>・ 10435: Durante la reproducción de DASH, el vídeo se congela al reproducir el truco hacia delante en Internet Explorer (Win 8.1)</p> <p>intermitentemente. Esto sucede ya que se utiliza la propiedad playRate de los elementos de vídeo sin la adaptación de la reproducción mediante trucos.</p> <p>14182: A veces, durante el rebobinado en el navegador Chrome, es posible que no se reciba el evento de búsqueda y, por lo tanto, el modo de truco no funcionará.</p> <p>・ 14942: Las tasas de reproducción se pueden establecer en Chrome para Android incluso en el caso de flujos de reproducción sin trucos, pero la configuración no se aplicará y la reproducción continuará a una velocidad normal.</p> <p>・ 17308: La búsqueda no funciona en el modo Trickplay.</p> <p>・ 17309: En el navegador Chrome, el modo de truco inverso no se puede mantener durante más de 2 segundos.</p> <p>19272: Es posible que la reproducción de trucos no se recupere del almacenamiento en búfer en el navegador Windows 10 Edge en caso de flujos DASH.</p> </td> 
   <td>No se admite el modo de truco de rebobinado.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Análisis de ID3</td> 
   <td>20346: SDK también debe devolver el byte de codificación de texto de los marcos ID3.</td> 
   <td><p>El SDK ignora las etiquetas ID3 disponibles en flujos de transporte de datos de audio (ADTS).</p> <p>・ 12378: Los metadatos temporizados de ID3 se analizan en diferentes momentos en Flash y navegador con compatibilidad con MSE y, por lo tanto, el comportamiento de visualización en la línea de tiempo del reproductor de referencia también es diferente.</p> <p>・ 19247: El análisis de ID3 no es compatible con el marco de trabajo de la interfaz de usuario.</p> </td> 
   <td><p>・ 20323: La etiqueta PRIV ID3 utilizada para indicar la marca de tiempo de la primera muestra de un segmento ac no se analiza en Safari (problema de Safari #32422733)</p> <p>・ 20350: En determinados dispositivos (incluido MAC OS X 10.1, iPad 10) Safari no proporciona un evento de cambio de señal cuando se encuentra en modo de truco y, por lo tanto, no se reciben fotogramas de ID3. (Problema de Safari #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Compatibilidad con los marcadores de discontinuidad</td> 
   <td> </td> 
   <td><p>・ La inserción de anuncios en el lado del cliente no es compatible con los flujos HLS que contienen discontinuidad.</p> <p>・ No se permite el cambio del códec de audio en las discontinuidades del flujo HLS.</p> <p>・ El interruptor de pista de audio no es compatible con el flujo HLS con los marcadores de discontinuidad</p> </td> 
   <td>El número de secuencia de discontinuidad es un requisito para los flujos HLS con discontinuidad para poder reproducirlos en Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 18: Funciones de protección de contenido**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>El rango de bytes no es compatible con el contenido cifrado AES-128.</td> 
   <td>12324: Los flujos cifrados HLS AES-128 no se reproducen en Safari si no se especifica la etiqueta IV.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>・ 12660: El reproductor HTML5 emite un error interno del servidor para el contenido del guión cifrado PlayReady caducado.</p> <p>・ 16720: El contenido cifrado DASH DRM no funcionará si falta el atributo de inicio en la etiqueta period.</p> <p>・ 18589: La reproducción no es compatible con flujos DRM protegidos Dash VoD Multiperíodo con Xlink.</p> <p>・ 18653: La reproducción de contenido multiperíodo amplio con varias claves se detiene en el primer período y no puede cambiar al siguiente período.</p> <p>・ 18656: El flujo MultiPeriod de Playready, cifrado con claves diferentes, no se reproduce.</p> <p>Playready 2.0 para Dash no está certificado.</p> <p> </p> <p> </p> </td> 
   <td>12602: El reproductor de HTML5 actualiza repetidamente los metadatos DRM de HLS Fairplay en Safari</td> 
   <td><p>Se puede reproducir contenido DASH Widevine DRM empaquetado a través de Bento4. No se reproduce el contenido empaquetado a través de Offline Packager y Shaka Packager. DASH PlayReady DRM no es compatible.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 19: Funciones principales de inserción de publicidad (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Pre/Mid/Post</td> 
   <td> </td> 
   <td><p>・ Los anuncios de predesplazamiento con contenido en directo HLS se reproducen en modo de reproductor dual.</p> <p>・ Los anuncios DASH con contenido HLS y los anuncios HLS con contenido DASH no son compatibles.</p> <p>・ 19002: En HTML5 Player con MSE adBreak. insertType no devuelve el valor correcto para representar el tipo de inserción correcto, es decir, el cliente insertado o el servidor insertado.</p> <p>7794: En dispositivos móviles (iOS, Android con Chrome 33 o inferior o Navegador nativo) donde la barra de control predeterminada está visible en modo de pantalla completa, la barra de búsqueda y los botones de avance rápido están disponibles cuando se reproduce el anuncio.</p> <p>・ 11048: El cambio del contenido de anuncio a HLS Live no es suave en el caso de las extensiones de Media Source.</p> <p>・ 16083: En Android 4.4 Chrome v52, a veces los anuncios HLS con contenido HLS pueden provocar un error de descodificación de la canalización después de la reproducción paralizada.</p> <p>・ 16097: Los errores encontrados durante la pausa publicitaria no se controlan, lo que puede hacer que el flujo principal detenga la reproducción.</p> <p>・ 18095: Los anuncios en MP4 no son compatibles con el contenido en directo de HLS.</p> <p>19120: Varias búsquedas en anuncios HLS con contenido HLS pueden hacer que el flujo detenga la reproducción.</p> <p>・ 19131: La superposición de almacenamiento en búfer puede aparecer al cambiar de la pausa publicitaria previa al contenido.</p> <p>・ 20296: En el caso de los flujos HLS Live, la búsqueda en la ventana DVR seguida de la búsqueda de rollos medios resueltos puede provocar un bloqueo de reproducción.</p> <p>・ 20298:HLS Transmisiones en directo con rodillos medios se paralizan en el primer momento en mitad de rollo y se mueven fuera de la ventana DVR.</p> <p>・ 20317: Las transmisiones en directo de HLS pueden bloquearse al cambiar al siguiente anuncio o de anuncio a contenido en caso de que la pausa publicitaria contenga más de un anuncio.</p> 
    <ul> 
     <li>Los anuncios de la ventana DVR de los flujos HLS Live no se resuelven.</li> 
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
   <td>21464: La respuesta a la publicidad se descarta por completo si el reempaquetado creativo falla en una de las publicidades de la pausa publicitaria.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 20: Funciones avanzadas de inserción de publicidad (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción de DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Solo publicidad</td> 
   <td> </td> 
   <td>20056: La propiedad de tecnología del reproductor no es relevante, ya que se basa en el contenido principal que está vacío en caso de reproducción solo de publicidad</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Directiva de publicidad personalizada</td> 
   <td> </td> 
   <td><p>・ Los comportamientos de publicidad no son compatibles con los anuncios en MP4 y el contenido en MP4.</p> <p>・ 13973: Comportamientos de publicidad personalizados: la directiva SKIP no genera un evento completo cuando se utiliza con MSE.</p> <p>・ 14939: Las directivas de comportamiento de publicidad personalizadas que se omiten y se omiten no funcionan para el contenido de DASH.</p> <p>・ 17131: El primer fotograma de la publicidad es visible y, a continuación, el contenido se reanuda en caso de que se OMITA la directiva de pausa publicitaria.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Publicidades complementarias/ publicidades tipo titular/ Publicidades en las que se puede hacer clic</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Las publicidades de titular no están visibles al utilizar el reproductor de referencia.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ Los comportamientos de publicidad no son compatibles con los anuncios VPAID.</p> <p>・ 15032: Las publicidades VPAID en combinación con anuncios MP4 o HLS en una pausa publicitaria no son compatibles.</p> <p>・ 19001: En Android e iOS cuando la publicidad VPAID se reproduce con MP4 como contenido principal, se pueden oír dos pistas de audio, una de contenido principal y otra de publicidad.</p> <p>・ 20762: Las publicidades VPAID no son compatibles con Picture in Picture (PIP).</p> <p>・ 21172: El evento de reproducción completa no se recibe para el contenido de HLS VOD con anuncios VPAID.</p> <p>・ 21173: No se recibe onAdBreakCompleteEvent para el contenido VOD de HLS ni para las publicidades VPAID de anuncio.</p> </td> 
   <td>El reproductor cambia entre el modo normal y el modo de pantalla completa al cambiar entre el contenido principal y el de VPAID.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Cuadro 21: Integraciones**

| **Tipo de contenido** | **Función** | **Flash** | **HTML5 en Firefox, IE, Chrome, Android Chrome** | **HTML5 en Safari, iOS Safari** | **Chromecast (solo reproducción de DASH)** |
|---|---|---|---|---|---|
| VOD + Activo | Integración VHL de Adobe Analytics |  | 19004: El seguimiento de Video Analytics no está disponible mediante la herramienta de configuración de interfaz de usuario. |  |  |

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.