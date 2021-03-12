---
title: Notas de la versión de TVSDK 3.13 para iOS
description: Las notas de la versión de TVSDK 3.13 para iOS describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de los dispositivos en TVSDK iOS 3.13.
translation-type: tm+mt
source-git-commit: d1cf8a05172c04655c8a7c76ce116c8f7be61ec9
workflow-type: tm+mt
source-wordcount: '7713'
ht-degree: 0%

---


# Notas de la versión de TVSDK 3.13 para iOS {#tvsdk-for-ios-release-notes}

Las notas de la versión de TVSDK 3.12 para iOS describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de los dispositivos en TVSDK iOS 3.12.

## Requisitos del sistema y software {#system-software-requirements}

Antes de descargar iOS 3.12, asegúrese de que las versiones de hardware, sistema operativo y aplicación cumplen los siguientes requisitos:

Sistema operativo: iOS 8.0 o posterior.

## iOS TVSDK 3.13

La versión incorpora compatibilidad con los anuncios DEMUXED &#39;HLS/CMAF&#39; (preroll, midroll y postroll) para emisiones en directo, VOD y FER.

Para ver las correcciones de los problemas notificados por los clientes, consulte [Problemas resueltos](#resolved-issues). Para ver las limitaciones, consulte [problemas conocidos y limitaciones](#known-issues-and-limitations).

### Nuevas funciones y correcciones en las versiones anteriores {#whats-new-previous}

**iOS TVSDK 3.12**

Se ha corregido un problema en el cual la emisión en directo fallaba tras 15 minutos de reproducción.

**iOS TVSDK 3.11**

Se han proporcionado correcciones para problemas de clientes en los que `isFallbackOnInvalidCreativeEnabled` y el método `customParams` causan que la aplicación se bloquee.

**iOS TVSDK 3.10**

* Se ha corregido un problema en el cual el reproductor TVSDK no activa la notificación `PTMediaPlayerStatusError` cuando la red no está disponible.

**iOS TVSDK 3.9**

* Se ha corregido un problema por el cual los subtítulos de VTT no se reproducían, lo que ocasionaba el bloqueo de la aplicación.

* iOS TVSDK 3.9 incluye el certificado de transporte personalizado actualizado.

**Corrección TVSDK 3.8.0.83 de iOS**

La corrección tenía el certificado de transporte individualizado actualizado.

**iOS TVSDK 3.8**

Cumplimiento de iOS 13 y desaprobación de la API de iOS 13 UIWebView administrada.

**iOS TVSDK 3.7**

Revisión para un escenario en el que la reproducción se detuvo cuando se realizó simultáneamente un gran número de solicitudes de resolución de anuncios.

**iOS TVSDK 3.6**

**Correcciones en la propiedad vastoXML de la clase`PTNetworkAdInfo`**

La propiedad vastoXML no se estaba configurando correctamente y devolvía un valor nulo.

**iOS TVSDK 3.5**

**Habilitación del audio de fondo**

*Configure la aplicación para que continúe reproduciendo audio cuando entre en segundo plano.*

Para habilitar esta función, es necesario establecer la nueva API `audioPlaybackInBackground` añadida en la clase PTMediaPlayer. Con esta API habilitada, la aplicación está lista para reproducir audio de fondo.

**iOS TVSDK 3.4.0.19 (revisión)**

Esta versión tiene una solución para los bloqueos de aplicaciones que se producen en un escenario de failover de anuncios.

**iOS TVSDK 3.4**

**Tiempo de espera de resolución de publicidad**

* Con TVSDK 3.4, los usuarios ahora pueden establecer el valor de tiempo de espera para la resolución general de anuncios y las descargas de manifiesto. Si dentro de un tiempo de espera determinado algunos anuncios no    resuelto, TVSDK reproducirá los anuncios restantes.

* PTAdMetadata: La API adRequestTimeout se ha desaprobado y se eliminará. El valor predeterminado se ha establecido en 35 segundos.

* Se han introducido dos nuevas API alternativas en PTAdMetadataClass: adResolutionTimeout: tiempo de espera para las llamadas generales de resolución de anuncios                adManifestTimeout : tiempo de espera para las descargas de manifiesto de publicidad.

**Optimización de ingresos**

Se ha habilitado TVSDK para que identifique las áreas de problema relacionadas con los flujos de trabajo de inserción de publicidad y para que informe del punto final de elección de Analytics.

**Versión 3.3**

TVSDK 3.3 ahora es compatible con el SDK para iOS 11. Todas las API obsoletas se han sustituido por alternativas adecuadas.

**Versión 3.2**

**Compatibilidad con registros adicionales (fase 2)**

Se ha agregado compatibilidad con notificaciones de error en caso de:

* La versión HLS del anuncio utiliza un nivel mayor que el contenido.

* Se excluye la variante de solo audio.

* Error en la solicitud VAST/VMAP.

**Versión 3.1**

* **Compatibilidad con registros adicionales**
Se ha agregado compatibilidad con notificaciones descriptivas en caso de errores de reproducción de anuncios.

* **Se ha agregado compatibilidad con la emisión de CMAF cifrada de Fairplay**
Ahora se admiten las transmisiones de CMAF cifradas de Fairplay con reproducción de códec AVC.

**Versión 3.0.1**

Esta versión no incorpora nuevas funciones ni mejoras.

**Versión 3.0**

* TVSDK 3.0 es compatible con flujos HEVC.

* Justo en el tiempo: resolución de anuncios más cerca de los marcadores de publicidad.

Se ha agregado la propiedad `enableDelayAdLoading` del tipo booleano en la interfaz de nivel de aplicación para habilitar JIT. Si `enableDelayAdLoading` es NO, `setadMetadata.delayAdLoading`pasará a ser True (propiedad de la interfaz PTAdMetadata).

Con esta propiedad habilitada, TVSDK resuelve cada pausa publicitaria antes de su posición en función del valor de tolerancia definido. De forma predeterminada, `delayAdTolerance` se establece en 5 segundos.

**Versión 1.4.45**

Para cumplir con Xcode10, TVSDK se ha trasladado de &quot;`libstdc++`&quot; a &quot;`libc++`&quot; y, como resultado, la versión mínima admitida es iOS 7. Anteriormente era iOS 6.

**Versión 1.4.44**

Esta versión no incorpora nuevas funciones ni mejoras.

**Versión 1.4.43**

* Experiencia parecida a la TV de poder unirse en medio de un anuncio sin activar el seguimiento parcial del anuncio.\
   Ejemplo: El usuario se une en el medio (a los 40 segundos) de una pausa publicitaria de 90 segundos que consta de tres anuncios de 30 segundos. Pasarán 10 segundos desde el segundo anuncio de la pausa.

   * El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.
   * Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Los rastreadores solo para el tercer anuncio se activan.

* Se ha agregado la propiedad enableVodPreroll del tipo booleano en la interfaz PTAdMetadata . La propiedad se puede utilizar para habilitar la emisión previa en un flujo VoD. Si enableVodPreroll es NO, PSDK no reproduce el anuncio previo a la emisión. Sin embargo, esto no afecta a los midrolls. El valor predeterminado de enableVodPreroll es YES.
* la API closedCaptionDisplayEnabled de la interfaz PTMediaPlayer está marcada como obsoleta a partir de iOS v1.4.43. Para determinar si hay subtítulos cerrados disponibles para un PTMediaPlayerItem determinado, examine la propiedad subtitlesOptions de PTMediaPlayerMediaItem.

**Versión 1.4.42**

Esta versión no incorpora nuevas funciones. Para obtener una lista de los problemas corregidos, consulte [Problemas resueltos](#resolved-issues).

**Versión 1.4.41**

Cambios en la API:

* **isSecure**: Se ha introducido una nueva API isSecure para garantizar que el reproductor no grabe ni genere un error. El valor predeterminado es true.

* **allowExternalRecording**: Se ha introducido una nueva API para permitir la duplicación de reproducción de contenido seguro. El espejado de reproducción de aire se trata como una grabación, por lo tanto `allowExternalRecording` el valor debe establecerse en `True`, para permitir el espejado de reproducción de aire o debe establecerse en `False` para detener el espejado de reproducción de aire para contenido seguro. De forma predeterminada, `value` es verdadero.

**Versión 1.4.40**

No hay nuevas funciones.

**Versión 1.4.39**

* iOS TVSDK está certificado con VHL 2.0.1 y con VHL 2.0.1 con Nielsen.

* El TVSDK de iOS se actualiza para realizar solicitudes CRS desde el nuevo host de Akamai `primetime-a.akamaihd.net`.

* La nueva configuración de nombre de host proporciona la entrega de recursos CRS a través de HTTP y HTTPS (SSL) a buena escala.

**Versión 1.4.36**

Integración y certificación de VHL 2.0 en iOS TVSDK : Reduzca la barrera en la implementación `VideoHeartbeatsLibrary` disminuyendo la complejidad de las API.

**Versión 1.4.34**

**Información de publicidad de red**

Las API de TVSDK ahora proporcionan información adicional sobre respuestas VAST de terceros. El ID de anuncio, el sistema de publicidad y las extensiones de publicidad VAST se proporcionan en la clase `PTNetworkAdInfo` accesible a través de la propiedad `networkAdInfo` en un recurso de publicidad. Esta información se puede utilizar para la integración con otras plataformas de Ad Analytics, como **Moat Analytics**.

**Versión 1.4.31**

* **Métricas** de facturaciónPara dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de a una tasa fija independientemente del uso real, los Adobes recopilan métricas de uso y utilizan estas métricas para determinar cuánto facturar a los clientes.

   Cada vez que TVSDK genera un evento de inicio de flujo, el reproductor comienza a enviar mensajes HTTP periódicamente al sistema de facturación del Adobe. El periodo, conocido como duración facturable, puede ser diferente para VOD estándar, VOD pro (anuncios mid-roll habilitados) y contenido activo. La duración predeterminada de cada tipo de contenido es de 30 minutos, pero el contrato con Adobe determina los valores reales.

* **Compatibilidad con varias CDN para CRS** AdsTVSDK ahora es compatible con Multi-CDN para anuncios CRS. Al proporcionar detalles de FTP para los anuncios CRS, puede especificar ubicaciones de CDN que no sean la CDN propiedad de la Adobe predeterminada, como Akamai.

**Versión 1.4.29**

En la clase `PTSDKConfig` se ha añadido la API forceHTTPS.

La clase `PTSDKConfig` proporciona métodos para aplicar SSL en las solicitudes realizadas a los servidores de Adobe Primetime de toma de decisiones de anuncios, DRM y Video Analytics. Para obtener más información, consulte los métodos `forceHTTPS` y `isForcingHTTPS` en esta clase. Si se carga un manifiesto a través de HTTPS, TVSDK conserva el uso de contenido de HTTPS y respeta este uso al cargar cualquier URL relativa de ese manifiesto.

>[!NOTE]
>
>Las solicitudes para dominios de terceros, como píxeles de seguimiento de anuncios, URL de contenido y anuncios y solicitudes similares, no se modifican, y es responsabilidad de los proveedores de contenido y los servidores de publicidad proporcionar direcciones URL compatibles con HTTPS.

**Versión 1.4.18**

Primetime iOS TVSDK ahora es compatible con los creativos de Javascript VPAID 2.0 para permitir una experiencia de publicidad interactiva y enriquecida en el flujo. Para obtener más información sobre VPAID 2.0, consulte Compatibilidad con anuncios VPAID.

**Versión 1.4.17**

* tvOS

   TVSDK es compatible con aplicaciones nativas de tvOS.
* Se pueden reproducir los siguientes tipos de contenido:

   * VOD
   * Activo
   * AES-128
   * Audio y subtítulos alternativos
   * FER

* Se pueden mostrar los siguientes tipos de publicidades:

   * Básico
   * VAST2
   * VAST3
   * VMA

* Actualmente no se admiten las siguientes funciones:

   * Digital Rights Management (DRM)
   * Pancartas publicitarias
   * Lenguaje de marcado de TV (TVML)

**Versión 1.4.13**

>[!NOTE]
>
>El módulo de Nielsen se ha eliminado de la compilación de TVSDK, el TVSDK se actualizará próximamente con un nuevo módulo de integración de Nielsen.

**Abandono de anuncios, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103)**

En el caso de los anuncios VAST (creativos) con la regla de reserva habilitada, TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta utilizar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva. Para obtener más información, consulte Reversión de anuncios para anuncios VAST y VMAP.

**Versión 1.4.9**

**Señalización de interrupción con sustitución de contenido alternativo**

Como parte de la actualización 1.4 de TVSDK, ahora también admitimos entrar y volver de las interrupciones regionales contra contenido lineal. Ahora, el TVSDK puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de bloqueo incluso cuando se muestra una programación alternativa en lugar de la programación original.

**Versión 1.4.8**

**Video Heartbeats Library (VHL) actualizado a la versión 1.5**

* Capacidad para enviar metadatos con el inicio de vídeo o el inicio de vídeo/anuncio/capítulo como datos de contexto.

* Menos tráfico de red: los latidos son menos en promedio y de menor tamaño.

**Versión 1.4.7**

* **Compatibilidad de individualización local**

Compatibilidad con instalaciones locales del servidor de individualización de Adobe para personalizar la solicitud de personalización del cliente para ir a un punto final diferente.

* **Protección de salida basada en resolución**

Las directivas de DRM ahora pueden especificar la resolución más alta permitida, según las capacidades de protección de salida del dispositivo. Por ejemplo, &quot;Si HDCP está disponible, permita que se reproduzca contenido de hasta 1080p resolución, y si HDCP no está disponible, permita que se reproduzca contenido de hasta 480p resolución&quot;.

**Versión 1.4.4**

* **Actualización de la biblioteca Video Heartbeats Library (VHL) a la versión 1.4.1.1**

   * Se ha agregado la capacidad de agrupar diferentes casos de uso de análisis, de otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos `trackAdBreakStart` y `trackAdBreakComplete`. La pausa publicitaria se infiere de las llamadas de método `trackAdStart` y `trackAdComplete` .
   * La propiedad `playhead` ya no es necesaria al rastrear anuncios.
   * Se ha agregado compatibilidad con el ID de visitante de Marketing Cloud.

* **Integración del SDK de Nielsen**

Ahora, TVSDK admite el envío de señalizaciones mTVR e ID3 de MDPR al SDK de Nielsen sin ninguna integración personalizada. Para empezar, descargue el SDK de la aplicación para iOS 3.1.2.19 de Nielsen y siga las instrucciones que se encuentran aquí en la Guía del programador de iOS.

**Versión 1.4.0**

* **Señalización de interrupción con sustitución de contenido alternativo**

Como parte de la actualización 1.4 de TVSDK, ahora TVSDK también admite entrar y volver de las interrupciones regionales en el contenido lineal. Ahora, el TVSDK puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de bloqueo incluso cuando se muestra una programación alternativa en lugar de la programación original.

* **Eliminar/reemplazar anuncios C3**

Ahora, no se necesita ningún trabajo previo adicional para insertar de forma dinámica nuevos anuncios en recursos de vídeo bajo demanda (VOD) que salen de la ventana C3. El SDK de TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar de forma dinámica nuevos anuncios. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se emite durante la emisión y se baja inmediatamente para utilizarlo como contenido bajo demanda sin el tiempo adecuado para &quot;limpiar&quot; el recurso.

## Problemas resueltos {#resolved-issues}

Cuando la resolución está asociada a un problema registrado, se muestra una referencia de Zendesk, por ejemplo ZD#xxxxx.

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOS TVSDK 3.13**

* (ZD 42085): Problemas con la reproducción en flujos CMAF.

* (ZD-43215): Se bloquea al descartar el reproductor mientras un anuncio está en curso.

* (ZD 43210): la reproducción de iOS HLS se bloquea cuando el subtítulo WebVTT está habilitado.

**iOS TVSDK 3.12**

* La emisión en directo falla tras 15 minutos de reproducción al utilizar TVSDK para iOS 3.10.

### Problemas resueltos en versiones anteriores {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - El `isFallbackOnInvalidCreativeEnabled` hace que la aplicación se bloquee.

* (ZD#41289) - `NSInvalidArgumentException` se observa con el método `customParams` que provoca el bloqueo de la aplicación.

**iOS TVSDK 3.10**

(ZD#40943) - El reproductor TVSDK no activa la notificación PTMediaPlayerStatusError cuando la red no está disponible.

**iOS TVSDK 3.9**

(ZD#40272): El SDK para iOS no reproduce los subtítulos VTT con el error 101001 y provoca la congelación de la aplicación.

**iOS TVSDK 3.8**

* (ZD#40087): iOS se bloquea con un error del reproductor en el contenido de VOD caducado.

* (ZD#40083) - Los anuncios pre-roll no se reproducen para emisión en directo con `OpportunityGenerator` y el reproductor da error.

* (ZD#39828): a la propiedad `CurrentItem` le falta la anotación de incapacidad, lo que provoca el bloqueo del reproductor cuando el estado del reproductor contenido en la notificación es `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961): El contenido no se reproduce en la ventana Imagen en imagen (PiP) después de que un contenido termina de reproducirse, cuando se configura la reproducción de varios contenidos en el PiP.

**iOS TVSDK 3.6**

No hay problemas nuevos en esta versión.

**iOS TVSDK 3.5**

No hay problemas nuevos en esta versión.

**Versión 3.3**

(ZD#37820) : se ha añadido una lista de permitidos para el encabezado personalizado HS-Id, HS-SSAI-TAG.

**Versión 3.2**

* **Ticket#36588** : se observa un bloqueo del reproductor cuando se llama al método MediaPlayer STOP.

Se ha corregido un bloqueo intermitente observado cuando se llama al método STOP para algunos flujos con subtítulos.

* **ticket#37080** : solicitudes duplicadas vistas para llamadas de manifiesto.
Se han corregido las solicitudes duplicadas realizadas para las direcciones URL de manifiesto durante la reproducción. TVSDK ahora realiza una llamada por manifiesto.

* **ticket#37**  - La regla de normalización CRS falla con el tipo de coincidencia eq Se ha corregido un caso en el que el reproductor se bloqueaba cuando se encontraba con el último conjunto de reglas de normalización para nombres de host con un tipo de coincidencia &quot;eq&quot;.

**Versión 3.1**

**Vale #36313** : resultados impredecibles intermitentes durante las pausas publicitarias lineales Se ha corregido la reproducción intermitente durante las pausas publicitarias lineales en la emisión en directo.

**Versión 3.0.1**

**Ticket36948**  - CRS - Orden de selección de recursos incoherente en iOS 12 El recurso seleccionado para CRS no siempre es la variante de mayor calidad devuelta en una respuesta VAST o VMAP.

**Versión 3.0**

* **Ticket35311** : el estado del reproductor no se PONE EN PAUSA durante una interrupción de llamada telefónica. Se ha agregado un controlador de interrupción para impedir que el reproductor interrumpa. Al interrumpirse, el estado del reproductor se PAUSA y, a continuación, reanuda la reproducción al hacer clic en el botón de reproducción.

* **Ticket36685**  - Activos activos - El tiempo no coincide con el progreso del tiempo del reproductor y la hora del marcador SCTE El tiempo correcto se calcula para los marcadores SCTE que están por encima del punto activo.

* **Ticket36492** -  `currentTime` y  `localTime` no se actualizan cuando se busca una nueva posición durante el estado en pausa El tiempo actual del reproductor se puede establecer en cero en caso de que el reproductor esté en estado pausado; antes, el tiempo actual se establecía en cero solo en estado de reproducción.

**Versión 1.4.45**

* **Ticket36294** : iOS TVSDK no funciona con Xcode 10 Se han corregido los problemas de compilación con TVSDK en XCode 10. Debido a los requisitos de XCode 10, las aplicaciones creadas en TVSDK para iOS 1.4.45 y posteriores requieren un destino de implementación mínimo como iOS 7.0

* **Ticket36321**  - Discrepancia observada en rango buscable entre  `PTMediaPlayer` y la  `AVPlayer` instancia en estado &quot;Reproduciendo&quot;.

* **Ticket36493** :  `libstdc++` compatibilidad con iOS 12 Se han corregido los problemas de compilación con TVSDK en iOS 12. Las aplicaciones creadas en TVSDK para iOS 1.4.45 y posteriores requieren un objetivo de implementación mínimo como iOS 7.0

**Versión 1.4.44**

* **Ticket34683** : El Tiempo De Progreso De La Reproducción Del Anuncio Es Negativo

Se han añadido comprobaciones adicionales para controlar el caso cuando hay una discordancia entre la duración indicada por el servidor de publicidad y el contenido publicitario real.

* **Ticket34801** : currentTime y localTime no se actualizaban cuando se buscaba una nueva posición durante el estado pausado El tiempo actual del reproductor se puede establecer en cero en caso de que el reproductor esté en estado pausado; antes, el tiempo actual se establecía en cero solo en estado de reproducción.

* **Ticket35037** : se bloquea la reproducción con una dirección URL incorrecta al volver de la inserción de anuncios basada en señales.
Se ha mejorado la corrección proporcionada para el problema cerrado n.º 34385 de la versión 1.4.42. Se ha agregado el código de control de excepciones y comprobaciones isCanceled para que la cola de operaciones sea más robusta.

**Versión 1.4.43**

* (ZD#32990) - iOS: Se reproduce el contenido en lugar de los anuncios en algunos puntos de referencia. `selectedMediaOptionInMediaSelectionGroup` La API que formaba parte de la interfaz AVPlayerItem ahora se ha movido a AVMediaSelection en iOS 11. El problema se resolvió con esta nueva API.

* (ZD#33683) TVSDK eliminado == sufijo de las cadenas de metadatos. El problema se corrige en la lógica de análisis.

* (ZD#33905) : TVSDK de iOS realiza llamadas a los archivos de manifiesto con dos agentes de usuario. El problema del agente de usuario se ha corregido en la primera llamada m3u8 (nuevo caso de instalación). Los M3u8 tienen los mismos agentes de usuario para todas las llamadas ahora.

* (ZD#34293): Los anuncios insertados en flujos LINEAR no se reproducen correctamente en iOS11. El problema se ha corregido para los anuncios previos a la publicación.

* (ZD#34684) : cuando se aplica la directiva de omisión de publicidad, los fotogramas de anuncio pre-roll se muestran durante unos segundos. Se ha introducido una nueva API, enableVodPreroll , para deshabilitar la reproducción previa en la reproducción del vod. El valor predeterminado de esta API es &quot;Sí&quot;. La API garantiza la omisión de la vinculación del contenido de la publicidad en el contenido principal.

* (ZD#34765) : después de llamar a stop(), pocos segmentos de Transmisiones de transporte se siguen descargando. Se ha mejorado la API Stop() para evitar la descarga de segmentos adicionales.

* (ZD#34865): los anuncios previos a la emisión para emisión en directo se truncan en iOS. En relación con iOS11, y al agregar una comprobación adicional para confirmar si el flujo es previo a la emisión o contenido principal, se soluciona este problema.

* (ZD#35093) : se ha corregido un escenario de conmutación por error en el que, si la variante principal del flujo falla al iniciarse (devuelve 404), la reproducción no cambia al flujo de copia de seguridad.

**1.4.42 (1.4.42.118)**

* (ZD#34385) : La reproducción se detiene con una dirección URL incorrecta al volver de la inserción de anuncios basada en señales.

   Aumente los recuentos simultáneos máximos de `CustomAVAssetLoaderOperations`, de modo que las lecturas de manifiesto puedan continuar ejecutándose.

* (ZD#34373) - Los usuarios finales no pueden retransmitir a dispositivos conectados HDMI cuando no se permite la grabación de flujo.

* (ZD#32678): TVSDK no recopila los ID de anuncio correctos en iOS.

   El ID de anuncio del creativo de anuncio final ahora se recoge en pings VHL en caso de redirecciones VAST/VMAP.

* (ZD#33904): TVSDK no está registrado para las notificaciones de AVFfoundation `AVAudioSessionMediaServicesWereLostNotification` y `AVAudioSessionMediaServicesWereResetNotification`.

   `PTMediaServicesWereLostNotification` y ahora se  `PTMediaServicesWereResetNotification` puede registrar en la aplicación del reproductor para obtener las notificaciones cuando se restablecen o pierden los servicios de medios.

* (ZD#33815) : los clientes no pueden actualizar sus reglas de CRS de priorización y normalización sin requerir una actualización de la aplicación.

   Se han añadido las API `getCRSRulesJsonURL` y `setCRSRulesJsonURL` al SDK para iOS TVSDK .

**Versión 1.4.41 (1.4.41.76)**

* (ZD #34464): Creación de problemas de la aplicación de referencia con TVSDK versión 1.4.41

   A partir de esta versión, Xcode 9 es necesario para compilar TVSDK para iOS.
* (ZD #29456) - El juego aéreo empieza en estado pausado

   Se ha corregido el problema de pausa que se producía cuando el vídeo se pausaba al entrar en la reproducción.
* (ZD #30371) - Cambios en la hora de inicio de AdBreak cuando insertamos más de 2 anuncios en flujo lineal

   Se ha corregido el error al intentar reproducir contenido en Apple TV, que impedía que se reprodujera completamente
* (ZD #32146): no se recibe ningún `PTMediaPlayerStatusError` para el contenido de HLS Live sobre el bloqueo de iOS 11 dev beta

   No se recibe ningún `PTMediaPlayerStatusError` para el contenido de HLS Live y VOD al bloquear mediante Charles (Borrar conexión y 403).

* (ZD #29242): La reproducción de vídeo de reproducción de Airplay falla con los anuncios activados.

   Cuando los anuncios están habilitados y AirPlay está habilitado para iniciar la reproducción de un vídeo, la reproducción de vídeo nunca se inicia y no se muestra ningún error.

* (ZD#33341) - `DRMInterface.h` déclencheur genera advertencias en Xcode 9.

   Se corrigieron dos prototipos de bloque en `DRMInterface.h` que faltaban la palabra &quot;void&quot; en sus listas de parámetros.

* (ZD#31979): No se compila ni ejecuta cuando es iOS 10 o posterior para iPhone 7/iPhone7+.

   Se ha corregido la compilación de documentos IB para versiones anteriores a iOS 7, que ya no es compatible.

* (ZD#32920) - Pantalla en blanco dentro de una pausa publicitaria y sin finalización de pausa publicitaria.

   Cuando una pausa publicitaria presenta instancias de anuncio y una vez finalizada una instancia de anuncio, se muestra una pantalla en blanco.

* (ZD#32509) - Desactivar la grabación de pantalla de iOS 11 Desactivar la grabación de pantalla en iOS 11.

* (ZD#33179) - Fallo de evento intermitente en iOS11.

   Se ha corregido el error de evento en iOS 11.

**Versión 1.4.40**  (1.4.40.72)

* (ZD #32465): El reproductor no puede gestionar listas de reproducción combinadas.

   Invoque `finishLoadingWithError`(con: Error) para la base AV para probar flujos alternativos/conmutación por error de déclencheur.

* (ZD #31951) - Error de TVSDK durante las rotaciones de licencia.

   Se ha corregido el problema de rotación de la licencia.
* (ZD #31951) - Pantalla en blanco dentro de una pausa publicitaria y sin finalización de pausa publicitaria.

   Se ha corregido un problema por el cual los anuncios VPAID de Facebook a menudo devolvían varios bloques CDATA en un único nodo VAST `<AdParameters>`.
* (ZD #33336) - iOS TVSDK - Las pods de anuncios no se rellenan, a pesar de que Freewheel devuelve suficientes anuncios.

   Se ha creado una relación principal-secundario entre el anuncio de secuencia y el anuncio de reserva, y se ha ordenado según la secuencia principal y el índice.

**Versión 1.4.39**  (1.4.39.43)

* (ZD #32178): La versión de iOS TVSDK es incorrecta.

   El resultado de la versión de TVSDK en los archivos de registro era 1.0.211. Se ha corregido para obtener la versión correcta.

* (ZD #32199) - Carga de publicidad diferida - El vídeo no se muestra para el contenido.

   La línea de tiempo de Adbreak local que no se inicializaba anteriormente, ahora se actualiza antes de su uso.

* (ZD #27528): el vídeo, el audio o ambos se congelan de 1 a 45 segundos después de que se inicie la reproducción de un recurso, si el audio secundario está establecido en no predeterminado en iOS 1.2.

   Prepare e informe las pistas de audio en estado Preparado.

* (ZD #30411) - Puede obtener resultados inesperados como sin audio o audio incorrecto, si elige un idioma Sap secundario.

   Prepare e informe las pistas de audio en estado Preparado.

* (ZD #32199) - Carga de publicidad diferida - El vídeo no se muestra para el contenido.

   La línea de tiempo de Adbreak local que no se inicializaba anteriormente, ahora se actualiza antes de su uso.

* (ZD #27528): el vídeo, el audio o ambos se congelan de 1 a 45 segundos después de que se inicie la reproducción de un recurso, si el audio secundario está establecido en no predeterminado en iOS 1.2.

   Prepare e informe las pistas de audio en estado Preparado.

* (ZD #30411) - Puede obtener resultados inesperados como sin audio o audio incorrecto, si elige un idioma Sap secundario.

   Prepare e informe las pistas de audio en estado Preparado.

**Versión 1.4.38**  (1.4.38.860)

* (ZD #29281) - iOS: Añadir AdSystem y Creative Id a solicitudes CRS

Uso de Creative Id y AdSystem en solicitudes CRS basadas en reglas de normalización CRS

* (ZD #29176) - Bloqueo en `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

Ahora se gestiona el bloqueo debido a AdBreak vacío.

* (ZD #30125): Los anuncios programáticos no funcionan en la plataforma iOS

Se ha agregado compatibilidad con anuncios programáticos en iOS.

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME Notification

El evento de metadatos temporizados no se activa para la etiqueta # EXT-X-PROGRAM-DATE-TIME con emisiones LIVE DRM.

**Versión 1.4.37 (1.4.37.842)**

* (ZD #28950 ): Problema de reproducción de VOD

Problema de reproducción cuando la etiqueta # EXT-X-PLAYLIST-TYPE en el flujo se establece en Event en lugar de VOD

* (ZD #29281) - iOS: Añadir AdSystem y Creative Id a solicitudes CRS

Uso de Creative Id y AdSystem en solicitudes CRS basadas en reglas de normalización CRS.

* (ZD #29462) - Anuncio de TremorHub en A&amp;E VOD que provoca un bloqueo en aplicaciones iOS

**Versión 1.4.36 (1.4.36.835)**

* (ZD #29418): Los avisos con duración 0 (#EXT-X-CUE-OUT:0.000) están provocando que el TVSDK de iOS detenga o bloquee la reproducción.

El problema se ha corregido y la reproducción se inicia correctamente.

* (ZD #29462): Anuncio en VOD que provoca un bloqueo en iOS TVSDK .

El problema se ha solucionado. iOS TVSDK está generando un `exception(AUDNetworkAdInfo::initWithAdId)` y no lo está manejando. La excepción se debe a un ID de anuncio vacío.

* (ZD #29281) - Añadir AdSystem y el ID creativo a las solicitudes CRS.

Incluya AdSystem y CreativeId como nuevos parámetros en las solicitudes 1401 y 1403 (todos los demás parámetros siguen siendo los mismos).

**Versión 1.4.35**  (1.4.35.830)

* (ZD #27830): Es necesario determinar mediante programación la diferencia entre subtítulos y subtítulos en iOS.

TVSDK ahora expone los dos tipos que se pueden usar para filtrar el tipo de subtítulo requerido.

* (ZD #29160) - Las señales de anuncios EXT-X-CUE-OUT no se duplican correctamente en TVSDK iOS.

Con el anuncio de midroll EXT-X-CUE-OUT se está reproduciendo ahora.

* (ZD #29100): La aplicación se bloquea cuando el usuario se desplaza hasta el final de una película.

Se han corregido varios bloqueos relacionados con la sincronización.

* (ZD #28785), (ZD #27712) y (ZD #25076) - La aplicación de iOS se está bloqueando durante los grandes eventos en directo.

Se han corregido varios bloqueos relacionados con la sincronización.

**Versión 1.4.34**  (1.4.34.815 para iOS 6.0+)

* (ZD #28481) - Interrupción de FER debido a que la clave incorrecta se añade al final de una pausa publicitaria para esos flujos FER

Para un flujo FER, la clave antes de la pausa publicitaria se inserta después del final de la pausa publicitaria. Este problema se resolvió adjuntando la *última clave vista* al final de la pausa publicitaria.

**Versión 1.4.33**  (1.4.33.803 para iOS 6.0+)

* (ZD# 21701) Habilitar CRS para subcuentas

Habilitado enviando la URL creativa original para la solicitud CRS 1401 en lugar de la URL normalizada, según el requisito del back end CRS.

* (ZD# 26218) - Problema de carga de PSDKResources.bundle

Este problema se ha resuelto actualizando la carga de recursos para que se vean desde todos los paquetes disponibles.

* (ZD# 27460) Llamada de primer anuncio de anuncio de anuncio de anuncio intermedio: POST a `cdn.auditude.com` que devuelve 403.

La nueva cuenta de CDN no puede gestionar una solicitud de CDN de POST. Este problema se resolvió actualizando el código para que la solicitud de publicidad `cdn.auditude.com` sea GET en lugar de POST.

**Versión 1.4.32**  (1.4.32.792 para iOS 6.0+)

* (ZD# 27132) Compatibilidad con valores decimales para las pausas publicitarias VMAP.

Cuando el contenido no se segmentaba a lo largo de las pausas publicitarias definidas, los enteros causaban colocaciones de anuncios inesperadas. El problema se resolvió al no convertir los valores decimales en enteros.

* (ZD# 27189) El contenido AES con la etiqueta EXT-X-DISCONTINUITY-SECQUENCE no se reproduce correctamente.

El problema se resolvió colocando la etiqueta al principio de la lista de reproducción.

**Versión 1.4.31**  (1.4.31.785 para iOS 6.0+)

* (ZD# 24528) Implementar métricas de uso de TVSDK para la facturación

Para obtener más información, consulte [Métricas de facturación].

* (ZD# 24642) Compatibilidad con imágenes en imagen para TVSDK

Se ha corregido la función de imagen en imagen, que en algunos casos no funcionaba correctamente.

* (ZD# 25246) Señales de pausa publicitaria incorrectas

Este problema se resolvió alineando etiquetas de discontinuidad entre manifiestos de variante.

* (ZD# 26218) El proceso de compilación de la aplicación se complica al intentar incluir PSDKLibrary.framework en el marco de aplicaciones del cliente

Este problema se resolvió empaquetando el archivo PSDKLibrary.framework como se solicitó.

* (ZD# 26364) Compatibilidad con varias CDN para anuncios CRS

Para obtener más información, consulte Compatibilidad con varias CDN para la entrega de anuncios CRS.

* (ZD# 27028) Retraso en la reproducción de algunos flujos en iOS 10.

Este problema se ha resuelto proporcionando una solución alternativa para las emisiones que no tienen una extensión M3U8.

**Versión 1.4.30**  (1.4.30.754 para iOS 6.0+)

En esta versión se han resuelto los siguientes problemas para TVSDK:

* (ZD# 24180) Agregue un encabezado personalizado a la lista de permitidos.

Se ha añadido un nuevo encabezado personalizado a la lista de permitidos TVSDK.

* (ZD# 25016) El flujo de conmutación por error se selecciona aleatoriamente cuando se establecen los parámetros de control de ABR

Este problema se resolvió manteniendo los flujos ABR en orden cuando la configuración de ABR se proporciona con la configuración initialBitrate en un flujo que incluye direcciones URL de conmutación por error. Esto evitará reproducir los flujos de failover en lugar de los principales.

* (ZD# 25076) Bloqueo en PTAuditudeAdResolver loadComplete

Se ha corregido el problema en el que se producía un bloqueo durante el inicio/parada rápidos de varias instancias de PTMediaPlayer con anuncios.

* (ZD# 25960) No hay etiquetas suscritas adicionales que activen emisiones de notificación de cambio de metadatos

Se ha corregido el problema en el que no se notifica a una etiqueta suscrita cuando aparece antes de que se corrija el primer segmento del manifiesto.

* (ZD# 26084) PSDK lanzando un 106000.101000.Error del decodificador -11833 al realizar la transición de la última pausa publicitaria al contenido de entretenimiento

Cuando el último tiempo de inicio de pausa publicitaria desde VMAP cae antes de que la duración total se complete, en determinadas condiciones, la clave no se inserta hasta después del final de la última pausa publicitaria. Este problema se ha corregido.

* La biblioteca de Video Heartbeat (VHL) se ha actualizado a la versión 1.5.9 para resolver los siguientes problemas:

* (ZD #22351) VHL - Analytics: Duración de los recursos de vídeo en directo

Este problema se ha resuelto añadiendo la API assetDuration a PTVideoAnalyticsTrackingMetadata para actualizar la duración del recurso para las emisiones en directo/lineales y proporcionar una lógica para comprobar el flujo en directo.

* (ZD# 22675) VHL: Analytics: Actualización de la duración de los recursos de vídeo en directo

Este problema es el mismo que ZD #22351.

* (ZD #25908) VHL - Analytics: Bloqueo de eventos de Heartbeat de Adobe

Este problema se resolvió actualizando la implementación para utilizar la última versión de VHL para iOS versión 1.5.9 para mejorar la estabilidad y el rendimiento.

* (ZD #25956) VHL - Analytics: Bloquear al reproducir vídeos repetidamente

Este problema es el mismo que ZD #25908.

**Versión 1.4.29**  (1.4.29.743)

* (ZD# 23901) Los anuncios de terceros no se reproducen

Este problema se solucionó moviéndose a la estructura de URL CRS v3 para incluir el ID de zona en la URL reempaquetada.

* (ZD #25183) Problemas con la reproducción de DRM en tvOS e iOS

Este problema se ha resuelto proporcionando compatibilidad con varias etiquetas clave necesarias para la compatibilidad con varios DRM.

* (ZD# 25334) TVSDK no reproduce contenido compartido cDVR

Este problema se ha resuelto impidiendo que TVSDK convirtiera cadenas vacías en direcciones URL absolutas.

* (ZD# 25347) Establezca el encabezado HTTP personalizado en AVURLAset

Se ha añadido compatibilidad con encabezados personalizados en sus solicitudes de segmento a través de la clase PTNetworkConfiguration.

**Versión 1.4.28**  (1.4.28.722)

* (ZD #24549) Varias llamadas de seguimiento de anuncios

Este problema se resolvió actualizando el administrador de cronología para detectar notificaciones en un objeto específico cuando se crean varios reproductores.

* (ZD #24758) PTManifestLogger no es compatible con iOS 8

Este problema se resolvió actualizando la biblioteca de utilidades del registrador al destino de implementación de la versión 7.0.

* (ZD #24775) Flujo retrasado debido a anuncios

Este problema se resolvió calculando correctamente el deriva de duración en las listas de reproducción de eventos.

* (ZD #24799) Algunos de los episodios no se reproducen en la aplicación iOS

Este problema se resolvió usando el servidor web local para subtítulos cuando los archivos WebVTT están georestringidos.

**Versión 1.4.27**  (1.4.27.711) para iOS 6.0+

* (ZD #24089): Optimizaciones para la resolución de anuncios en flujos DVR largos

Este problema se resolvió añadiendo varias optimizaciones para reducir el tiempo necesario para procesar la ventana DVR en flujos en directo/lineales.

* (ZD #21554) - Las señalizaciones de error de TVSDK no se activan para el tipo de aplicación = video/mp4

Este problema se ha resuelto permitiendo que el reproductor haga ping en las URL de seguimiento de errores correctas en formatos de recurso no válidos.

* (ZD #24424) - El bloqueo de tipo EXC_BAD_ACCESS KERN_INVALID_ADDRESS se origina desde el interior de PSDKLib para iOS en dispositivos de hardware más nuevos.

Se ha corregido el bloqueo que se producía debido a una instancia de reproductor de medios desasignada, cuando la reproducción cambia rápidamente entre diferentes flujos.

* (ZD #24575): Bloqueo en TVSDK en dispositivos de 32 bits cuando enableDebugLog=true

Se ha corregido el problema en el formato de registro que provocó el bloqueo en dispositivos de 32 bits cuando el registro está habilitado.

**Versión 1.4.26**  (1.4.26.702) para iOS 6.0+

* (ZD# 20213): El FW de TVSDK debe ser dinámico/modularizado para XCode7

Se ha corregido al actualizar las bibliotecas con compatibilidad con módulos

**Versión 1.4.25**  (1.4.25.684) para iOS 6.0+

* (ZD #19629): Se pone en pausa el vídeo en directo al entrar en el aire a ATV 4

Este problema se resolvió agregando un periodo de espera después de eliminar elementos antiguos pero antes de agregar nuevos elementos a AVQueuePlayer. Sin el periodo de espera, las notificaciones se envían al elemento incorrecto.

* (ZD #19856): No se muestran subtítulos cuando está activado de forma predeterminada

Se han corregido los problemas en la lista de reproducción del webvtt, que hacía que los subtítulos no se mostraran correctamente.

* (ZD #21590) - Rendimiento y seguimiento de vídeo en las últimas versiones de origen

Se ha corregido el problema de la longitud del vídeo que faltaba en VideoAnalytics.

* (ZD #20202): Al configurar el estilo de los subtítulos personalizados, se bloquea la aplicación de iOS

Este problema se ha resuelto añadiendo comprobaciones de objetos nulos adicionales al establecer los estilos de subtítulo.

* (ZD #20709): duración del vídeo registrada como 0 en el seguimiento de inicio de vídeo

Este problema es el mismo que (ZD #21590).

* (ZD #22280): Duración del vídeo de Analytics establecida en 0

Este problema es el mismo que (ZD #21590).

* (ZD #22592) - Problemas con el juego aéreo en Primetime

Este problema es el mismo que (ZD #19629).

* (ZD#22922) - Conmutación de velocidad de bits manual para iOS

Este problema se resolvió al proporcionar una opción para especificar la velocidad de bits máxima.

* (ZD #23084) - Cumplimiento de Apple para redes solo IPv6

Se han eliminado los símbolos que Apple no recomendaba para la compatibilidad con IPv6.

**Versión 1.4.24**  (1.4.24.661) para iOS 6.0+

* ZD #2548) - Compatibilidad de Primetime con publicidad interactiva en dispositivos móviles - VPAID 2.0

Este problema se resolvió actualizando la lógica para mostrar la vista del reproductor si un anuncio VPAID no se reprodujo.

* (ZD #20101): La implementación de capítulos personalizados activa un evento de inicio de capítulos durante la reproducción del anuncio

Este problema se resolvió actualizando VideoAnalyticsTracker para detectar correctamente el inicio/finalización del capítulo al realizar la transición entre los límites de capítulos y no capítulos.

* (ZD #20784) - Analytics: Se completa la activación de contenido para transiciones de vídeo en directo

Este problema se resolvió añadiendo una lógica para almacenar en déclencheur manualmente la finalización del contenido durante una sesión de seguimiento de vídeo.

Se han actualizado las bibliotecas siguientes:

* Biblioteca AdobeMobile a 4.10.0
* Biblioteca VHL a 1.5.6
* Biblioteca VHL-Nielsen 1.6.7
* (ZD #21855) - Los subtítulos no se reproducen después de la emisión

En este problema, las etiquetas de discontinuidad duplicadas provocaban que los subtítulos no aparecieran después de la emisión. Este problema se ha resuelto eliminando las etiquetas de discontinuidad que están una al lado de la otra.

* (ZD #21994) - Cadena fuera de límite en PTHLSUtils

La causa más probable del bloqueo es cuando una EXT-X-KEY tiene una URL rodeada de comillas.

* ZD #22074) - El bloqueo de AUDVAST ocurre una vez al minuto en iOS

En la versión 1.4.23, se corrigió el bloqueo causado por la presencia de caracteres no seguros en una URL de redireccionamiento de VAST. Sin embargo, TVSDK seguía omitiendo estos anuncios.

Este problema se resolvió manejando los caracteres no seguros y permitiendo que se reprodujeran los anuncios.

* (ZD #22694) - PTMediaPlayer.  La vista está oculta para el reproductor

Este problema se resolvió actualizando la lógica para mostrar la vista del reproductor si un anuncio VPAID no se reprodujo.

**Versión 1.4.23**  (1.4.23.641) para iOS 6.0+

* (ZD #18016): No hay respuesta del SDK de Primetime con una condición de red incorrecta

Este problema se ha resuelto mejorando la notificación de errores cuando se produce un error grave de AVFfoundation y permitiendo que la aplicación gestione el reinicio después del error.

* (ZD #20580) - Bloqueo en PTSplicerManager

Este problema se resolvió proporcionando protección adicional contra problemas de concurrencia que provocan el bloqueo.

* (ZD #21782) - Código de error de iOS 10100

Se ha corregido el problema por el que el TVSDK devolvía un error 101000 al iniciar la reproducción en flujos DRM de acceso a Adobe.

* (ZD #21889): Los anuncios en línea y la reproducción de contenido sin conexión fallan

Se ha corregido un problema en el que la reproducción fallaba después de que se corrigiera un anuncio en contenido sin conexión cifrado AES.

* (ZD #22074) - El bloqueo de AUDVAST se produce una vez al minuto en iOS

Este problema se ha resuelto mejorando la gestión de las etiquetas de anuncios VAST de terceros que tienen caracteres no válidos en la dirección URL.

* (ZD #22257): El TVSDK no reproduce el flujo DRM

Se ha corregido el problema por el que el TVSDK que devolvía un error 101000 al iniciar la reproducción en flujos DRM de acceso a Adobe.

**Versión 1.4.22**  (1.4.22.627) para iOS 6.0+

* (ZD #18709): Bloqueo en TVSDK para iOS

Se ha corregido el problema de un bloqueo que se producía en algunos flujos protegidos por DRM de acceso a Adobe.

* (ZD #18850) - Actualice la lógica de selección creativa basada en las reglas CRS

Este problema se resolvió añadiendo un archivo de configuración .json para especificar la prioridad de selección creativa.

* (ZD #19770) - La fuente de vídeo de AES protegida ya no se reproduce

Se ha solucionado el problema en el que algunos flujos redirigidos 302 no podían jugar.

* (ZD #19629): Se pone en pausa el vídeo en directo al entrar en el aire a ATV 4

Este problema se resolvió añadiendo una solución para pausar el vídeo en directo cuando se activa la reproducción de audio para los dispositivos Apple TV 4. El problema parece ser AppleTV 4.

* (ZD #21119): El TVSDK se detiene después de la reproducción del anuncio

Se ha añadido compatibilidad con flujos cifrados de AES con una secuencia IV mientras se utilizaba la inserción de anuncios.

* (ZD #21125) - Retorno de la pausa publicitaria en directo/lineal antes de

Se ha añadido compatibilidad para volver de una pausa publicitaria antes de que se reproduzca la pausa publicitaria hasta el final. El retorno anticipado se indica mediante una etiqueta de manifiesto personalizada.

* (ZD #21224) - Soporte de Airplay para emisiones tokenizadas de Akamai

Se han agregado API a la clase PTNetworkConfiguration para anexar cookies como parámetros de URL en segmentos para ciertas emisiones token de Akamai.

* (ZD #21287): registro externo

Se ha corregido un problema con algunas instrucciones de registro que se mostraban de forma predeterminada en la consola xcode incluso cuando el registro estaba deshabilitado.

* (ZD #21446) - Los eventos de pausa publicitaria a veces no se activan con el TVSDK

En las emisiones de EVENTO, las pausas publicitarias no se activan correctamente en la versión anterior. Esta compilación aborda este problema.

**Versión 1.4.21**  (1.4.21.605) para iOS 6.0+

* (ZD #20749) - Fallback omite las respuestas VAST no vacías; Se activan direcciones URL de seguimiento de anuncios adicionales

Se ha resuelto un problema con los pings duplicados en los anuncios de reserva.

**Versión 1.4.20**  (1.4.20.590) para iOS 6.0+

* (ZD #18639): El TVSDK está utilizando una CPU/recursos excesivos en un recurso de grabación en caliente largo

El uso excesivo de CPU/recursos se ha corregido en los dos niveles. Primero, permitiendo que la función de actualización de tiempo se ejecute en una cola global, en lugar del subproceso principal, y optimizando el uso de CPU para analizar el manifiesto con el m3u8 procesado y almacenado en caché previamente.

* (ZD #19349): los anuncios previos a la emisión se omiten al restringir la conexión de red.

Este problema se resolvió proporcionando un evento de tiempo de espera (requestTimeout) a la aplicación y a los metadatos de publicidad .  adRequestTimeout API para anular el tiempo de espera predeterminado de 10 segundos.

* (ZD #19446) - Falta notificación en las transmisiones en directo

Este problema se resolvió permitiendo que la aplicación se suscribiera a EXT-X-PROGRAM-DATE-TIME en transmisiones en vivo.

* (ZD #19459): Bloqueo al preparar audio alternativo con PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Bloqueo - `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

Este problema es el mismo que Zendesk #19459.

* (ZD #19574): El TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM

En la carga inicial del archivo de manifiesto en PTMediaPlayerItem.prepareToPlay, si falla la carga del manifiesto, el TVSDK no informa del cuerpo de la respuesta de error a la aplicación.

Este problema se resolvió permitiendo que el TVSDK informara de la respuesta de error como un error a la aplicación.

* (ZD #19615): La lógica de reserva no funciona

En la implementación actual, los anuncios de reserva se omitieron y no se volvieron a empaquetar a menos que estos anuncios estuvieran en formato m3u8. Este problema se resolvió añadiendo también la compatibilidad para volver a empaquetar anuncios de reserva.

* (ZD #19770): El TVSDK no reproduce ningún contenido AES protegido con redireccionamiento 302

Se ha corregido el problema de redirección porque la dirección URL de redirección se borraba con cleanConnectionData antes de que se pudiera usar para analizar el manifiesto.

* (ZD #19856): los subtítulos no se muestran para algunas tasas de bits cuando están activados de forma predeterminada

Este problema se ha resuelto al gestionar el error de iOS para los segmentos de las emisiones en los que no se muestran los subtítulos.

* (ZD #19868): El TVSDK se bloquea cuando se transmite un elemento creativo no válido

Se ha corregido el bloqueo en el SDK de TVSDK que estaba deslocalizando incorrectamente una instancia del vasto analizador.

* (ZD #20180): Los anuncios VPAID se omiten ocasionalmente

El tipo mime de JavaScript no siempre se incluía o consideraba como un tipo mime válido. Este problema se ha resuelto incluyendo JavaScript como tipo de mime válido.

* (ZD #20749) - Fallback omite las respuestas VAST no vacías; Se activan direcciones URL de seguimiento de anuncios adicionales

Se ha solucionado el problema de algunos de los elementos creativos que no se están reempaquetando.

**Versión 1.4.19**  (1.4.19.563) para iOS 6.0+

* ZD #18639) - El TVSDK utiliza una CPU/recursos excesivos en un recurso de grabación en caliente y largo

Este problema se resolvió optimizando la reescritura de la lista de reproducción DRM m3u8 en los bits de caché de la lista de reproducción que se han reescrito anteriormente. Esto es más relevante cuando reproduce transmisiones en vivo m3u8 para las que m3u8 se descarga después de cada descarga de segmento.

* (ZD#18956) - player.drmManager es nil cuando el punto de interrupción se establece en el reproductor de demostración de iOS

Este problema se resolvió actualizando la implementación de la API PTMediaPlayer.drmManager para recoger DRMManager del marco de DRM.

**Versión 1.4.18** ( 1.4.18.557) para iOS 6.0+

* (ZD #18844) El cabezal de reproducción de seguimiento del contenido en directo en el reproductor iOS.

Este problema se resolvió permitiendo que las aplicaciones establecieran su propio valor de cabezal de reproducción.

* (Zendesk #18518): Si no se especifica el nombre del vídeo, el nombre del TVSDK es de forma predeterminada * reproductor basado en PSDK.*

Este problema se resolvió eliminando el valor predeterminado del nombre del reproductor.

**Versión 1.4.17**  (1.4.17.545) para iOS 6.0+

* (Zendesk #2228): Mejore el TVSDK para devolver la respuesta JSON de la recuperación de un manifiesto

En lugar de enviar un error cuando el contenido no es M3U8, el marco de DRM devuelve un DRMMetadata nulo. El problema se resolvió añadiendo metadatos para exponer el contenido cuando se produce la notificación M3U8_PARSER_ERROR.

* (Zendesk #2231) - Error devuelto al recuperar el manifiesto no disponible en MediaPlayerNotification

La misma resolución que Zendesk #2228

* (Zendesk #3304) - La macro VAST 3.0 `[ERRORCODE]` no se rellena

Se ha resuelto el problema en el que el SDK de Auditude no puede enviar un ping cuando la URL de seguimiento tiene espacios al principio.

* (Zendesk #17294) - Bloqueo SecKeyRawSign

Se ha resuelto un posible bloqueo cuando el código del cliente utiliza la cadena de claves.

* (Zendesk #18008): Compatibilidad con cookies para iOS8+ para admitir transmisiones con token

Las transmisiones con token de Akamai requieren que las cookies se envíen en solicitudes de segmento, lo que no fue posible en iOS 7 y versiones anteriores. A partir de iOS 8, Apple ha agregado una API que permite pasar cookies para solicitudes de segmentos. Esta compatibilidad ya está disponible en TVSDK . También se ha añadido soporte para enviar un usuario-agente, si está disponible.

* (Zendesk #18166): TVSDK 1.4.15 proporciona cientos de advertencias al compilar con DWARF con opciones de archivo dSYM

Se han resuelto todas las advertencias.

**Nota**: Se han añadido bibliotecas compatibles con tvOS para TVSDK .

**Versión 1.4.16**  (1.4.16.1454)

* Zendesk #3875 - Tab S se bloquea durante la reproducción

Revertir la dependencia de OKHTTP en la auditude para CRS porque TVSDK ahora está utilizando directamente httpurlconnection en lugar de curl. El problema se resolvió borrando las excepciones antes de realizar otra llamada de JNI.

* (Zendesk #4487) - Seguimiento del canal de contenido lineal

El problema se resolvió reiniciando el rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* (Zendesk #17919) - Android: la búsqueda de contenido causa un error de latido

El problema era resolver el latido en un estado de error cuando hay una búsqueda en un capítulo

* (Zendesk #18053): La aplicación que utiliza el TVSDK se bloquea en el malvavisco

El SDK de TVSDK se bloqueaba en el sistema operativo Android M cuando la biblioteca TVSDK utiliza código neón que realiza la conversión de color RGB YUV `->`. Este problema se resolvió actualizando las funciones que causan este problema usando la versión no neon de `code`.

* (Zendesk #18072) - Android M: bloqueo de aplicación

Este bloqueo se produce al llamar a las API MediaCodecList y MediaCodecInfo al comprobar si el perfil y el nivel son compatibles. Adobe está buscando el soporte técnico de Google para obtener más información. Este problema se ha resuelto proporcionando una solución temporal cargando toda la información del códec con antelación para evitar llamar a estas API solo cuando se necesita información del códec.

* (Zendesk #18074) - Los subtítulos árabes no funcionan en Nexus con Android 6.0

Este problema se resolvió proporcionando compatibilidad con el mapa de fuentes CTS de Android.

**Versión 1.4.15**  (1.4.15.512) para iOS 6.0+

**Nota**: El módulo Nielsen se ha eliminado de la compilación de TVSDK, pero el TVSDK se actualizará próximamente con un nuevo módulo de integración de Nielsen.

* (ZD #2228) - Error devuelto al recuperar el manifiesto no disponible en MediaPlayerNotification

Se han agregado metadatos para exponer el contenido cuando se produce la notificación M3U8_PARSER_ERROR.

* (ZD #4437): Bloqueos dentro del SDK de Adobe Primetime

Se ha corregido un bloqueo informado al preparar subtítulos o audio alternativo.

* (ZD #4487) - Seguimiento del canal lineal de contenido

Se permite la reinicialización del rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

**Versión 1.4.14**  (1.4.14.498) para iOS 6.0+

* (ZD #17260): Bloqueo en playlistManagerForURL

Se ha corregido un bloqueo intermitente debido a problemas de concurrencia.

**Versión 1.4.13**  (iOS 6.0+)

* (ZD #3304) - La macro VAST 3.0 `[ERRORCODE]` no se rellena

   * El código de error 400 se expone si está en línea   el anuncio tiene un elemento creativo incorrecto.
   * `[ERRORCODE]` la macro se codificará con la dirección URL.

* (ZD #3865) Integración de Heartbeat con anuncios IMA

Se ha corregido un error por el que la duración del vídeo se informaba incorrectamente.

* Se ha actualizado el reproductor de demostración TVSDK para que admita iOS 9

Para admitir correctamente iOS 9, debe configurar las excepciones de Application Transportation Security. A los efectos de la demostración, ATS está completamente desactivado.

**Versión 1.4.12**  (1.4.12.464) para iOS 6.0+

* (ZD #4521) CRS Prueba del lado del cliente y SSAI

Se ha corregido MD5 inverso incorrecto en la URL 3P.

**Versión 1.4.12**  (1.4.12.463) para iOS 6.0+

* (ZD #2751) CSAI y CRS / Mejora: Gestione elementos dinámicos en determinadas direcciones URL de archivos multimedia.

Se ha actualizado el servicio de reempaquetado creativo para que gestione correctamente los anuncios con direcciones URL creativas dinámicas.

* (ZD #3654) Fuga de memoria en la versión PSDK después de la versión 1.3.4.166

Se ha corregido una fuga de memoria en drmFramework con reproducción regular en dispositivos iOS 8.2

* (ZD #3988) El predesplazamiento se omite al volver a buscarlo después de la primera reproducción

Se ha corregido un error para que las políticas de publicidad pudieran deshabilitarse correctamente.

* (ZD #4017) Solicitud de la API de iOS para forzar la reproducción del anuncio en la búsqueda hacia atrás

Resuelto con corrección para ZD #4279

* (ZD #4279) Inserción de anuncios de HLS TVSDK -302 problema de redireccionamiento en iOS y escritorio

Se ha corregido un error cuando un recurso de publicidad usaba una dirección URL de redireccionamiento relativa

**Versión 1.4.9**  (1.4.9.427) para iOS 6.0+

* (ZD #3075) Problema de accesibilidad de Internet - iOS

Se ha añadido una notificación para detectar si la reproducción se ha detenido.

* (ZD #3193) Solicitud de una API de cambio de perfil en TVSDK

Se ha actualizado PTPlaybackInformation para exponer la velocidad de bits indicada actualizada. Se ha actualizado la notificación BITRATE_CHANGE para que sea más fiable y precisa para las velocidades de bits notificadas por la M3U8.

* (ZD #3324) Problemas con los anuncios de Primetime cuando no hay medios publicitarios en VMAP

Compatibilidad con URL de seguimiento de pausa publicitaria vacías, TVSDK ahora verificará el inicio de la pausa publicitaria y completará los pings para las pausas publicitarias vacías.

**Versión 1.4.8**  (1.4.8.402)

* (ZD #3158) IOS 7 se bloquea en reproducciones de eventos completos

**Versión 1.4.7**  (1.4.7.382)

* (ZD #2197) Seguimiento de errores de publicidad. Se ha añadido la notificación para el recurso que no pudo cargar el manifiesto.
* (ZD #2894) El reproductor realiza 4 solicitudes de manifiesto de nivel superior durante la reproducción.
* (ZD #2992) Informes de audiencia duraciones e identificadores extraños.

**Versión 1.4.6** (1.4.6.325)

* (ZD #2197) Seguimiento de errores de publicidad. Se ha añadido una notificación para el recurso que no pudo cargar el manifiesto

**Versión 1.4.5**  (1.4.5.283)

* (ZD #2141) Implementación de Analytics para la aplicación TreeHouse, se ha añadido la `AdobeAnalyticsPlugin.a` biblioteca para crear el paquete .
* Actualización de la biblioteca Video Heartbeats a la versión 1.4.1.2
* (PTPALY-4226) (relacionado con ZD #2423) Realizar el restablecimiento de DRM puede resultar en la eliminación de los datos del documento de la aplicación.

**Versión 1.4.4**  (1.4.4.242)

* La biblioteca de Video Heartbeats (VHL) se actualiza a la versión 1.4.1.

* (ZD #2435) Documentación del SDK de TV sobre las actualizaciones de las necesidades de análisis

**Versión 1.4.2**  (1.4.2.210: iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` devuelve vacío
* (ZD #2109) Primetime PSDK 1.4.1.125 no funciona con Xcode 5.1.1
* (ZD #2137) Bloqueo en PSDK en iOS cuando no se pueden cargar metadatos DRM

**Versión 1.4.1** (1.4.1.125)

* (ZD #1107) CocoaLumberjack símbolos duplicados
* (ZD #1644) Modificación del agente de usuario de iOS para informes y segmentación
* (ZD #1850) Archivos Lumberjack de cacao incluidos en el SDK para iOS
* (ZD#1908) El SDK ignora las etiquetas personalizadas si hay más de 1

**Versión 1.4.0**  (1.4.0.32)

* Zendesk #1024 - Función para eliminar un anuncio del flujo a través de un manifiesto

## Certificación y compatibilidad de dispositivos {#device-certification-and-support}

>[!NOTE]
>
>Las siguientes funciones son **no** compatibles con el TVSDK:
>
>* Movimiento lento, en cualquier plataforma o versión.
>* Juego de trucos en vivo.


**Versión 1.4.43**

* TVSDK 1.4.43 está certificado para iOS 11.

**Versión 1.4.29**

* TVSDK 1.4.29 se ha certificado para iOS 10.

**Versión 1.4.28**

* TVSDK 1.4.28 está certificado para iOS 10 Beta 7.
* Compatibilidad con DRM para forzar HTTPS añadiendo API `forceHTTPS` y `isForcingHTTPS`.
* Se han actualizado las bibliotecas VHL a la versión 1.5.8, las bibliotecas móviles de Adobe a la versión 4.8.4 y la biblioteca de utilidades de registrador a la versión 7.0 de destino de implementación.

**Versión 1.4.19**

Esta versión de TVSDK ha sido certificada con la compatibilidad con FairPlay para iOS y tvOS.

**Versión 1.4.17**

* tvOS

   Esta versión de TVSDK incluye compatibilidad con tvOS y se ha certificado para flujos HLS no cifrados.

   **Nota**: Recuerde las siguientes directrices de compilación:

   * La compatibilidad con TVSDK tvOs está limitada a emisiones cifradas DRM sin Adobe. Debe eliminar la referencia a drmNativeInterface.framework en la configuración de compilación de tvOS. Los flujos cifrados de AES siguen siendo compatibles.
   * Apple requiere que todas las aplicaciones de Apple TV estén habilitadas para código de bits, por lo que debe activar este indicador en la configuración del proyecto.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

* Debido a la desaprobación de la clase UIWebView de iOS, en iOS TVSDK 3.6 y posteriores:
   * Los anuncios VPAID no se reproducirán como se espera en el iPad 13.
   * Los anuncios Companion no se reproducirán según lo esperado.

* En iOS TVSDK, todos los anuncios se vinculan al manifiesto de contenido. Los comportamientos de los anuncios se implementan buscando basándose en la duración de los segmentos de contenido y anuncios. Por lo tanto, si las duraciones de los segmentos no son precisas, es posible que la búsqueda no siempre termine en el fotograma exacto del principio o final de la pausa publicitaria. Incluso si las duraciones van hasta el fotograma, existe una tolerancia que la plataforma misma impone a la búsqueda y puede haber algunos fotogramas, anuncios o contenido mostrados. Esto supone una limitación de la plataforma y del modo en que la inserción de anuncios funciona con TVSDK en iOS.
* La decisión de omitir se produce en el evento de búsqueda en este caso. Sin embargo, dado que las duraciones del segmento de publicidad en el manifiesto no representan con precisión la duración real del anuncio, la búsqueda no es precisa. Por lo tanto, cuando se aplican las políticas de publicidad, verá algunos fotogramas de publicidad.
* Es posible que el vídeo de rotación de licencias no se reproduzca en iOS 11 y que se reproduzca correctamente en iOS 9.x e iOS 10.x.
* En la compatibilidad con VPAID 2.0, si la reproducción está activa en AirPlay, los anuncios VPAID se omiten.
* drmNativeInterface.framework no se vincula correctamente cuando el destino mínimo se establece en iOS7 (o posterior).
Solución alternativa: Especifique explícitamente la biblioteca libstdc++.6.dylib de la siguiente manera: Vaya a Target->Fases de compilación->Vincular binario con bibliotecas y añada libstdc++.6.dylib.
* El anuncio posterior a la emisión no se inserta para reemplazar la API.
* Al buscar en una pausa publicitaria (sin salir de ella), se genera una notificación de inicio y pausa publicitarias duplicadas
* Configurar currentTimeUpdateInterval no tiene ningún efecto.
Nota: En algunas versiones de iOS, el sistema operativo no carga los recursos dentro de PSDKLibrary.framework automáticamente. Es importante copiar manualmente el PSDKResources.bundle en los recursos del paquete de la aplicación: Vaya a Fases de compilación y copie los recursos del paquete.
* La aplicación de referencia no se puede crear con Xcode 8 o versiones inferiores. A partir de la versión 1.4.41 de iOS TVSDK, utilice Xcode 9 para compilar.
* Los anuncios VPAID no respetan el valor delayAdLoadingTolerance .
* 24077- Para ciertos contenidos HLS con subtítulos, el reproductor se bloquea en el método Stop o Reset.
* Las notificaciones de error detalladas no están disponibles en caso de que la resolución de anuncios justo a tiempo esté habilitada.
* Las notificaciones de error se registran según el tiempo de resolución de la publicidad y no según la secuencia de publicidad.
* La compatibilidad con HEVC tiene las siguientes limitaciones en esta versión
   * DRM no compatible
   * La compatibilidad con CC (CEA 608/708) no está disponible, ya que no es compatible con CMAF.
   * La compatibilidad con 4K aún no está presente.
   * La compatibilidad con etiquetas ID3 no está disponible, ya que no es compatible con CMAF.
   * Transmisiones de HEVC en directo sin muestrear no verificadas.
   * La compatibilidad con anuncios HEVC no está verificada.
* Con JIT habilitado y la tolerancia establecida en 10 segundos, no se ve ninguna llamada VAST para la primera pausa publicitaria de midroll en caso de anuncios de redireccionamiento VMAP->VAST.
* Para que el tiempo de espera de la resolución del anuncio funcione correctamente, cada vez que se actualiza la lista de reproducción durante la reproducción del flujo en directo, el reproductor espera una lista de reproducción vinculada en un plazo de 20 segundos. Si no recibe una lista de reproducción vinculada dentro del intervalo mencionado, se produce un error interno y el reproductor se detiene.

## Recursos útiles {#helpful-resources}

* [Guía del programador de TVSDK 3.4 para iOS](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-for-ios/introduction/ios-3x-overview.html)
* [Referencia de la API de TVSDK iOS 3.4](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
