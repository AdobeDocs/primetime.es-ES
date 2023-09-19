---
title: Notas de la versión de TVSDK 2.4 del explorador
description: Las notas de la versión del explorador TVSDK 2.4 describen las funciones nuevas, admitidas y no admitidas, y los problemas conocidos del explorador TVSDK 2.4.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# Notas de la versión de TVSDK 2.4 del explorador {#browser-tvsdk-release-notes}

Las notas de la versión del explorador TVSDK 2.4 describen las funciones nuevas, admitidas y no admitidas, y los problemas conocidos del explorador TVSDK 2.4.

## Introducción {#introduction}

Browser TVSDK es un kit de herramientas que le permite añadir funciones avanzadas de reproducción de vídeo, protección de contenido y publicidad a las aplicaciones de reproductor de vídeo basadas en navegador.

El TVSDK 2.4 del explorador proporciona API de JavaScript para crear aplicaciones de vídeo basadas en el explorador e incluye compatibilidad de reproducción en los siguientes modos:

* Solo HTML 5
* HTML5 con reserva de flash automático
* Flash siempre

Esta versión incluye la siguiente información:

· [Documentación de la API TVSDK del explorador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

· [Guía de programación de Browser TVSDK](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

· [Guía de migración de TVSDK para 1.4 DHLS a Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

· [Conversión del explorador TVSDK 2.4.6 a la versión 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

· Una implementación de referencia, que se incluye en la compilación.

>[!NOTE]
>
>*Para obtener una lista completa de las consideraciones de seguridad de esta versión, consulte Consideraciones de seguridad.

## Novedades y funciones compatibles {#what-s-new-and-supported-features}

Esta versión de Browser TVSDK proporciona nuevas funciones que puede utilizar para mejorar las aplicaciones de vídeo.

**Nuevo en la actualización 2.4.12 (compilación 204)**

La siguiente adición está disponible como parte de la actualización del explorador TVSDK 2.4.12 (compilación 204):

* La implementación de la API por volumen de AdobePSDK.MediaPlayer se cambia para permitir la reproducción automática en iOS cuando se silencia la reproducción.

· Una nueva API, `auditudeSettings.ignoreVPAIDAds`, se agrega para permitir ignorar los anuncios VPAID recibidos del servidor de Auditude. La API no funciona para la reserva de Flash.

**Versión 2.4.11**

Las siguientes mejoras y adiciones están disponibles como parte de la versión del explorador TVSDK 2.4.11:

· La conmutación por error de segmentos en directo de HLS es compatible con los modos de reserva MSE y Flash.

· Compatibilidad con `AuditudeSettings.creativeRepackagingDomain` La API ahora también está disponible para MSE. Anteriormente solo era compatible con el modo de reserva de Flash.

· La versión incluye correcciones para problemas críticos del cliente. Consulte *Problemas corregidos* una lista.

**Versión 2.4.10**

Las siguientes mejoras y adiciones están disponibles como parte de la versión del explorador TVSDK 2.4.10:

· TVSDK proporciona enableLogging() para activar o desactivar el registro. Consulte la [Documentación de API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)para su uso.

· TVSDK ya no admite capítulos predeterminados al utilizar Adobe Analytics. Defina y administre capítulos con su aplicación.

· La versión incluye correcciones para problemas críticos del cliente. Consulte *Problemas corregidos *a lista.

**Versión 2.4.9**

Las siguientes mejoras y adiciones están disponibles como parte de la versión del explorador TVSDK 2.4.9:

· HLS VOD y transmisiones en vivo con discontinuidad de tiempo, pero sin marcadores de discontinuidad son compatibles.

· Los fotogramas ID3 v2.4.0 son compatibles con la etiqueta de vídeo de Safari para VOD de HLS y transmisiones en directo.

· La implementación de carga segura de publicidad garantiza que las llamadas al servidor de publicidad se actualicen a HTTP seguro en función de la configuración de la API. Para obtener más información, consulte las clases AdobePSDK.AdvertisingMetadata y AdobePSDK.ForceHttpsAdConfiguration. Esta función no se admite en el modo de reserva de Flash.

· La información de ID de anuncio y la información de extensión asociada con las respuestas de VAST 3.0 ahora están disponibles para la aplicación por TVSDK y se pueden utilizar para implementar la integración de Moat para las mediciones de publicidad. Para obtener más información, consulte API AdobePSDK.NetworkAdInfo. Esto no se admite en el modo de reserva de Flash.

· La clase AdobePSDK.ForceHttpsConfiguration ya no está disponible. Se ejecuta correctamente mediante

AdobePSDK.ForceHttpsAdConfiguration (clase).

· Una nueva API, AdobePSDK.optimizeFlashCalls, ya está disponible para optimizar las llamadas a fin de mejorar la experiencia de reproducción HLS en el modo de reserva de Flash. Esta opción está desactivada de forma predeterminada.

**Nuevo en la actualización 2.4.8 (compilación 6002)**

Esta actualización contiene correcciones para problemas críticos del cliente. Consulte *Problemas solucionados*, para la lista.

**Versión 2.4.8**

Las siguientes mejoras y adiciones están disponibles como parte de la versión del explorador TVSDK 2.4.8:

· El SDK ahora es compatible con Chrome EME y los cambios de prácticas recomendadas disponibles a partir de Chrome v58. Para obtener más información, consulte [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· El marco de la interfaz de usuario ahora admite DRM de acceso HLS en el flujo de trabajo de Flash, solo publicidad y segmentación de información.

· La API setDRMAuthenticateData se agrega al marco de la interfaz de usuario. Para reproducir flujos protegidos con DRM de acceso a Adobe, invoque esta API. Como alternativa, el atributo drmAuthenticateData se puede especificar en el reproductor. Consulte [AdobePSDK.videoBehavior](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)para obtener más información.

**Versión 2.4.7**

Las siguientes funciones son nuevas en la versión 2.4.7:

· Adición del configurador de IU en el marco de la interfaz de usuario

Puede configurar el reproductor de una de las siguientes maneras:

· Uso de un objeto JSON

· Uso de API

Para ayudar a generar el objeto JSON, Browser TVSDK proporciona una herramienta **UI Configurator **.

En esta herramienta, puede seleccionar varias opciones, hacer clic en **Probar configuración **para comprobar la configuración y hacer clic en **Descargar configuración **para descargar la configuración. Después de descargar el archivo, puede pasar el contenido de este archivo como objeto JSON a la API ptp.videoPlayer.

· Adición de la API MediaPlayerItemConfig al marco de la IU

Varias funciones, como advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration, se pueden configurar mediante MediaPlayerItemConfig. Para obtener más información, consulte la documentación de AdobePSDK.MediaPlayerItemConfig en la [API de TVSDK del explorador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [documentación](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

En el marco de la interfaz de usuario de, se ha modificado la forma de pasar configuraciones de red a través de la configuración del reproductor.

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

* Compatibilidad con flujos de trabajo de DRM y Analytics en el marco de IU de

Las configuraciones de DRM y el seguimiento de Analytics se pueden habilitar a través del marco de la interfaz de usuario.

* Adición de `AdobePSDK.embedSWFinFullScreenDiv` API

Esta nueva API proporciona flexibilidad a la aplicación del reproductor para seleccionar el div en el que puede incrustar el archivo FlashFallback.swf.

* Reemplazado `getVersion`API de `AdobePSDK.MediaPlayer` clase con `AdobePSDK.Version` para obtener información relacionada con la versión de TVSDK. Para obtener más información, consulte `AdobePSDK.Version` API [aquí](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versión 2.4.6**

Las siguientes funciones son nuevas en la versión 2.4.6:

* **Compatibilidad con Browserify**

Browserify le permite utilizar los módulos de estilo node.js en el explorador. Puede definir las dependencias y Browserify agrupa todo en un archivo JavaScript.

* **Factura**

Con la ayuda de la facturación, TVSDK del explorador puede recopilar métricas de uso del reproductor para facturar a los clientes de Primetime.

>[!NOTE]
>
>La enumeración obsoleta MediaPlayer.Events y las constantes obsoletas de Enum PSDKErrorCode se han eliminado en la versión 2.4.6. Para obtener más información, consulte [Conversión del explorador TVSDK 2.4.5 a la versión 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versión 2.4.5**

Las siguientes funciones son nuevas en la versión 2.4.5:

* **Reproducciones y anuncios de eventos completos**

  Los flujos de reproducción completa de eventos (FER) de HLS ahora admiten la resolución de anuncios y comportamientos de anuncios. Para habilitar esta compatibilidad, establezca el modo de señalización de publicidad en `MANIFEST_CUES` al crear el `MediaPlayerItemConfig` objeto.

* **Compatibilidad con MediaplayerView ScalePolicy**

  Los desarrolladores de aplicaciones ahora pueden especificar un scalePolicy diferente para la vista mediante la propiedad scalePolicy de MediaPlayerView.

* **Compatibilidad con contenido anamórfico**

  La reproducción de contenido anamórfico ahora se admite al utilizar MSE y la reproducción en Flash.

* **Aplicación selectiva de`withCredentials`**

Cuándo `withCredentials` se establece en true, la variable `Access-Control-Allow-Origin` el encabezado no se puede establecer en comodín. Según la respuesta del servidor, TVSDK del explorador establecerá de forma selectiva la variable `withCredentials` atributo. Para obtener más información acerca de esta compatibilidad, consulte [Documentos de API de TVSDK del explorador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versión 2.4.4**

Las siguientes funciones fueron nuevas en la versión 2.4.4:

* **Aplicación de muestra de Chromecast**

Esta versión es compatible con una aplicación de remitente y receptor que muestra la reproducción de flujos de VOD DASH y flujos de Widevine DASH con inserción de anuncios en el lado del cliente.

* **Compatibilidad con failover avanzado**

Esta versión es compatible con casos de uso de failover avanzados (failover de segmentos y servidores) para flujos de VOD de HLS.

**Versión 2.4.3**

Las siguientes funciones fueron nuevas en la versión 2.4.3:

* **Etiquetas personalizadas para DASH VOD**

  Las etiquetas personalizadas en línea (eventos) se pueden suscribir y recibir como un objeto TimedMetadata.

* **Reproducción de flujos sin extensiones**

  Ahora se admiten flujos HLS y DASH sin extensiones. Para el archivo de manifiesto, es necesario especificar resourceType al cargar el recurso. Para segmentos y archivos VTT, se utiliza el encabezado de respuesta Content-Type para determinar el tipo de contenido.

**Versión 2.4.2**

Las siguientes funciones fueron nuevas en la versión 2.4.2:

* **Paridad de API**

Para obtener una lista completa de la paridad de la API, consulte la [Guía de migración de TVSDK para 1.4 DHLS a Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Compatibilidad con AES de muestra**

  Esta versión agrega compatibilidad con la reproducción de contenido cifrado AES de muestra en MSE y la reserva de Flash. Se ha eliminado la obligación de alojar contenido AES sobre un origen seguro en Google Chrome.

* **Compatibilidad con contenedores de AAC**

  Ahora se admite la reproducción de archivos con la extensión .aac. Pueden ser emisiones de solo audio o audio alternativo.

  >[!NOTE]
  >
  >Los códecs AC3 y AC3 mejorados aún no son compatibles.

* **Reproducción de flujo tokenizada**

Los flujos HLS que se entregan a través de una red de distribución de contenido (CDN) a veces pueden utilizar tokens de autenticación en las solicitudes de verificación de manifiesto y segmento, y estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookie. Ahora se admite la reproducción de dichos flujos.

**Versión 2.4.1**

Las siguientes funciones fueron nuevas en la versión 2.4.1:

* **Marco de IU**

Este marco de trabajo, diseñado para acelerar el desarrollo de la interfaz de usuario para aplicaciones de reproductor de vídeo basadas en JavaScript, consta de API para incluir controles básicos como reproducción/pausa y volumen y para añadir o eliminar fácilmente elementos como estados de barra de desplazamiento y ajustes de subtítulos. Puede especificar el comportamiento asociado a los controles, crear controles personalizados y aplicar máscara a la interfaz de usuario del reproductor. Todo esto sucede a través del marco de trabajo, sin necesidad de manipular directamente la estructura del DOM.

* **Mejoras en la reproducción de HLS para emisiones en directo**

Esta versión admite las discontinuidades causadas por la inserción de anuncios. Utiliza la etiqueta EXT-PROGRAM-DATE-TIME seguida de la etiqueta EXT-MEDIA-SEQUENCE para sincronizar los perfiles de velocidad de bits adaptables y garantizar una reproducción fluida.

* **Compatibilidad con VPAID 2.0**

La versión 2.0 de la definición de la interfaz del servidor de anuncios del reproductor de vídeo (VPAID) proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de anuncios y monetizar el contenido de vídeo. Esta versión admite anuncios VPAID de JavaScript lineales para contenido de vídeo bajo demanda (VOD).

* **Etiquetas HLS personalizadas**

Los flujos de medios pueden llevar metadatos adicionales en forma de etiquetas en el archivo de lista de reproducción/manifiesto. El TVSDK del explorador permite especificar y suscribirse a etiquetas adicionales y recibir notificaciones cuando dichas etiquetas aparecen en el manifiesto.

* **Marcadores de anuncio mostrados en la cronología del reproductor**

Esta versión admite la visualización de marcadores de publicidad en la cronología del reproductor para contenido en directo y VOD. Puede ver este comportamiento en el reproductor de referencia.

**Compatible con 2.4**

Las siguientes funciones estaban disponibles en la versión 2.4:

* **Reproducción de audio MP3**

  Esta versión es compatible con la reproducción de audio MP3 en navegadores con extensiones de fuentes de medios (MSE) y con la etiqueta de vídeo Safari.

* **Reproducción de vídeo MP4**

  Se admiten las siguientes funciones:

   * Reproducción de un solo flujo
   * Anuncios MP4 previos a la emisión y posteriores a la emisión con comportamientos y seguimiento de anuncios
   * Anuncios HLS previos a la emisión y posteriores a la emisión con comportamientos y seguimiento de anuncios
   * Anuncios DASH previos a la emisión y posteriores a la emisión con comportamientos y seguimiento de anuncios

## Plataformas compatibles {#supported-platforms}

Browser TVSDK tiene requisitos específicos para los niveles de plataformas y software en los que debe ejecutarse. Se admiten las siguientes plataformas y niveles de software:

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

* APPLE OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### Configuraciones web móviles {#mobile-web-configurations}

* Android 4.4

   * Explorador nativo
   * Chrome 33+

* Android 5.0

   * Navegador nativo
   * Chrome 33+

* Android 6.0

   * · Chrome 33+

* APPLE IOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast (segunda generación; solo para reproducción DASH)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Tecnología</strong> </p> </td> 
   <td><p><strong>Etiqueta de vídeo TVSDK del explorador</strong><sup>1</sup></p> </td> 
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
   <td><p>HLS, GUIÓN</p> </td> 
   <td><p>MP4 y HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de características {#feature-matrix}

Esta es una lista de las funciones compatibles y no compatibles con esta versión:

* *Funciones de audio MP3: reproducción principal*
* *Funciones de vídeo MP4: reproducción principal*
* *Funciones de vídeo MP4: Ad Insertion principal*

>[!NOTE]
>
>*En las tablas de matriz de funciones que aparecen a continuación, una &quot;Y&quot; significa que la función es compatible con la versión actual.*

### Funciones de audio MP3 {#mp-audio-features}

**Tabla 1: Reproducción principal{#table-core-playback}**

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | MP3 VOD | Reproducción general (reproducir, pausar, buscar) | No compatible | Y | Y |

1 La etiqueta de vídeo TVSDK del explorador no admite streaming y DRM. La compatibilidad con códec y contenedor no es la misma en todos los exploradores.

2 Firefox usa el Flash Player de forma predeterminada para la versión 41 o anterior.

### Características de audio MP4 {#mp-audio-features-1}

**Tabla 2: Reproducción principal**

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | MP4 VOD | Reproducción general (reproducir, pausar, buscar) | No compatible | Y | Y |

**Tabla 3: Ad Insertion principal**

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | Anuncio previo a la emisión (MP4) | No compatible | Y | Y |
| Ad Insertion | MP4 VOD | Post-roll (MP4) | No compatible | Y | Y |

Para obtener más información acerca de la compatibilidad con funciones HLS o DASH, consulte a continuación.

## Matriz de características HLS {#hls-feature-matrix}

Esta es la matriz de características para las características HLS de TVSDK del explorador.

* *Reproducción principal de HLS*
* *Funciones de reproducción avanzadas de HLS*
* *Funciones de protección de contenido HLS*
* *Funciones de inserción de publicidad principal de HLS*
* *Funciones avanzadas de inserción de publicidad de HLS*
* *Integraciones HLS*

>[!NOTE]
>
>*En las tablas de matriz de funciones que aparecen a continuación, una &quot;Y&quot; significa que la función es compatible con la versión actual.*

### Funciones de HLS {#hls-features}

Se admiten las siguientes funciones:

**Tabla 4: Reproducción principal de HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>VOD FER</p> </td> 
   <td><p>Reproducción general (reproducción, pausa y búsqueda)</p> </td> 
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
   <td><p>608/708 subtítulos</p> </td> 
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
   <td><p>Conmutación por error avanzada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>QoS y notificaciones del reproductor</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Compatibilidad con QoS limitada</p> </td> 
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
   <td><p>Estableciendo parámetros de control de búfer</p> </td> 
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
   <td><p>Redirección 302</p> </td> 
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
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reproducción en offset</p> </td> 
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
   <td><p>Juego de trucos</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smooth Trick Play</p> </td> 
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
   <td><p>Compatibilidad con marcadores de discontinuidad</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Flujos tokenizados</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Factura</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 6: Características de protección de contenido HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Acceso a Adobe</p> </td> 
   <td><p>No compatible</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 7: Funciones de inserción de publicidad principal de HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Anuncio previo a la emisión (MP4/HLS)</p> </td> 
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
   <td><p>Post-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD FER</p> </td> 
   <td><p>Resolución y comportamientos de anuncios</p> </td> 
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

**Tabla 8: Funciones avanzadas de inserción de anuncios de HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo anuncio</p> </td> 
   <td><p>No compatible</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Parámetros de segmentación</p> </td> 
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
   <td><p>Carga diferida de publicidad</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>No compatible</p> </td> 
   <td><p>Limitación de plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anuncios complementarios, Anuncios de banner, Anuncios en los que se puede hacer clic</p> </td> 
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

**Tabla 9: Integraciones de HLS{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
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

## Matriz de características del SALPICADERO {#dash-feature-matrix}

Esta es la matriz de características para las características de DASH en el explorador TVSDK.

· *Funciones de reproducción DASH Core*

· *Funciones de reproducción avanzadas de DASH*

· *Funciones de protección de contenido DASH*

· *Funciones de inserción de publicidad principal de DASH*

· *DASH Funciones avanzadas de inserción de anuncios*

· *Integraciones de DASH*

>[!NOTE]
>
>En las tablas de matriz de características que aparecen a continuación, una Y significa que la función es compatible con la versión actual.

### Funciones de GUIÓN {#dash-features}

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
   <td><p>VOD FER</p> </td> 
   <td><p>Reproducción general (reproducción, pausa y búsqueda)</p> </td> 
   <td><p>No compatible</p> </td> 
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
   <td><p>608/708 subtítulos</p> </td> 
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
   <td><p>QoS y notificaciones del reproductor</p> </td> 
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
   <td><p>Estableciendo parámetros de control de búfer</p> </td> 
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
   <td><p>Audio de límite tardío</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Redirección 302</p> </td> 
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
   <td><p>Reproducción en offset</p> </td> 
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
   <td><p>Smooth Trick Play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Análisis de ID3</p> </td> 
   <td><p>No compatible</p> </td> 
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
   <td><p>Flujos tokenizados</p> </td> 
   <td><p>No compatible</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reproducción</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Factura</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 12: Características de protección de contenido DASH**

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
   <td><p>No compatible</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>No compatible</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protección de contenido</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>· Widevine en Chrome, Firefox 47 y versiones posteriores y Chromecast</p> <p>· PlayReady en Internet Explorer en Windows 8.1 y Edge</p> <p>· DRM de Primetime para Windows Firefox (solo vídeo)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 13: Funciones de inserción de publicidad DASH Core**

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
   <td><p>Anuncio previo a la emisión (MP4/DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Mid-roll (SALPICADERO)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD FER</p> </td> 
   <td><p>Resolución y comportamientos de publicidad</p> </td> 
   <td><p>No compatible</p> </td> 
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
   <td><p>No compatible</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 14: Funciones avanzadas de inserción de anuncios DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoría</strong></p> </td> 
   <td><p><strong>Tipo de contenido</strong></p> </td> 
   <td><p><strong>Función</strong></p> </td> 
   <td><p><strong>HTML 5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo anuncio</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parámetros de segmentación</p> </td> 
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
   <td><p>No compatible</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Carga diferida de publicidad</p> </td> 
   <td><p>No compatible</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anuncios complementarios, anuncios de banner, anuncios en los que se puede hacer clic</p> </td> 
   <td><p>No compatible</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>No compatible</p> </td> 
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
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integraciones</p> </td> 
   <td><p>VOD + Activo</p> </td> 
   <td><p>Integración de VHL de Adobe Analytics</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemas corregidos {#issues-fixed}

**Problemas corregidos en la actualización 2.4.12 (compilación 204)**

Los siguientes problemas se solucionan en la actualización de la versión 2.4.12 de TVSDK del explorador (compilación 204):

· **21647**- TVSDK debe permitir la reproducción automática de vídeo en dispositivos iOS cuando el audio está silenciado.

· **21465**- Acceso al sistema con clave de error denegado al reproducir un flujo DASH protegido por DRM después de reproducir un flujo DASH Live.

· **21442**- Habilite la reproducción automática de contenido en la web de iOS, después de reproducir el anuncio previo al desplazamiento con un gesto del usuario.

· **21240**: API proporcionada para filtrar los anuncios VPAID analizados desde Auditude/VMAP.

**Problemas corregidos en la versión 2.4.11**

Los siguientes problemas se corrigen en la versión 2.4.11 de TVSDK del explorador:

**Funciones principales de reproducción:**

· **19192**: TVSDK ahora implementa TextFormat:bottomInset y TextFormat:safeArea. Debido a estas mejoras, los subtítulos opcionales se pueden volver a colocar si la barra de control se muestra en la pantalla.

· **21009**: los subtítulos cerrados persisten en la pantalla en caso de búsqueda a través de la discontinuidad hasta que aparecen nuevos subtítulos.

· **21141**: la búsqueda de nuevo se rechaza debido a una condición de carrera durante la adición de segmentos.

· **21142**: haciendo que los rangos de reproducción seleccionables estén disponibles cuando el reproductor está en estado INITIALIZED. Debido a estos cambios, ahora se admite el inicio de la sesión en la posición.

· **21363**: los subtítulos 608/708 no están sincronizados después de la inserción de anuncios para flujos DASH.

**Funciones de inserción de anuncios:**

· **21179**: los problemas relacionados con el anuncio durante la emisión (pausas largas, fotogramas en negro) con contenido de VOD ahora se resuelven configurando correctamente la propiedad ad.primaryAsset.adParameters.

· **21257**: el archivo MP4 con la tasa de bits más alta se selecciona para la transcodificación si MP4 no es un tipo MIME válido y la función de reempaquetado creativo está habilitada.

· **21361**: TVSDK ahora pasa el sistema de anuncios y el ID creativo de la respuesta VAST como parámetros de consulta en la solicitud de paquete creativo para admitir reglas de normalización adicionales.

**Problemas corregidos en la versión 2.4.10**

Los siguientes problemas se solucionan en la versión 2.4.10 de TVSDK para exploradores:

**Funciones principales de reproducción:**

· **21060**: Error de códec no válido producido con flujos HLS que contienen discontinuidad y los cuadros ISO BMFF se ejecutan hasta el final del flujo.

· **21045**: la reproducción automática no funciona en iOS después de que se complete la primera reproducción de vídeo en una lista de reproducción.

· **20975**: El proveedor de QoS devuelve la velocidad de fotogramas como NaN en el explorador Chrome.

· **20823**: error de códec no admitido al encontrar segmentos sin datos.

· **20769**: SDK ahora comienza con la velocidad de bits actual en la búsqueda en lugar de cambiar inmediatamente según la directiva ABR.

· **20031**: En el modo vertical de IE11 (Windows 8.1), la pantalla de vídeo se vuelve pequeña. Función de protección de contenido:

· **19316**: Omita los segmentos que no se puedan descifrar en el caso de flujos HLS AES-128.

**Problemas corregidos en la versión 2.4.9**

Los siguientes problemas se solucionan en la versión 2.4.9 de TVSDK para exploradores:

**Funciones principales de reproducción:**

· **13407**: Los flujos de DASH pueden paralizarse si Firefox deja de enviar el evento &quot;ontimeupdate&quot; durante la reproducción.

· **16380**: Durante la reproducción de contenido de audio y vídeo mezclado de segmentos con tiempos de inicio no coincidentes mediante MSE, el error de sincronización de audio entre representaciones se acumula en los conmutadores ABR, lo que provoca finalmente un error (problema de #663686).

· **17985**: Al reproducir un flujo ISO-BMFF determinado en el navegador Firefox, la reproducción se queda atascada (problema de Firefox #1342913). Esto se ha corregido desde Firefox v53.

· **19141**: No capturado (en promesa) ReferenciaError: la anchura no está definida.

· **18997, 19299**: Problema de parpadeo de vídeo en el límite del segmento. Esto ocurría porque el SDK no calculaba correctamente el desplazamiento de tiempo de composición de la última muestra.

· **19780**: la reproducción no se inicia para el contenido HLS y el anuncio HLS en Firefox v53 (#354653 de problemas de Firefox).

· **20046**: la fecha y hora del programa se recibe como clave en lugar de como valor cuando se recibe como objeto de metadatos cronometrado.

· **20047**: useDefaultResizeHandler genera un error con la reserva de Flash.

· **20179**: La reserva de Flash no funciona con el Flash Player v25.0.0.171.

· **20293**: Firefox detiene el almacenamiento en búfer de datos para ciertos flujos HLS que llevan a un bloqueo.

· **20626**: El reproductor emite un error de descodificación de medios en Chrome debido a un manejo incorrecto de muestras de vídeo con duración cero.

· **20078**: La reproducción se detiene por el error del explorador &quot;QuotaExceeded&quot;.

· **18639**: En el flujo en directo de HLS, el texto 608 CC aparece a veces como mal escrito.

· **20028**: El parámetro de tamaño ClosedCaptions no cambia el tamaño de la fuente.

· **20613**: los cuadros de subtítulos cerrados se superponen entre sí, lo que los hace ilegibles.

**Funciones del Ad Insertion principal (CSAI):**

· **20043**: Faltan las llamadas de impresión de publicidad y seguimiento de publicidad con varios anuncios y redirecciones de terceros.

· **20044**: Cuando se utiliza el reempaquetado creativo, todos los anuncios de la pausa publicitaria deben volver a empaquetarse correctamente. De lo contrario, la pausa publicitaria se descarta completamente.

· **20097**: la reproducción del anuncio se omite y el contenido principal se reanuda inmediatamente en lugar de esperar el tiempo de espera de 20 segundos si el manifiesto del anuncio no está disponible.

**Problemas corregidos en la actualización 2.4.8 (compilación 6002)**

Los siguientes problemas se solucionan en la actualización de la versión 2.4.8 de TVSDK del explorador (compilación 6002):

· **14126:** La reproducción puede detenerse en Firefox (problema #1316024) debido a un hueco interno en el búfer de origen MSE. Intente buscar para reanudar la reproducción

· **19608:** Se ha corregido para respetar el valor de desplazamiento de tiempo de la respuesta de Auditude VMAP.

· **19635:** Corrige el estancamiento de vídeo en Internet Explorer 11 en Windows 10.

· **19761:** Correcciones de problemas de ABR con HLS.

· **19780:** Corrige la reproducción del anuncio con contenido HLS dañado en Mozilla Firefox v53.

· **19877 y 19744:** Los problemas corrigen la incoherencia al seleccionar la velocidad de bits después de una operación de búsqueda. Ahora, la selección de la velocidad de bits en la búsqueda es el valor más bajo de la velocidad de bits actual y de la velocidad de bits en el inicio.

· **19881:** La reproducción atascada y la superposición del almacenamiento en búfer aparecen durante infinito tiempo después de realizar una búsqueda de 3 a 4 veces.

· **19884:** Confirme el cumplimiento de los requisitos de ruta de medios verificada (VMP) de Chrome 59 Beta. bTVSDK pudo reproducir contenido de Widevine DRM con Chrome 59 Beta.

· **19916:** Se ha interrumpido la reproducción de DRM en UI-Framework. Ahora, invoca acquisitionLicense incluso si no hay ninguna directiva en los metadatos.

**Problemas corregidos en la versión 2.4.8**

Los siguientes problemas se solucionan en la versión 2.4.8 de TVSDK para exploradores:

· **10075**: Al buscar antes de la cronología, el evento de reproducción completa no se recibía en Firefox y Chrome y el evento de búsqueda no se recibía en Firefox.

· **15775**: el evento Reproducir completado no se recibe en Windows 8.1 Internet Explorer.

· **17306**: para flujos SAI, se admite la reproducción. No se admite el seguimiento de anuncios enlazados.

· **19142**: A veces, el rebobinado hace que el reproductor de vídeo permanezca en estado de almacenamiento en búfer para siempre.

· **19218**: los marcadores de publicidad no están disponibles a través del marco de la IU.

· **19219**: la reproducción de solo anuncios no funciona a través del marco de interfaz de usuario.

· **19222**: la clave AES-128 se solicita una vez para una lista de reproducción y las solicitudes posteriores se proporcionan desde la caché. Anteriormente se estaba solicitando para cada segmento.

· **19597**: Se ha visto &quot;TypeError no capturado: no se puede leer la propiedad &#39;log&#39; de undefined&quot; con las compilaciones de Chrome para Canary.

· **19605**: adRequestDomain no estaba disponible en el modo de reserva de Flash.

· **19608**: no se insertaban anuncios VMAP para transmisiones en directo de HLS. Ahora, el SDK tiene en cuenta los marcadores de referencia y no depende de los valores de desplazamiento temporal en las respuestas VMAP.

· **19637**: la reproducción de solo anuncios provoca un error de secuencia de comandos al final del anuncio.

· **19732**: las solicitudes de lista de reproducción de CRS fallaban con un error 404. Las solicitudes 1401 y 1403 del TVSDK del explorador ahora se actualizan para encargarse de eso.

· **19762**: acquisitionLicense se solía llamar antes de setAuthenticationToken, por lo que se devolvió una licencia válida independientemente de la validez del token. Esto se corrigió ahora y se llama a acquisitionLicense solo después de la respuesta setAuthenticationToken.

**Problemas corregidos en la versión 2.4.7**

Se han corregido los siguientes problemas en la versión 2.4.7:

· **8397**: Es posible que los flujos en directo de HLS generados a través del Adobe Media Server no se reproduzcan si los segmentos no comienzan con un fotograma clave.

· **13606**: se han corregido varios problemas relacionados con la búsqueda para la emisión HLS en el navegador Chrome.

· **14807**: En el navegador Chrome, si la búsqueda o la pausa se activa inmediatamente después de play(), la reproducción puede detenerse con el error DOMException: La solicitud de play() se interrumpió por una llamada...(Problema de Chromium# 593273).

· **19085**: los parámetros de MediaPlayer como volume, abrControlParameters y ccStyle no se establecen como predeterminados al restablecer el reproductor.

**Problemas corregidos en la versión 2.4.6**

Se ha corregido el siguiente problema en la versión 2.4.6:

· **18093**: TimedMetadata para la etiqueta junto a la etiqueta suscrita se devuelve cuando se utiliza la versión 24 del Flash Player en el modo de reserva de Flash.

**Problemas corregidos en la versión 2.4.4**

Se han corregido los siguientes problemas en la versión 2.4.4:

· **8711**: Con MSE, los subtítulos 608/708 se dejan justificados de forma predeterminada.

· **13934**: La configuración de ABR para anuncios no es aplicable cuando se reproduce con transmisiones en directo de HLS.

· **14079**: La longevidad de los flujos en directo HLS con una ventana DVR baja puede fallar, ya que la reproducción puede retrasarse debido a problemas de latencia de red. Haga clic en el punto en directo para reanudar la reproducción.

· **15037**: las muestras enviadas con el marco de la interfaz de usuario del reproductor no funcionan en Microsoft Internet Explorer 10 en Windows 7.

· **15913**: Para flujos de VOD de HLS, en Chrome, el flujo no se reproducirá si la respuesta del manifiesto es 304 no modificada. Esto se ha corregido desde Chrome v55 (633696 de problemas de Chromium).

· **16103**: En Android Chrome, en condiciones de ancho de banda bajo, la reproducción puede detenerse con el TypeError: No se puede leer la propiedad &quot;programDateTime&quot; de error indefinido.

· **16265**: Para los flujos en directo y VOD de HLS, las búsquedas entre discontinuidades no funcionan.

· **16709**: La reanudación del flujo en directo de HLS con PDT y el marcador de discontinuidad puede provocar que el reproductor se quede atascado en el almacenamiento en búfer.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

A continuación se mencionan las limitaciones y problemas conocidos de TVSDK para exploradores.

**Tabla 16: Características principales de reproducción**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Reproducción general (reproducir, pausar, buscar)</td> 
   <td><p>· No se admiten formatos de medios distintos de HLS.</p> <p>8799: La reserva de Flash no se encarga del contenido mixto y, por lo tanto, debe asegurarse de que el contenido, el anuncio y otras URL no produzcan contenido mixto (contenido seguro y no seguro juntos).</p> <p>· 19271: La reproducción multivisión a través de la interfaz de usuario no es compatible con el modo de reserva de Flash.</p> <p>· La reserva de Flash no funciona en Microsoft Internet Explorer 8 y 9 en Windows 7, ya que estas versiones no son compatibles con el SDK.</p> <p>· 20262: La reserva de Flash añade parámetros personalizados a la lista de información de objetivo. Además, el orden de prioridad de los parámetros personalizados es diferente en el caso del Flash y el MSE.</p> <p>· 20653: La reserva de Flash de TVSDK del explorador no funciona en Win10 con Creators Update.</p> <p>· Flash Fallback funciona con Flash Player versión 23 y posterior.</p> <p>· 20087 - Chrome 59 Beta con</p> <p>Flash 25.0.0.171</p> <p>Beta (predeterminada), la reproducción HLS no funciona en el modo de reserva de Flash. Está funcionando bien en Canarias.</p> </td> 
   <td><p>· 12563: Los flujos de guiones con códec de audio mp4a.40.02 no se reproducen en Firefox debido a una cadena de códec de audio no compatible en MPD. Se admite el códec de audio mp4a.40.2.</p> <p>15029: Al cambiar entre vídeos en multiView en UI-Framework, el botón de reproducción/pausa no se actualiza en consecuencia.</p> <p>· 16034: En Windows 8.1 IE, llamar a reset() conduce a un error de tipo MIME desconocido. Vuelva a cargar el contenido para reanudar la reproducción.</p> <p>· 18235: Se observan ciertos problemas de búsqueda con los flujos de vod de DASH con los anuncios.</p> <p>· 18727: La API de error no es compatible con MSE</p> <p>18750: es posible que los eventos de cambio de estado estén desordenados en algunos casos tanto para el SDK como para el marco de trabajo de la interfaz de usuario y que en el marco de trabajo de la interfaz de usuario falten eventos IDLE e Inicializando el cambio de estado para los oyentes de evento agregados después de cargar el recurso.</p> <p>· 18889: Si MediaPlayer está en estado ERROR, no se devuelve el objeto de vista.</p> <p>· 19039: Si AdobePSDK. Reproductor multimedia. seekToLocal() se utiliza con un valor mayor que EOF y la reproducción comienza desde el principio en el caso de MSE.</p> <p>· 19049: No se informa de ningún estado de error en el Flash Player en Chrome, IE o Firefox cuando el vídeo se bloquea durante la reproducción.</p> <p>· 17205: La reproducción de vídeo se detiene cuando se reproduce un flujo sin mezclar durante unas horas mientras el audio sigue reproduciéndose (problema de cromo# 664033).</p> <p>· 12308: Es posible que se le haya aplicado timeStampOffset a los flujos de DASH con el elemento layout_time_offset especificado en el navegador Chrome, lo que provoca un tiempo de descodificación negativo y, por lo tanto, un error MEDIA_ERR_ SRC_NOT_ SUPPORTED (#398141 de problemas de Chromium).</p> <p>· 14126: La reproducción puede detenerse en Firefox (número de problema 1316024) debido a un hueco interno en el búfer de origen MSE. Intente buscar para reanudar la reproducción.</p> <p>· 19115: MS Edge e IE 11 (Win 8.1 y 10) no establecen Origin como nulo en el redireccionamiento CORS y, sin embargo, falla porque el encabezado no es nulo, lo que provoca un error de reproducción.</p> <p>· 19861: Problema con el comportamiento de adición en el búfer de origen para los medios ya reproducidos. Chrome rechaza el fragmento anexado, incluido moov, lo que provoca un error de descodificación posterior. (#735335 de problema de cromo)</p> <p>19921: La reproducción se detiene para cierto contenido HLS aunque se haya almacenado en búfer correctamente (#713540 de problemas de Chromium)</p> <p>· 20444: Si se busca el final del alcance del almacenamiento en búfer en IE y Edge, la reproducción puede estancarse.</p> <p>· 20511: A veces, el rechazo de búsqueda se puede observar en los flujos HLS con o sin anuncios.</p> <p>· 20743: En Windows 10 Chrome, el flujo en directo de HLS se reproduce durante unos segundos antes de la reproducción previa a la emisión de MP4.</p> <p>· 21043: Es posible que la dimensión de vídeo no sea correcta al cargar por primera vez debido a la falta de metadatos.</p> <p>· 21115: Se requiere el gesto del usuario de Android para iniciar la reproducción si el anuncio previo a la emisión está disponible para los vídeos en una lista de reproducción.</p> <p>· HLS Live no admite la rollover de marca de tiempo.</p> <p>· No admite audio AAC-SSR.</p> <p>Los códecs de audio AC3 y Enhanced AC3 no son compatibles.</p> <p>· Para emisiones con discontinuidad de marca de tiempo pero sin marcadores de discontinuidad</p> <p>· La reproducción puede tener problemas y una búsqueda incorrecta debido a saltos.</p> <p>· Es posible que la duración del contenido y de la reproducción no coincidan.</p> <p>· Las discontinuidades entre representaciones y representaciones deben coincidir en cuanto a otros aspectos, lo que puede provocar problemas de sincronización y estancamiento.</p> <p>· Los subtítulos y WebVTT podrían no aparecer cerca del final del flujo.</p> <p>· Los cambios de códec de audio no son compatibles con los saltos de marca de tiempo.</p> <p>· No se admite la inserción de anuncios.</p> <p>· El modo de truco de avance rápido puede conducir a un bucle de reproducción en Win 8.1 IE 11 (MS issue #12446268).</p> <p>GUIÓN:</p> <p>· Para emisiones en directo: se admite el perfil en directo con tipo dinámico.</p> <p>· Para emisiones VoD: se admite el perfil en directo con tipo estático.</p> <p>Para flujos VoD: el perfil ondemand no está certificado para flujos de trabajo publicitarios.</p> </td> 
   <td><p>· No se admiten los flujos de vídeo en directo y a petición DASH.</p> <p>· La reproducción de vídeo PIP (Imagen en imagen) no es compatible con iOS en modo de pantalla completa.</p> <p>En Safari (Etiqueta de vídeo), la extensión menos manifiesto sin tener un encabezado de tipo de contenido correcto no funciona.</p> </td> 
   <td><p>· applicationID en la aplicación del remitente debe ser el mismo que se genera al registrar la URL del receptor como aplicación de receptor personalizada.</p> <p>· El reproductor de referencia está certificado para flujos de trabajo DASH. El marco de interfaz de usuario no está certificado.</p> <p>Para obtener una lista de los códecs multimedia admitidos, consulte <a href="https://developers.google.com/cast/docs/media"><em>aquí</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>VOD FER</td> 
   <td>Reproducción general (reproducir, pausar, buscar)</td> 
   <td> </td> 
   <td>18098: Se observan ciertos problemas de búsqueda con el flujo FER LBA de HLS.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Velocidad de bits adaptable</td> 
   <td><p>· 20079: reescritura del búfer en búsqueda dentro del intervalo almacenado en búfer.</p> <p>20080: El comportamiento de la ABR del Flash es coherente con el MSE.</p> </td> 
   <td><p>· La variante de reserva solo de audio en un flujo ABR se ignora debido a limitaciones relacionadas con el búfer.</p> <p>· 12289: Los parámetros de control ABR no se aplican para audio en caso de emisiones HLS/DASH sin mezclar.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Subtítulos 608/708</td> 
   <td> </td> 
   <td><p>· 7810: En Android 4.4.4, Chrome no parece ser compatible con las familias de fuentes CSS básicas utilizadas por el reproductor y, por lo tanto, la función de cambio de estilo de fuente no funciona.</p> <p>· Los canales CC no se pueden cambiar en el caso de 608 subtítulos.</p> <p>· Las funciones de estilo avanzadas no son compatibles con subtítulos para 608.</p> <p>Se admiten subtítulos incrustados (608/708), marcados con la etiqueta Accesibilidad.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206: El reproductor ignora las etiquetas de región del archivo WebVTT al mostrar los subtítulos.</p> <p>· GUIÓN: No se admiten archivos VTT fragmentados o segmentados.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Conmutación por error de manifiesto</td> 
   <td>21056: Con la reserva de Flash, la conmutación por error no se produce para el flujo en directo si el flujo principal devuelve un error 404 durante la reproducción.</td> 
   <td>La conmutación por error de manifiesto solo se aplica al contenido y no a los anuncios.</td> 
   <td>La conmutación por error de lista de reproducción faltante funciona en Safari solo para el código de error HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Conmutación por error avanzada</td> 
   <td> </td> 
   <td><p>· La conmutación por error de segmentos no admite omitir segmentos no disponibles y continuar la reproducción.</p> <p>20533: Los segmentos que falten en una lista de reproducción deben tratarse como una discontinuidad y la reproducción debe reanudarse a partir del siguiente segmento disponible.</p> <p>21267: La conmutación de la emisión debido a una conmutación por error puede provocar la descarga de segmentos más antiguos.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Notificaciones de QoS y reproductor</td> 
   <td>21129: La velocidad de fotogramas no está disponible en caso de reserva de Flash.</td> 
   <td><p>• 11170:</p> <p>Timed_Event no está disponible para el TVSDK del explorador con MSE, a diferencia de para el TVSDK del explorador con reserva de Flash.</p> <p>21129: La velocidad de fotogramas no se calcula para emisiones en directo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Compatibilidad con encabezados de cookie</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Safari no es compatible con el indicador de credenciales ni con los encabezados de cookies.</p> <p>21051: Para permitir cookies en Safari, habilite la configuración "Cookies y datos de sitios web" en Preferencias &gt; Privacidad.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Etiquetas personalizadas</td> 
   <td>14763: No se deben admitir etiquetas personalizadas que no sean las que empiecen por #. Ahora mismo, el objeto TimedMetadata se crea y registra para dichas etiquetas durante la reserva de Flash.</td> 
   <td>Los flujos con etiquetas personalizadas en banda no están certificados.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Audio de enlace tardío</td> 
   <td> </td> 
   <td><p>· La inserción de anuncios no es compatible con transmisiones LBA en directo de HLS.</p> <p>· 17273: Los flujos LBA de VOD de HLS cambian a la representación predeterminada en caso de failover y no se pueden volver a seleccionar por última vez.</p> <p>· 20251: La transmisión LBA en vivo de HLS puede demorarse en la búsqueda.</p> <p>· 20497: El reproductor permanece en estado de almacenamiento en búfer si los flujos sin mezclar LBA de HLS tienen fotogramas de audio o vídeo faltantes cerca del final del flujo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Redirección 302</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>la optimización de redireccionamiento no se admite en los exploradores Edge e IE de Windows, ya que no admiten la propiedad responseURL en el objeto XMLHttpRequest.</p> </td> 
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
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Reproducción en offset</td> 
   <td><p>El inicio de la reproducción con un valor de desplazamiento determinado no es compatible con el contenido MP4.</p> </td> 
   <td>20492: los anuncios mid-roll que preceden al desplazamiento se reproducen antes de que el contenido se reanude desde el valor de desplazamiento.</td> 
   <td>IOS no admite la reproducción con desplazamiento.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Juego de trucos</td> 
   <td>El juego de trucos suave no funciona para emisiones que no tienen representaciones de iFrame.</td> 
   <td><p>· Las adaptaciones de Trick Play no son compatibles con Firefox e Internet Explorer y, por lo tanto, el modo de truco inverso no está disponible en estos navegadores.</p> <p>· El juego de trucos no está disponible cuando se reproduce contenido junto con anuncios.</p> <p>· 10435: Durante la reproducción de DASH, el vídeo se congela en el juego de truco hacia delante en Internet Explorer (Win 8.1)</p> <p>intermitentemente. Esto sucede porque utilizamos la propiedad playbackRate de los elementos de vídeo sin la adaptación trick play.</p> <p>14182: A veces, durante el rebobinado en el navegador Chrome, el evento de búsqueda puede no recibirse y, por lo tanto, el modo truco no funcionará.</p> <p>· 14942: Las tasas de reproducción se pueden establecer en Chrome para Android incluso en caso de emisiones de reproducción sin trucos, pero no se aplicará la configuración y la reproducción continuará a velocidad normal.</p> <p>· 17308: La búsqueda no funciona en el modo Trickplay.</p> <p>· 17309: En el navegador Chrome, el modo de truco inverso no se puede mantener durante más de 2 segundos.</p> <p>19272: Es posible que Trick Play no se recupere del almacenamiento en búfer en el navegador Windows 10 Edge en caso de emisiones DASH.</p> </td> 
   <td>El modo de truco de rebobinado no es compatible.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Análisis de ID3</td> 
   <td>20346: El SDK también debe devolver el byte de codificación de texto de los marcos ID3.</td> 
   <td><p>El SDK ignora las etiquetas ID3 disponibles en las secuencias de transporte de datos de audio (ADTS).</p> <p>· 12378: Los metadatos cronometrados de ID3 se analizan en momentos diferentes en el Flash y el navegador compatible con MSE, por lo que el comportamiento de visualización en la cronología del reproductor de referencia también es diferente.</p> <p>· 19247: El análisis de ID3 no es compatible con el marco de la interfaz de usuario.</p> </td> 
   <td><p>· 20323: Safari no analiza la etiqueta PRIV ID3 utilizada para indicar la marca de tiempo de la primera muestra del segmento aac (#32422733 de problemas de Safari)</p> <p>· 20350: En ciertos dispositivos (incluido MAC OS X 10.1, iPad10) Safari no proporciona un evento de cambio de señal cuando está en modo truco y, por lo tanto, no se reciben fotogramas ID3. (#32450526 de problema de Safari)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Compatibilidad con marcadores de discontinuidad</td> 
   <td> </td> 
   <td><p>· La inserción de anuncios en el lado del cliente no es compatible con flujos HLS que contengan discontinuidad.</p> <p>· El cambio de códec de audio no está permitido en las discontinuidades del flujo HLS.</p> <p>· El interruptor de pista de audio no es compatible con flujos HLS con marcadores de discontinuidad</p> </td> 
   <td>El número de secuencia de discontinuidad es un requisito para los flujos HLS con discontinuidad para la reproducción en Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 18: Características de protección de contenido**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción DASH)</strong></td> 
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
   <td><p>· 12660: El reproductor HTML5 genera un error interno del servidor por el contenido caducado del guión cifrado de PlayReady.</p> <p>· 16720: El contenido cifrado DASH DRM no funcionará si falta el atributo de inicio en la etiqueta de punto.</p> <p>· 18589: La reproducción no es compatible con transmisiones multiperíodo VoD de guiones protegidos por DRM con Xlink.</p> <p>· 18653: La reproducción del contenido de Widevine MultiPeriod con varias claves se detiene en el primer período y no puede cambiar al siguiente.</p> <p>· 18656: Reproducir Reproducción MultiPeriod Stream, cifrado con diferentes claves, no se reproduce.</p> <p>Playready 2.0 para Dash no está certificado.</p> <p> </p> <p> </p> </td> 
   <td>12602: El reproductor HTML5 actualiza repetidamente los metadatos DRM de HLS Fairplay en Safari</td> 
   <td><p>Se puede reproducir el contenido DRM de DASH Widevine empaquetado a través de Bento4. El contenido empaquetado a través del empaquetador sin conexión y el empaquetador Shaka no se reproduce. DASH PlayReady DRM no es compatible.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 19: Características principales del Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Pre/Mid/Post</td> 
   <td> </td> 
   <td><p>· Los anuncios previos a la emisión con contenido en directo de HLS se reproducen en modo de reproductor dual.</p> <p>· No se admiten anuncios DASH con contenido HLS ni anuncios HLS con contenido DASH.</p> <p>· 19002: Reproductor In HTML 5 con MSE adBreak. insertionType no devuelve el valor correcto para representar el tipo de inserción correcto, es decir, el cliente insertado y/o el servidor insertado.</p> <p>7794: En dispositivos móviles (iOS, Android con Chrome 33 o inferior o explorador nativo) donde la barra de control predeterminada es visible en modo de pantalla completa, la barra de búsqueda y los botones de avance rápido están disponibles cuando se reproduce el anuncio.</p> <p>· 11048: El cambio del anuncio al contenido en directo de HLS no se realiza sin problemas en el caso de las extensiones de fuentes de medios.</p> <p>· 16083: En Android 4.4 Chrome v52, a veces HLS y con contenido HLS pueden provocar un error de descodificación de canalización después de una reproducción estancada.</p> <p>· 16097: Los errores encontrados durante la pausa publicitaria no se gestionan, lo que puede hacer que el flujo principal detenga la reproducción.</p> <p>· 18095: Los anuncios MP4 no son compatibles con el contenido en directo de HLS.</p> <p>19120: Las búsquedas múltiples en anuncios HLS con contenido HLS pueden hacer que el flujo detenga la reproducción.</p> <p>· 19131: Es posible que se muestre una superposición de almacenamiento en búfer al cambiar del anuncio previo a la emisión al contenido.</p> <p>· 20296: En el caso de transmisiones en directo HLS, la búsqueda en la ventana DVR seguida de la búsqueda de más de rollos medios resueltos puede llevar a la detención de la reproducción.</p> <p>· 20298: Los flujos en directo de HLS con rollos medios se detienen en el momento en que se produce el primer rollo medio y salen de la ventana del DVR.</p> <p>· 20317: Los flujos en directo de HLS pueden paralizarse al cambiar al anuncio siguiente o del anuncio al contenido en caso de que la pausa publicitaria contenga más de un anuncio.</p> 
    <ul> 
     <li>Los anuncios de la ventana DVR de las transmisiones en directo de HLS no se resuelven.</li> 
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
   <td>Creative Repackers</td> 
   <td> </td> 
   <td>21464: La respuesta del anuncio se descarta por completo si el reempaquetado creativo falla en uno de los anuncios de la pausa publicitaria.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 20: Funciones avanzadas del Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de contenido</strong></td> 
   <td><strong>Función</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 en Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 en Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo reproducción DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Solo anuncio</td> 
   <td> </td> 
   <td>20056: La propiedad de tecnología del reproductor no es relevante, ya que se basa en el contenido principal, que está vacío en caso de reproducción de solo anuncio</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Activo</td> 
   <td>Política de publicidad personalizada</td> 
   <td> </td> 
   <td><p>· Los comportamientos publicitarios no son compatibles con los anuncios MP4 ni con el contenido MP4.</p> <p>· 13973: Comportamientos de publicidad personalizados: la política de OMISIÓN no emite un evento completo cuando se utiliza con MSE.</p> <p>· 14939: Las políticas de comportamiento de publicidad personalizadas para omitir y omitir una pausa publicitaria no funcionan para el contenido de DASH.</p> <p>· 17131: El primer fotograma del anuncio es visible y, en caso de que se omita la política de pausas publicitarias, el contenido se reanuda.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Anuncios complementarios/ anuncios de banner/ Anuncios en los que se puede hacer clic</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Los anuncios de banner no están visibles al utilizar el reproductor de referencia.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· Los comportamientos publicitarios no son compatibles con los anuncios VPAID.</p> <p>· 15032: No se admiten anuncios VPAID en combinación con anuncios MP4 o HLS en una pausa publicitaria.</p> <p>· 19001: En Android y iOS, cuando se reproduce un anuncio VPAID con MP4, como contenido principal, se pueden escuchar dos pistas de audio, una de contenido principal y otra de publicidad.</p> <p>· 20762: Los anuncios VPAID no son compatibles con Imagen en imagen (PIP).</p> <p>· 21172: El evento Reproducir completo no se recibe para el contenido de VOD de HLS con anuncios VPAID.</p> <p>· 21173: onAdBreakCompleteEvent no se recibe para el contenido de VOD de HLS ni para los anuncios VPAID posteriores a la emisión.</p> </td> 
   <td>El reproductor cambia entre el modo normal y el modo de pantalla completa al cambiar entre el anuncio VPAID y el contenido principal.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabla 21: Integraciones**

| **Tipo de contenido** | **Función** | **Flash** | **HTML5 en Firefox, IE, Chrome, Android Chrome** | **HTML5 en Safari, iOS Safari** | **Chromecast (solo reproducción DASH)** |
|---|---|---|---|---|---|
| VOD + Activo | Integración de VHL de Adobe Analytics |  | 19004: El seguimiento de Video Analytics no está disponible a través de la herramienta de configuración de la interfaz de usuario. |  |  |

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
