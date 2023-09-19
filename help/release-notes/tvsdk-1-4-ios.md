---
title: Notas de la versión de TVSDK 1.4 para iOS
description: Las notas de la versión de TVSDK 1.4 para iOS describen las novedades o los cambios, los problemas resueltos y conocidos, y los problemas de los dispositivos en TVSDK iOS 1.4
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6549'
ht-degree: 0%

---

# Notas de la versión de TVSDK 1.4 para iOS {#tvsdk-for-ios-release-notes}

Las notas de la versión de TVSDK 1.4 para iOS describen las novedades o los cambios, los problemas resueltos y conocidos, y los problemas de los dispositivos en TVSDK iOS 1.4.

## Nuevas funciones {#new-features}

**Versión 1.4.45**

* Para cumplir con Xcode10, TVSDK se ha movido de &quot;`libstdc++`&quot; a &quot;`libc++`&quot; y, como resultado, la versión mínima admitida es iOS 7. Antes era iOS 6.

**Versión 1.4.44**

* No hay nuevas funciones ni mejoras en esta versión.

**Versión 1.4.43**

* Experiencia similar a la de TV de poder unirse en medio de un anuncio sin activar el seguimiento parcial de anuncios.\
  Ejemplo: Las uniones de usuarios se producen en medio (a los 40 segundos) de una pausa publicitaria de 90 segundos y consisten en tres anuncios de 30 segundos. Son 10 segundos del segundo anuncio de la pausa.

   * El segundo anuncio se reproduce durante el tiempo restante (20 segundos) seguido del tercer anuncio.
   * Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Solo se activan los rastreadores del tercer anuncio.

* Se ha agregado la propiedad enableVodPreroll de tipo booleano en la interfaz PTAdMetadata. La propiedad se puede utilizar para habilitar el anuncio previo a la emisión en un flujo VoD. Si enableVodPreroll es NO, PSDK no reproduce el anuncio previo a la emisión. Esto, sin embargo, no tiene ningún impacto en los midrolls. El valor predeterminado de enableVodPreroll es YES.
* La API closedCaptionDisplayEnabled de la interfaz PTMediaPlayer está marcada como obsoleta a partir de la versión 1.4.43 de iOS. Para determinar si hay subtítulos opcionales disponibles para un PTMediaPlayerItem determinado, examine la propiedad subtitlesOptions de PTMediaPlayerMediaItem.

**Versión 1.4.42**

No se han agregado nuevas funciones en esta versión. Para obtener una lista de los problemas corregidos, consulte Problemas resueltos.

**Versión 1.4.41**

Cambios de API:

* **isSecure**: Se introduce una nueva API isSecure para evitar que el reproductor grabe y genere un error. El valor predeterminado es True.
* **allowExternalRecording**: Se introduce una nueva API para permitir la duplicación de reproducción para un contenido seguro. La duplicación de reproducción aérea se trata como grabación; por lo tanto, el valor allowExternalRecording debe establecerse en &#39;True&#39;, para permitir la duplicación de reproducción aérea, o en &#39;False&#39; para detener la duplicación de reproducción para contenido seguro. De forma predeterminada, el valor es True.

**Versión 1.4.40**

No hay nuevas funciones.

**Versión 1.4.39**

* iOS TVSDK está certificado con VHL 2.0.1 y con VHL 2.0.1 con Nielsen.
* El SDK de TVSDK de iOS se actualiza para realizar solicitudes de CRS desde el nuevo host de Akamai `primetime-a.akamaihd.net`.
* La nueva configuración de nombre de host proporciona la entrega de recursos CRS a través de HTTP y HTTPS (SSL) a mayor escala.

**Versión 1.4.36**

Integrar y certificar VHL 2.0 en iOS TVSDK : Reduzca la barrera en la implementación de VideoHeartbeatsLibrary disminuyendo la complejidad de las API.

**Versión 1.4.34**

* Información de anuncio de red

  Las API de TVSDK ahora proporcionan información adicional sobre las respuestas VAST de terceros. Las extensiones de ID de anuncio, Sistema de publicidad y Anuncio VAST se proporcionan en `PTNetworkAdInfo` clase accesible mediante  `networkAdInfo`  propiedad en un recurso publicitario. Esta información se puede utilizar para integrar con otras plataformas de Ad Analytics como **Análisis de foso**.

**Versión 1.4.31**

* **Métricas de facturación** Para dar cabida a los clientes que desean pagar únicamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, los Adobes recopilan las métricas de uso y las utilizan para determinar cuánto facturar a los clientes.

Cada vez que TVSDK genera un evento de inicio de flujo, el reproductor comienza a enviar mensajes HTTP periódicamente al sistema de facturación de Adobe. El periodo, conocido como duración facturable, puede ser diferente para VOD estándar, PRO VOD (anuncios mid-roll habilitados) y contenido en directo. La duración predeterminada de cada tipo de contenido es de 30 minutos, pero el contrato con el Adobe determina los valores reales.

* **Compatibilidad con varias CDN para anuncios CRS** TVSDK ahora es compatible con Multi-CDN para anuncios CRS. Al proporcionar detalles de FTP para los anuncios de CRS, puede especificar ubicaciones de CDN distintas de la CDN de propiedad del Adobe predeterminada, como Akamai.

**Versión 1.4.29**

En la clase PTSDKConfig, se ha añadido la API forceHTTPS.

La clase PTSDKConfig proporciona métodos para aplicar SSL en solicitudes realizadas a los servidores de Adobe Primetime ad Decisioning, DRM y Video Analytics. Para obtener más información, consulte la `forceHTTPS` y `isForcingHTTPS` métodos en esta clase. Si un manifiesto se carga a través de HTTPS, TVSDK conserva el uso de contenido de HTTPS y respeta este uso al cargar cualquier dirección URL relativa de ese manifiesto.

**Nota**: Las solicitudes a dominios de terceros, como los píxeles de seguimiento de publicidad, las direcciones URL de contenido y publicidad, y solicitudes similares no se modifican y es responsabilidad de los proveedores de contenido y los servidores de publicidad proporcionar las direcciones URL compatibles mediante HTTPS.

**Versión 1.4.18**

Primetime iOS TVSDK ahora es compatible con los creativos de JavaScript VPAID 2.0 para permitir una experiencia de anuncio en flujo enriquecida e interactiva.

Para obtener más información sobre VPAID 2.0, consulte [Compatibilidad con anuncios VPAID](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md).

**Versión 1.4.17**

* tvOS

  TVSDK admite aplicaciones nativas de tvOS.
* Se pueden reproducir los siguientes tipos de contenido:

   * VOD
   * Activo
   * AES-128
   * Audio y subtítulos alternativos
   * FER

* Se pueden mostrar los siguientes tipos de anuncios:

   * Básico
   * VAST2
   * VAST3
   * VMA

* Actualmente no se admiten las siguientes funciones:

   * Digital Rights Management (DRM)
   * Titulares de publicidad
   * Lenguaje de marcado de TV (TVML)

**Versión 1.4.13**

**Nota**: el módulo Nielsen se ha eliminado de la compilación de TVSDK, el TVSDK se actualizará en un futuro próximo con un nuevo módulo de integración de Nielsen.

* **Reserva de anuncio, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103)**

Para los anuncios VAST (creativos) con la regla de reserva habilitada, TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Anuncio alternativo para anuncios VAST y VMAP](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md).

**Versión 1.4.9**

* **Señalización De Interrupción Con Sustitución De Contenido Alternativo**

Como parte de la actualización 1.4 del SDK de TVSDK, ahora también admitimos la inclusión y el retorno de las interrupciones regionales en el contenido lineal. El TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para monitorizar las señales de interrupción incluso cuando se muestra programación alternativa en lugar de la programación original.

**Versión 1.4.8**

* **Biblioteca de Video Heartbeats (VHL) actualizada a la versión 1.5**

   * Capacidad para enviar metadatos con inicio de vídeo o inicio de vídeo/publicidad/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño

**Versión 1.4.7**

* **Soporte de individualización local**

Compatibilidad con instalaciones on-premise del servidor de individualización de Adobe para personalizar la solicitud de individualización del cliente para ir a un punto final diferente.

* **Protección de salida basada en resolución**

Las directivas de DRM ahora pueden especificar la resolución más alta permitida, según las capacidades de protección de salida del dispositivo. Por ejemplo: &quot;Si HDCP está disponible, permitir que se reproduzca contenido con resolución de hasta 1080p, y si HDCP no está disponible, permitir que se reproduzca contenido con resolución de hasta 480p&quot;.

**Versión 1.4.4**

* **Actualización de la biblioteca de Video Heartbeats (VHL) a la versión 1.4.1.1.**

   * Se ha añadido la capacidad de combinar diferentes casos de uso de análisis, de otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete. La pausa publicitaria se deduce de las llamadas a los métodos trackAdStart y trackAdComplete.
   * La propiedad cabezal de reproducción ya no es necesaria al rastrear anuncios.
   * Se ha agregado compatibilidad con el ID de visitante de Marketing Cloud.

* **Integración del SDK de Nielsen**

   * TVSDK ahora es compatible con el envío de señalizaciones mTVR y MDPR ID3 al SDK de Nielsen sin ninguna integración personalizada. Para empezar, descargue el SDK de la aplicación Nielsen iOS 3.1.2.19.

**Versión 1.4.0**

* **Señalización De Interrupción Con Sustitución De Contenido Alternativo**

   * Como parte de la actualización de TVSDK 1.4, TVSDK ahora también admite la inclusión y la devolución de interrupciones regionales en contenido lineal. El TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para monitorizar las señales de interrupción incluso cuando se muestra programación alternativa en lugar de la programación original.

* **Eliminar/reemplazar anuncios C3**

   * Ahora, no se necesita ningún trabajo de preparación adicional para insertar dinámicamente nuevos anuncios en recursos de vídeo bajo demanda (VOD) que salen de la ventana de C3. TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar dinámicamente nuevos anuncios. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se emite durante la emisión y se extrae inmediatamente para su uso como contenido bajo demanda sin el tiempo adecuado para &quot;limpiar&quot; el recurso.

## Certificación y compatibilidad de dispositivos en 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Las siguientes funciones son **no** compatible con el TVSDK:
>
>* Cámara lenta, en cualquier plataforma o versión.
>* Jugar truco en vivo.

**Versión 1.4.43**

* TVSDK 1.4.43 está certificado para iOS 11.

**Versión 1.4.29**

* TVSDK 1.4.29 cuenta con la certificación para iOS 10.

**Versión 1.4.28**

* TVSDK 1.4.28 cuenta con la certificación para iOS 10 Beta 7.
* Compatibilidad con DRM para forzar HTTPS mediante la adición de las API forceHTTPS y isForcingHTTPS.
* Se han actualizado las bibliotecas VHL a 1.5.8, las bibliotecas de Adobe Mobile a 4.8.4 y la biblioteca de la utilidad del registrador a la versión 7.0 del destino de implementación.

**Versión 1.4.19**

Esta versión del TVSDK ha sido certificada con el Soporte FairPlay para iOS y tvOS.

**Versión 1.4.17**

* tvOS

  Esta versión del SDK de TVSDK incluye compatibilidad con tvOS y se ha certificado para flujos HLS no cifrados.

  **Nota**: Recuerde las siguientes directrices de compilación:

   * La compatibilidad con tvOs de TVSDK se limita a las secuencias cifradas DRM que no sean de Adobe. Debe quitar la referencia a drmNativeInterface.framework en la configuración de la versión de tvOS. Las secuencias cifradas AES siguen siendo compatibles.
   * Apple requiere que todas las aplicaciones de Apple TV estén habilitadas para código de bits, por lo que debe activar este indicador en la configuración del proyecto.

## Problemas resueltos en 1.4 {#resolved-issues-in}

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
-->

<!-- 

Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 

-->

**Versión 1.4.45{#ios-tvsdk}**

* #36294 de vale: iOS TVSDK no funciona con Xcode 10

   * Se han corregido los problemas de compilación con TVSDK en XCode 10. Debido a los requisitos de XCode 10, las aplicaciones creadas a partir de TVSDK para iOS 1.4.45 requieren un objetivo de implementación mínimo como iOS 7.0

* #36321 de vale: discrepancia observada en el intervalo buscable entre la instancia de PTMediaPlayer y AVPlayer en el estado &quot;Reproduciendo&quot;.
* #36493 de vale - `libstdc++` compatibilidad con iOS 12

   * Se han corregido los problemas de compilación con TVSDK en iOS 12. Las aplicaciones creadas a partir de TVSDK para iOS 1.4.45 requieren un objetivo de implementación mínimo como iOS 7.0

**Versión 1.4.44**

* #34683 De Ticket: El Tiempo De Progreso De Reproducción Del Anuncio Va En Negativo

   * Se realizan comprobaciones adicionales para controlar el caso cuando hay una discrepancia entre la duración notificada por el servidor de publicidad y el contenido real del anuncio.

* La #34801 de tickets - currentTime y localTime no se actualizaban al buscar una nueva posición durante el estado pausado

   * La hora actual del reproductor ahora se puede establecer en cero en caso de que el reproductor esté en estado pausado; anteriormente, la hora actual se solía establecer en cero solo en estado de reproducción.

* #35037 de tickets: puestos de reproducción con una URL incorrecta al volver de la inserción de anuncios basados en señales.

   * Se ha mejorado la corrección de los #34385 de problemas cerrados en la versión 1.4.42. Se ha agregado el código de control de excepciones y comprobación de isCanceled para que la cola de operaciones sea más sólida.

**Versión 1.4.43**

* (ZD#32990) - iOS: Reproducción de contenido en lugar de anuncios en algunos puntos de referencia. La API selectedMediaOptionInMediaSelectionGroup, que formaba parte de la interfaz AVPlayerItem, ahora se ha movido a AVMediaSelection en iOS 11. El problema se resolvió con esta nueva API.
* (ZD#33683) TVSDK ha eliminado == sufijo de las cadenas de metadatos. El problema se corrige en la lógica de análisis.
* (ZD#33905): iOS TVSDK realiza llamadas a los archivos de manifiesto con dos agentes de usuario. El problema del agente de usuario se ha corregido en la primera llamada m3u8 (caso de instalación reciente). Los M3u8 tienen los mismos user-agents para todas las llamadas ahora.
* (ZD#34293) - Los pre-rolls insertados en los flujos LINEALES no se reproducen correctamente en iOS11. El problema se ha corregido para los anuncios previos a la emisión.
* (ZD#34684): cuando se aplica la política de omisión de anuncios, los fotogramas de anuncio previo a la emisión se muestran durante unos segundos. Se ha introducido una nueva API, enableVodPreroll, para deshabilitar la reproducción de preroll en la reproducción de vod. El valor predeterminado de esta API es &quot;Sí&quot;. La API garantiza que se omita la vinculación de contenido de publicidad en el contenido principal.
* (ZD#34765) - Después de llamar a stop(), algunos segmentos de Transportes aún se descargan. Se ha mejorado la API Stop() para evitar la descarga de segmentos adicionales.
* (ZD#34865): Los anuncios previos a la emisión en directo se truncan en iOS. En relación con iOS11, y al añadir una comprobación adicional para confirmar si el flujo es de contenido principal o previo a la emisión, se soluciona este problema.
* (ZD#35093): se ha corregido un escenario de conmutación por error en el que, si la variante principal de la secuencia falla al inicio (devuelve 404), la reproducción no cambia a una secuencia de copia de seguridad.

**Versión 1.4.42 (1.4.42.118)**

* (ZD#34385): La reproducción se detiene con una URL incorrecta al volver de la inserción de publicidad basada en señales.

  Aumente los recuentos simultáneos máximos de CustomAVAsetLoaderOperations, de modo que las lecturas de manifiesto puedan seguir ejecutándose.
* (ZD#34373) - Los usuarios finales no pueden transmitir a dispositivos conectados a HDMI cuando la grabación de flujo no está permitida.
* (ZD#32678): TVSDK no recopila los ID de anuncio correctos en iOS.

  El ID de anuncio del creativo de publicidad final ahora se recoge en los pings VHL en caso de redirecciones VAST/VMAP.
* (ZD#33904): TVSDK no está registrado para las notificaciones de AVFfoundation AVAudioSessionMediaServicesWhereLostNotification y AVAudioSessionMediaServicesWhereResetNotification.

  PTMediaServicesWhereLostNotification y PTMediaServicesWhereResetNotification ahora se pueden registrar en la aplicación del reproductor para obtener las notificaciones cuando se restablezcan o pierdan los servicios de medios.

* (ZD#33815): Los clientes no pueden actualizar sus reglas de CRS de priorización y normalización sin requerir una actualización de la aplicación.

  Se han agregado las API getCRSRulesJsonURL y setCRSRulesJsonURL a iOS TVSDK

**Versión 1.4.41 (1.4.41.76)**

* (ZD #34464): Problemas al crear la aplicación de referencia con TVSDK versión 1.4.41

  A partir de esta versión, se requiere Xcode 9 para compilar TVSDK para iOS.
* (ZD #29456) - El juego aéreo comienza en estado pausado

  Se ha corregido el problema de pausa que se produce cuando el vídeo se pausa al entrar en reproducción.
* (ZD #30371): La hora de inicio de AdBreak cambia cuando insertamos más de 2 anuncios en un flujo lineal

  Se ha corregido el error al intentar reproducir contenido en Apple TV, que impedía la reproducción por completo
* (ZD #32146)- No se recibe PTMediaPlayerStatusError por el contenido de HLS Live al bloquear la beta de desarrollo de iOS 11

  No se recibe ningún error PTMediaPlayerStatusError para el contenido de HLS Live y VOD al bloquear con Charles (Colocar conexión y 403)
* (ZD #29242): La reproducción de vídeo de Airplay falla con los anuncios activados

  Cuando los anuncios están activados y AirPlay está habilitado para comenzar a reproducir un vídeo, la reproducción de vídeo nunca se inicia y no se muestra ningún error
* (ZD#33341) - Los déclencheur de DRMInterface.h generan advertencias en Xcode 9

  Se han corregido dos prototipos de bloques en DRMInterface.h a los que les faltaba la palabra &quot;void&quot; en sus listas de parámetros
* (ZD#31979): No se compila/ejecuta cuando es iOS 10 o posterior para iPhone 7/iPhone7+

  Se ha solucionado que la compilación de documentos del IB para versiones anteriores a iOS 7 ya no es compatible
* (ZD#32920): Pantalla en blanco dentro de una pausa publicitaria y sin finalización de la pausa publicitaria

  Cuando una pausa publicitaria presenta instancias de anuncio y una vez finalizada una instancia de anuncio, se muestra una pantalla en blanco
* (ZD#32509): Deshabilitar la grabación de pantalla de iOS 11 Deshabilitar la grabación de pantalla en iOS 11

* (ZD#33179) - Fallo de evento intermitente en iOS11

  Se ha corregido el error de evento en iOS 11

**Versión 1.4.40** (1.4.40.72)

* (ZD #32465): el reproductor no puede gestionar listas de reproducción combinadas.

  Llame a finishLoadingWithError(with: Error) para que la base AV pruebe secuencias alternativas o conmutación por error de déclencheur.

* (ZD #31951): Error de TVSDK durante las rotaciones de licencias.

  Se ha corregido el problema de rotación de licencias.
* (ZD #31951): Pantalla en blanco dentro de una pausa publicitaria y sin finalización de la pausa publicitaria.

  Se ha corregido un problema por el que los anuncios VPAID de Facebook devolvían a menudo varios bloques CDATA en un solo nodo \&amp;lt;AdParameters\&amp;gt; VAST.
* (ZD #33336) - [iOS] TVSDK: Los pods de anuncios no se rellenan, a pesar de que Freewheel haya devuelto suficientes anuncios.

  Se ha creado una relación principal-secundario entre el anuncio de secuencia y el anuncio de reserva y la ordenación basada en la secuencia principal y el índice.

**Versión 1.4.39** (1.4.39.43)

* (ZD #32178): la versión de TVSDK de iOS es incorrecta.

  La salida de la versión de TVSDK en los archivos de registro era 1.0.211. Se ha corregido para que muestre la versión correcta.

* (ZD #32199) Carga lenta de publicidad: no se muestra el vídeo para el contenido.

  La cronología de Adbreak local que no se inicializaba anteriormente, ahora se actualiza antes de su uso.

* (ZD #27528): el vídeo, el audio o ambos se bloquean entre 1 y 45 segundos después de que se inicie la reproducción de un recurso, si el audio secundario está establecido en no predeterminado en iOS 1.2.

  Prepare e informe pistas de audio en estado Ready.

* (ZD #30411) - Puede obtener resultados inesperados como no audio o audio incorrecto, si elige un idioma Sap secundario.

  Prepare e informe pistas de audio en estado Ready.

* (ZD #32199) Carga lenta de publicidad: no se muestra el vídeo para el contenido.

  La cronología de Adbreak local que no se inicializaba anteriormente, ahora se actualiza antes de su uso.

* (ZD #27528): el vídeo, el audio o ambos se bloquean entre 1 y 45 segundos después de que se inicie la reproducción de un recurso, si el audio secundario está establecido en no predeterminado en iOS 1.2.

  Prepare e informe pistas de audio en estado Ready.

* (ZD #30411) - Puede obtener resultados inesperados como no audio o audio incorrecto, si elige un idioma Sap secundario.

  Prepare e informe pistas de audio en estado Ready.

**Versión 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Agregar AdSystem y el ID creativo a las solicitudes de CRS

Uso del ID creativo y AdSystem en solicitudes CRS basadas en reglas de normalización CRS

* (ZD #29176): error en PTAdPolicyDeligate satAdBreakAsWatched:position

Ahora se gestiona el bloqueo debido a un AdBreak vacío.

* (ZD #30125): Los anuncios programáticos no funcionan en la plataforma de iOS

Se ha agregado compatibilidad con anuncios programáticos en iOS.

* (ZD #30782) - Notificación #EXT-X-PROGRAM-DATE-TIME

El evento de metadatos cronometrados no se activa para la etiqueta # EXT-X-PROGRAM-DATE-TIME con flujos DRM en directo.

**Versión 1.4.37 (1.4.37.842)**

* (ZD #28950 ): Problema de reproducción de VOD

Problema de reproducción cuando la etiqueta # EXT-X-PLAYLIST-TYPE del flujo se establece en Event en lugar de VOD

* (ZD #29281) - iOS: Agregar AdSystem y el ID creativo a las solicitudes de CRS

Uso de Creative Id y AdSystem en solicitudes CRS basadas en reglas de normalización CRS.

* (ZD #29462): El anuncio de TremorHub en A&amp;E VOD provoca un bloqueo en las aplicaciones de iOS

**Versión 1.4.36 (1.4.36.835)**

* (ZD #29418): Las señales con una duración 0 (#EXT-X-CUE-OUT:0.000) hacen que iOS TVSDK detenga o bloquee la reproducción.

El problema se soluciona y la reproducción se inicia correctamente.

* (ZD #29462): El anuncio en VOD provoca un bloqueo en iOS TVSDK .

El problema se ha corregido. iOS TVSDK está generando una excepción (AUDNetworkAdInfo::initWithAdId) y no la está administrando. La excepción se debe a un ID de anuncio vacío.

* (ZD #29281): agregue AdSystem y un ID creativo a las solicitudes de CRS.

Incluya AdSystem y CreativeId como nuevos parámetros en las solicitudes 1401 y 1403 (todos los demás parámetros son iguales).

**Versión 1.4.35** (1.4.35.830)

* (ZD #27830): Es necesario determinar mediante programación la diferencia entre los subtítulos y los subtítulos cerrados en iOS.

TVSDK ahora expone los dos tipos que se pueden utilizar para filtrar el tipo de rótulo requerido.

* (ZD #29160): Las señales de publicidad EXT-X-CUE-OUT no se insertan correctamente en TVSDK iOS.

Con EXT-X-CUE-OUT midroll anuncio está jugando ahora.

* (ZD #29100): La aplicación se bloquea cuando el usuario se desplaza hasta el final de una película.

Se han corregido varios bloqueos relacionados con la sincronización.

* (ZD #28785), (ZD #27712) y (ZD #25076): La aplicación de iOS se bloquea durante los grandes eventos en directo.

Se han corregido varios bloqueos relacionados con la sincronización.

**Versión 1.4.34** (1.4.34.815 para iOS 6.0+)

* (ZD# 28481): interrupción de FER debido a que la clave incorrecta se anexa al final de una pausa publicitaria para esos flujos FER

Para un flujo FER, la clave antes de la pausa publicitaria se inserta después del final de la pausa publicitaria. Este problema se resolvió adjuntando el *clave vista por última vez* al final de la pausa publicitaria.

**Versión 1.4.33** (1.4.33.803 para iOS 6.0+)

* (ZD# 21701) Habilitar CRS para subcuentas

Se habilita enviando la URL creativa original para la solicitud CRS 1401 en lugar de la URL normalizada, según el requisito del back-end CRS.

* (ZD# 26218): problema de carga de PSDKResources.bundle

Este problema se resolvió actualizando la carga de recursos para buscar en todos los paquetes disponibles.

* (ZD# 27460) Primera llamada de anuncio de Midroll: POST a cdn.auditude<span></span>.com devolviendo 403.

La nueva cuenta de CDN no puede gestionar una solicitud de CDN de POST. Este problema se resolvió actualizando el código para que la `cdn.auditude.com` solicitud de anuncio para ser GET en lugar de POST.

**Versión 1.4.32** (1.4.32.792 para iOS 6.0+)

* (ZD# 27132) Compatibilidad con valores decimales para pausas publicitarias VMAP.

Cuando el contenido no se segmentaba a lo largo de las pausas publicitarias definidas, los números enteros provocaban ubicaciones de anuncios inesperadas. El problema se resolvió al no convertir los valores decimales en enteros.

* (ZD# 27189) El contenido de AES con la etiqueta EXT-X-DISCONTINUITY-SEQUENCE no se reproduce correctamente.

El problema se resolvió colocando la etiqueta al principio de la lista de reproducción.

**Versión 1.4.31** (1.4.31.785 para iOS 6.0+)

* (ZD# 24528) Implementar métricas de uso de TVSDK para la facturación

Para obtener más información, consulte [Métricas de facturación](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md).

* (ZD# 24642) Compatibilidad con Imagen en imagen para TVSDK

La función imagen en imagen, que en algunos casos no funcionaba correctamente, se ha corregido.

* (ZD# 25246) Señales de interrupción de publicidad incorrectas

Este problema se resolvió alineando las etiquetas de discontinuidad entre los manifiestos de variante.

* (ZD# 26218) El proceso de generación de la aplicación se complica al intentar incluir PSDKLibrary.framework en el marco de trabajo de la aplicación del cliente

Este problema se resolvió empaquetando PSDKLibrary.framework como se solicitó.

* (ZD# 26364) Compatibilidad con varias CDN para anuncios CRS
<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028) Retraso en la reproducción de algunos flujos en iOS 10.

Este problema se resolvió proporcionando una solución alternativa para los flujos que no tienen una extensión M3U8.

**Versión 1.4.30** (1.4.30.754 para iOS 6.0+)

Los siguientes problemas se resolvieron para TVSDK en esta versión:

* (ZD# 24180) Añadir un encabezado personalizado a la lista de permitidos

Se ha añadido un nuevo encabezado personalizado a la lista de permitidos de TVSDK.

* (ZD# 25016) El flujo de conmutación por error se selecciona aleatoriamente cuando se definen los parámetros de control ABR

Este problema se resolvió manteniendo los flujos ABR en orden cuando la configuración ABR se proporciona con la configuración de velocidad de bits inicial en un flujo que incluye direcciones URL de conmutación por error. Esto evitará reproducir los flujos de conmutación por error en lugar del principal.

* (ZD# 25076) Error en PTAuditudeAdResolver loadComplete

Se ha corregido un problema por el que se producía un bloqueo durante el inicio/parada rápido de varias instancias de PTMediaPlayer con anuncios.

* (ZD# 25960) No hay etiquetas suscritas adicionales que activen difusiones de notificación de cambio de metadatos

Problema en el cual una etiqueta suscrita no recibe una notificación cuando aparece antes de que se haya corregido el primer segmento del manifiesto.

* (ZD# 26084) El PSDK está lanzando un 106000.101000.-11833 error del decodificador no encontrado al pasar de la última pausa publicitaria al contenido de entretenimiento

Cuando el tiempo de inicio de la última pausa publicitaria desde VMAP cae antes de que se complete la duración total, en ciertas condiciones, la clave no se inserta hasta después del final de la última pausa publicitaria. Este problema se ha corregido.

* La biblioteca de Video Heartbeat (VHL) se ha actualizado a la versión 1.5.9 para resolver los siguientes problemas:

   * (ZD #22351) VHL: Analytics: duración de recursos de vídeo en directo

Este problema se resolvió agregando la API assetDuration a `PTVideoAnalyticsTrackingMetadata` para actualizar la duración del recurso para flujos en directo/lineales y proporcionar una lógica para comprobar el flujo en directo.

* (ZD# 22675) VHL: Analytics: Actualización de la duración de los recursos de vídeo en directo

Este problema es el mismo que el de ZD #22351.

* (ZD #25908) VHL: Analytics: Bloqueo de evento de Heartbeat de Adobe

Este problema se solucionó actualizando la implementación para utilizar la última versión de VHL para iOS 1.5.9 con el fin de mejorar la estabilidad y el rendimiento.

* (ZD #25956) VHL - Analytics: Se bloquea al reproducir vídeos repetidamente

Este problema es el mismo que el de ZD #25908.

**Versión 1.4.29** (1.4.29.743)

* (ZD# 23901) No se reproducen los anuncios de terceros

Este problema se resolvió moviéndose a la estructura de URL de CRS v3 para incluir el ID de zona en la URL empaquetada de nuevo.

* (ZD #25183) Problemas con la reproducción de DRM en tvOS y iOS

Este problema se resolvió proporcionando compatibilidad con varias etiquetas clave necesarias para la compatibilidad con múltiples DRM.

* (ZD# 25334) TVSDK no puede reproducir contenido compartido de cDVR

Este problema se resolvió impidiendo que TVSDK convirtiera cadenas vacías en URL absolutas.

* (ZD# 25347) Establecer un encabezado HTTP personalizado en el recurso AVURLA

Se ha agregado compatibilidad con encabezados personalizados en sus solicitudes de segmento a través de la clase PTNetworkConfiguration.

**Versión 1.4.28** (1.4.28.722)

* (ZD #24549) Varias llamadas de seguimiento de anuncios

Este problema se resolvía actualizando el administrador de la cronología para recibir notificaciones sobre un objeto específico cuando se creaban varios reproductores.

* (ZD #24758) PTManifestLogger no es compatible con iOS 8

Este problema se resolvió al actualizar la biblioteca de la utilidad del registrador al destino de implementación de la versión 7.0.

* (ZD #24775) Retraso en la emisión debido a anuncios

Este problema se resolvió calculando correctamente la deriva de duración en las listas de reproducción de eventos.

* (ZD #24799) Algunos de los episodios no se reproducen en la aplicación de iOS

Este problema se resolvía utilizando el servidor web local para subtítulos cuando los archivos WebVTT están restringidos geográficamente.

**Versión 1.4.27** (1.4.27.711) para iOS 6.0+

* (ZD #24089): Optimizaciones para la resolución de anuncios en emisiones DVR largas

Este problema se resolvió añadiendo varias optimizaciones para reducir el tiempo necesario para procesar la ventana del DVR en emisiones lineales o en directo.

* (ZD #21554): señalizaciones de error de TVSDK no activadas para el tipo de aplicación = video/mp4

Este problema se resolvió permitiendo que el reproductor hiciera ping a las direcciones URL de seguimiento de errores correctas en formatos de recurso no válidos.

* (ZD #24424): el bloqueo del tipo EXC_BAD_ACCESS_KERN_INVALID_ADDRESS se origina desde PSDKLib para iOS en dispositivos de hardware más nuevos.

Se ha corregido un bloqueo que se producía debido a una instancia de reproductor de medios desasignada, cuando la reproducción cambia rápidamente entre diferentes flujos.

* (ZD #24575): error en TVSDK en dispositivos de 32 bits cuando enableDebugLog=true

Se ha corregido el problema en el formato de registro que ocasionaba el bloqueo en dispositivos de 32 bits cuando el registro está habilitado.

**Versión 1.4.26** (1.4.26.702) para iOS 6.0+

* (ZD# 20213): TVSDK FW debe ser dinámico/modular para XCode7

   * Se corrigió actualizando las bibliotecas con compatibilidad con módulos

**Versión 1.4.25** (1.4.25.684) para iOS 6.0+

* (ZD #19629) - Video en vivo se pausa al entrar en Airplay a ATV 4

Este problema se resolvió añadiendo un período de espera después de eliminar los elementos antiguos, pero antes de añadir nuevos elementos a AVQueuePlayer. Sin el periodo de espera, las notificaciones se envían al elemento incorrecto.

* (ZD #19856): no se muestran subtítulos cuando está habilitado de forma predeterminada

Se han corregido los problemas en la lista de reproducción de webvtt, que provocaban que los subtítulos no se mostraran correctamente.

* (ZD #21590): Rendimiento y seguimiento de vídeo en las últimas versiones de origen

Se ha corregido el problema de la duración del vídeo que faltaba en Video Analytics.

* (ZD #20202): Al configurar el estilo de los subtítulos personalizados, se bloquea la aplicación de iOS

Este problema se resolvió añadiendo comprobaciones de objetos nulos adicionales al establecer estilos de subtítulos.

* (ZD #20709): la duración del vídeo aparece como 0 en el seguimiento de inicio de vídeo

Este problema es el mismo que (ZD #21590).

* (ZD #22280): La duración del vídeo de Analytics se establece en 0

Este problema es el mismo que (ZD #21590).

* (ZD #22592) - Problemas con Airplay en Primetime

Este problema es el mismo que (ZD #19629).

* (ZD#22922): Conmutación manual de la velocidad de bits para iOS

Este problema se resolvió proporcionando una opción para especificar la velocidad de bits máxima.

* (ZD #23084): conformidad de Apple para redes solo IPv6

Se han eliminado los símbolos no recomendados por Apple para la compatibilidad con IPv6.

**Versión 1.4.24** (1.4.24.661) para iOS 6.0+

* ZD #2548): Compatibilidad de Primetime con publicidad interactiva en dispositivos móviles: VPAID 2.0

Este problema se resolvió al actualizar la lógica para mostrar la vista del reproductor si un anuncio VPAID no se reproduce.

* (ZD #20101): La implementación de capítulos personalizados activa el evento de inicio de capítulos durante la reproducción del anuncio

Este problema se solucionó actualizando VideoAnalyticsTracker para detectar correctamente el inicio y la finalización de capítulos al realizar la transición entre los límites de capítulos y no capítulos.

* (ZD #20784): Analytics: la activación de contenido finaliza las transiciones de vídeo en directo

Este problema se solucionó añadiendo una lógica para almacenar en déclencheur manualmente la finalización del contenido durante una sesión de seguimiento de vídeo.

Se han actualizado las bibliotecas siguientes:

* Biblioteca de Adobe Mobile a 4.10.0
* Biblioteca VHL a 1.5.6
* Biblioteca VHL-Nielsen a 1.6.7
* (ZD #21855) - Los subtítulos no se reproducen después del mid-roll

En este número, las etiquetas de discontinuidad duplicadas causaban que los subtítulos no aparecieran después de la emisión. Este problema se resolvió eliminando las etiquetas de discontinuidad contiguas.

* (ZD #21994): Cadena fuera de los límites en PTHLSUtils

La causa más probable del bloqueo es cuando una EXT-X-KEY tiene una dirección URL rodeada de comillas.

* ZD #22074): AUDVAST Se produce un bloqueo una vez al minuto en iOS

En la versión 1.4.23, se solucionó el bloqueo provocado por la presencia de caracteres no seguros en una URL de redireccionamiento VAST. Sin embargo, TVSDK seguía omitiendo estos anuncios.

Este problema se resolvió gestionando los caracteres no seguros y permitiendo que se reprodujeran los anuncios.

* (ZD #22694) - PTMediaPlayer.  El reproductor oculta la vista

Este problema se resolvió al actualizar la lógica para mostrar la vista del reproductor si un anuncio VPAID no se reproduce.

**Versión 1.4.23** (1.4.23.641) para iOS 6.0+

* (ZD #18016): No hay respuesta del SDK de Primetime con una condición de red incorrecta

Este problema se resolvió mejorando la notificación de errores cuando se produce un error grave de AVFfoundation y para permitir que la aplicación gestione el reinicio después del error.

* (ZD #20580): Error en PTSplicerManager

Este problema se resolvió proporcionando protección adicional contra los problemas de concurrencia que causan el bloqueo.

* (ZD #21782): 10100 de código de error de iOS

Se ha corregido el problema por el que TVSDK devolvía un error de 101000 al iniciar la reproducción en flujos DRM de acceso al Adobe.

* (ZD #21889): La reproducción de anuncios en línea y contenido sin conexión falla

Problema en el cual la reproducción fallaba después de que se hubiera corregido un anuncio en contenido sin conexión cifrado de AES.

* (ZD #22074): AUDVAST Se produce un bloqueo una vez al minuto en iOS

Este problema se resolvió mejorando la gestión de las etiquetas de anuncios VAST de terceros que tienen caracteres no válidos en la dirección URL.

* (ZD #22257): TVSDK no puede reproducir el flujo DRM

Se ha corregido el problema del TVSDK que devolvía un error de 101000 al iniciar la reproducción en flujos DRM de acceso al Adobe.

**Versión 1.4.22** (1.4.22.627) para iOS 6.0+

* (ZD #18709): Error en el TVSDK para iOS

Se ha corregido el problema de un bloqueo que se producía en algunos flujos protegidos por DRM de acceso de Adobe.

* (ZD #18850): Actualice la lógica de selección creativa basada en las reglas de CRS

Este problema se resolvió añadiendo un archivo de configuración .json para especificar la prioridad de selección creativa.

* (ZD #19770): La fuente de vídeo AES protegida ya no se reproduce

Se ha corregido el problema por el cual algunos flujos redirigidos 302 no se reproducían.

* (ZD #19629) - Video en vivo se pausa al entrar en Airplay a ATV 4

Este problema se resolvió añadiendo una solución para la pausa de vídeo en directo cuando la reproducción en directo está activada para dispositivos Apple TV 4. El problema parece ser un problema de AppleTV 4.

* (ZD #21119): El TVSDK se detiene después de la reproducción del anuncio

Se ha agregado compatibilidad con flujos cifrados AES con una secuencia IV al utilizar la inserción de publicidad.

* (ZD #21125): Regreso antes de la pausa publicitaria en directo/lineal

Se ha agregado compatibilidad para volver de una pausa publicitaria antes de que se reproduzca hasta su finalización. El retorno anticipado se indica mediante una etiqueta de manifiesto personalizada.

* (ZD #21224) - Soporte de Airplay para emisiones tokenizadas de Akamai

Las API se han agregado a la clase PTNetworkConfiguration para anexar cookies como parámetros de URL en segmentos para determinados flujos tokenizados de Akamai.

* (ZD #21287) - Registro externo

Se ha corregido un problema con algunas instrucciones de registro que se muestran de forma predeterminada en la consola xcode incluso cuando el registro está deshabilitado.

* (ZD #21446): Los eventos de pausa publicitaria a veces no se activan mediante el TVSDK

En los flujos de EVENTO, las pausas publicitarias no se activan correctamente en la versión anterior. Esta compilación soluciona este problema.

**1.4.21** (1.4.21.605) para iOS 6.0+

* (ZD #20749): La reserva omite las respuestas VAST no vacías; se activan las direcciones URL de seguimiento de anuncios adicionales

Se ha resuelto un problema con los pings duplicados en los anuncios de reserva.

**1.4.20** (1.4.20.590) para iOS 6.0+

* (ZD #18639): El TVSDK utiliza una cantidad excesiva de CPU/recursos en un recurso de grabación en caliente de larga duración

El uso excesivo de CPU/recursos se ha corregido en los dos niveles. En primer lugar, dejando que la función de actualización de tiempo se ejecute en una cola global, en lugar del subproceso principal, y optimizando el uso de CPU para analizar el manifiesto con el m3u8 previamente procesado y almacenado en caché.

* (ZD #19349): Los anuncios previos a la emisión se omiten al limitar la conexión de red.

Este problema se resolvió proporcionando un evento de tiempo de espera (requestTimeout) a la aplicación y a adMetadata  La API adRequestTimeout anula el tiempo de espera predeterminado de 10 segundos.

* (ZD #19446) - Falta la notificación en los flujos en directo

Este problema se resolvió permitiendo que la aplicación se suscribiera a EXT-X-PROGRAM-DATE-TIME en emisiones en directo.

* (ZD #19459): se bloquea al preparar audio alternativo con PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Bloqueo - [PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]

Este problema es el mismo que el de Zendesk #19459.

* (ZD #19574): TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM

En la carga inicial del archivo de manifiesto en PTMediaPlayerItem.prepareToPlay, si se produce un error al cargar el manifiesto, TVSDK no informa del cuerpo de la respuesta de error a la aplicación.

Este problema se resolvió permitiendo que TVSDK informara de la respuesta de error como un error a la aplicación.

* (ZD #19615): la lógica de reserva no funciona

En la implementación actual, los anuncios de reserva se omitían y no se volvían a empaquetar a menos que estos anuncios estuvieran en formato m3u8. Este problema se resolvió añadiendo también la compatibilidad con el reempaquetado de anuncios de reserva.

* (ZD #19770): TVSDK no reproduce ningún contenido AES protegido con redirección 302

El problema de redirección se ha corregido porque cleanConnectionData estaba borrando la dirección URL de redirección antes de que se pudiera usar para analizar el manifiesto.

* (ZD #19856): Los subtítulos no se muestran para algunas tasas de bits cuando está habilitado de forma predeterminada

Este problema se resolvió gestionando el error de iOS para los segmentos de los flujos en los que los subtítulos no se muestran.

* (ZD #19868): El TVSDK se bloquea cuando se trafica un elemento creativo no válido

Se ha corregido el bloqueo en el TVSDK que desasignaba incorrectamente una instancia del vasto analizador.

* (ZD #20180): Los anuncios VPAID se omiten ocasionalmente

El tipo MIME de JavaScript no siempre se incluía ni se consideraba un tipo MIME válido. Este problema se resolvió incluyendo JavaScript como un tipo MIME válido.

* (ZD #20749): La reserva omite las respuestas VAST no vacías; se activan las direcciones URL de seguimiento de anuncios adicionales

Se ha solucionado el problema en el que algunos de los creativos no se están reempaquetando.

**Versión 1.4.19** (1.4.19.563) para iOS 6.0+

* ZD #18639): el TVSDK utiliza una cantidad excesiva de CPU/recursos en un recurso de grabación en caliente de larga duración

Este problema se resolvió optimizando la reescritura de la lista de reproducción DRM m3u8 para almacenar en caché bits de la lista de reproducción que se han reescrito anteriormente. Esto es más relevante cuando reproduce flujos m3u8 en directo para los que el m3u8 se descarga después de cada descarga de segmento.

* (ZD#18956) - player.drmManager es nil cuando el punto de interrupción se establece en iOS Demo Player

Este problema se resolvió al actualizar la implementación de la API PTMediaPlayer.drmManager para recoger DRManager del marco de DRM.

**Versión 1.4.18** ( 1.4.18.557) para iOS 6.0+

* (ZD #18844) Seguimiento del cabezal de reproducción para contenido en directo en el reproductor iOS.

Este problema se resolvió permitiendo que las aplicaciones establecieran su propio valor de cabezal de reproducción.

* #18518 de Zendesk: si no se especifica el nombre del vídeo, el nombre predeterminado de TVSDK es *Reproductor basado en PSDK.*

Este problema se resolvió eliminando el valor predeterminado del nombre del reproductor.

**Versión 1.4.17** (1.4.17.545) para iOS 6.0+

* Zendesk #2228: Mejore el TVSDK para devolver la respuesta JSON de la recuperación de un manifiesto

En lugar de enviar un error cuando el contenido no es M3U8, el marco de DRM devuelve un metadato DRM nulo. El problema se resolvía añadiendo metadatos para exponer el contenido cuando se producía la notificación M3U8_PARSER_ERROR.

* Zendesk #2231: Error devuelto al recuperar el manifiesto no disponible en MediaPlayerNotification

La misma resolución que Zendesk #2228

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` la macro no se rellena

Se ha resuelto el problema del SDK de Auditude que no puede enviar un ping cuando la URL de seguimiento tiene espacios al principio.

* #17294 de Zendesk: error SecKeyRawSign

Se ha resuelto un posible bloqueo cuando el código del cliente utiliza la cadena de claves.

* Zendesk #18008 - Cookies de soporte para iOS8+ para admitir flujos tokenizados

Los flujos tokenizados de Akamai requieren que las cookies se envíen en solicitudes de segmento, lo cual no era posible en iOS 7 y versiones anteriores. A partir de iOS 8, Apple ha agregado una API que permite pasar cookies para solicitudes de segmentos. Esta compatibilidad ya está disponible en el TVSDK . También se ha agregado compatibilidad para enviar un usuario-agente, si está disponible.

* Zendesk #18166 - TVSDK 1.4.15 da cientos de advertencias cuando se compila con DWARF con las opciones de archivo dSYM

Se han resuelto todas las advertencias.

**Nota**: Se han añadido bibliotecas compatibles con tvOS para TVSDK

**Versión 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S se bloquea durante la reproducción

Revertir la dependencia de OKHTTP en la audiencia para CRS porque TVSDK ahora utiliza directamente httpurlconnection en lugar de curl. El problema se resolvió borrando excepciones antes de realizar otra llamada JNI.

* Zendesk #4487 - Seguimiento del canal lineal de contenido

El problema se resolvió reinicializando el rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* Zendesk #17919 - Android - la búsqueda de contenido causa un error de latido

El problema era resolver el latido en un estado de error cuando había una búsqueda en un capítulo

* Zendesk #18053: La aplicación que utiliza el SDK de TVSDK se bloquea en Marshmallow

TVSDK se bloqueaba en el sistema operativo Android M cuando la biblioteca TVSDK utiliza código de neón que hace la conversión de color YUV -> RGB. Este problema se resolvió actualizando las funciones que lo causan mediante el uso de una versión de código que no es de neón

* Zendesk #18072 - Android M - Error en la aplicación

Este bloqueo se produce al llamar a las API MediaCodecList y MediaCodecInfo al comprobar si el perfil y el nivel son compatibles. El Adobe busca la compatibilidad de Google para obtener más información. Este problema se solucionó cargando toda la información del códec con antelación para evitar llamar a estas API solo cuando se necesita información del códec.

* Zendesk #18074 - Subtítulos en árabe que no funcionan en Nexus con Android 6.0

Este problema se resolvió al proporcionar compatibilidad con el mapa de fuentes CTS de Android.

**Versión 1.4.15** (1.4.15.512) para iOS 6.0+

**Nota**: el módulo Nielsen se ha eliminado de la compilación de TVSDK, pero el TVSDK se actualizará en un futuro próximo con un nuevo módulo de integración de Nielsen.

* (ZD #2228): Error devuelto al recuperar el manifiesto no disponible en MediaPlayerNotification

Se han agregado metadatos para exponer el contenido cuando se produce la notificación M3U8_PARSER_ERROR.

* (ZD #4437): Bloqueos dentro del SDK de Adobe Primetime

Se ha corregido un bloqueo notificado al preparar subtítulos/audio alternativo.

* (ZD #4487): Seguimiento del canal lineal de contenido

Se permite reiniciar el rastreador de latidos de vídeo durante una sesión de reproducción de flujo lineal.

**Versión 1.4.14** (1.4.14.498) para iOS 6.0+

* (ZD #17260): Error en playlistManagerForURL

Se ha corregido un bloqueo intermitente debido a problemas de concurrencia.

**Versión 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` la macro no se rellena

   * El código de error 400 se expone si el anuncio en línea tiene un error creativo.
   * `[ERRORCODE]` La macro tendrá codificación URL.

* (ZD #3865) Integración de Heartbeat con anuncios IMA

Se ha corregido un error por el cual se informaba de la duración del vídeo incorrectamente.

* Se ha actualizado el reproductor de demostración de TVSDK para admitir iOS 9

Para admitir correctamente iOS 9, debe configurar las excepciones de Application Transportation Security. A los efectos de la demostración, el ATS está completamente desactivado.

**Versión 1.4.12** (1.4.12.464) para iOS 6.0+

* (ZD #4521) Prueba de CRS del lado del cliente y SSAI

Se ha corregido un MD5 inverso incorrecto en la URL 3P.

**Versión 1.4.12** (1.4.12.463) para iOS 6.0+

* (ZD #2751) CSAI y CRS | Mejorar: Gestionar elementos dinámicos en determinadas URL de archivos multimedia.

Se ha actualizado el servicio de reempaquetado creativo para que gestione correctamente los anuncios con direcciones URL creativas dinámicas.

* (ZD #3654) Pérdida de memoria en la versión de PSDK después de 1.3.4.166

Se ha corregido una fuga de memoria en drmFramework con reproducción regular en dispositivos iOS 8.2

* (ZD #3988) El predesplazamiento se omite al buscar de nuevo en él después de la primera reproducción

Se ha corregido un error para que las políticas publicitarias se pudieran desactivar correctamente.

* (ZD #4017) Solicitud de la API de iOS para forzar la reproducción de la publicidad en la búsqueda hacia atrás

Resuelto con corrección para ZD #4279

* (ZD #4279) Inserción de publicidad de TVSDK de HLS -302 problema de redirección en iOS y escritorio

Se ha corregido un error por el que un recurso publicitario utilizaba una URL de redireccionamiento relativa

**Versión 1.4.9** (1.4.9.427) para iOS 6.0+

* (ZD #3075) Problema de accesibilidad de Internet - iOS

Se ha añadido una notificación para detectar cuándo se ha detenido la reproducción.

* (ZD #3193) Solicitud de una API de cambio de perfil en TVSDK

Se ha actualizado PTPlaybackInformation para exponer el parámetro indicadoBitrate actualizado. Se ha actualizado la notificación BITRATE_CHANGE para que sea más fiable y precisa en cuanto al tiempo para las velocidades de bits notificadas del M3U8.

* (ZD #3324) Problema de informe de anuncios de Primetime cuando no hay medios publicitarios en VMAP

Compatibilidad para hacer ping a las URL vacías de seguimiento de pausas publicitarias. TVSDK ahora verificará los pings de inicio y finalización de las pausas publicitarias vacías

**Versión 1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7 se bloquea en las reproducciones de eventos completos

**Versión 1.4.7** (1.4.7.382)

* (ZD #2197) Seguimiento de errores de publicidad. Se ha agregado una notificación para el recurso que no se ha podido cargar el manifiesto.
* (ZD #2894) El reproductor realiza 4 solicitudes de manifiesto de nivel superior durante la reproducción.
* (ZD #2992) Auditude que informa de duraciones e identificadores extraños.

**Versión 1.4.6**(1.4.6.325)

* (ZD #2197) Seguimiento de errores de publicidad. Se ha añadido una notificación para el recurso que no se ha podido cargar el manifiesto

**Versión 1.4.5** (1.4.5.283)

* (ZD #2141) Implementación de Analytics para la aplicación TreeHouse, añadió la biblioteca AdobeAnalyticsPlugin.a para crear el paquete
* Actualización de la biblioteca de Video Heartbeats a 1.4.1.2
* (PTPALY-4226) (relacionado con ZD #2423) La realización del restablecimiento de DRM puede dar como resultado la eliminación de los datos del documento de aplicación.

**Versión 1.4.4** (1.4.4.242)

* Actualización de la biblioteca de Video Heartbeats (VHL) a 1.4.1.

* (ZD #2435) La documentación del SDK de TV sobre Analytics necesita actualizaciones

**Versión 1.4.2** (1.4.2.2010 : iOS 6.0+)

* (ZD #1129) _player.currentItem.audioOptions devuelve vacío
* (ZD #2109) Primetime PSDK 1.4.1.125 no funciona con Xcode 5.1.1
* (ZD #2137) Bloqueo en PSDK en iOS cuando no se pueden cargar metadatos DRM

**Versión 1.4.1** (1.4.1.125)

* (ZD #1107) Símbolos duplicados de CocoaLumberjack
* (ZD #1644) Modificar el agente de usuario de iOS para segmentación e informes
* (ZD #1850) Archivos de Cocoa Lumberjack incluidos en el SDK de iOS
* (ZD#1908) PSDK ignora las etiquetas personalizadas si hay más de 1

**Versión 1.4.0** (1.4.0.32)

* Zendesk #1024: función para eliminar el anuncio del flujo a través del manifiesto

## Problemas conocidos en 1.4 {#known-issues-in}

* En iOS TVSDK , todos los anuncios se vinculan al manifiesto de contenido. Los comportamientos de anuncio se implementan mediante la búsqueda en función de la duración de los segmentos de contenido y publicidad. Por lo tanto, si las duraciones de los segmentos no son precisas, es posible que la búsqueda no siempre termine en el fotograma exacto del principio o el final de la pausa publicitaria. Incluso si las duraciones son inferiores al fotograma, existe una tolerancia que la propia plataforma impone a la búsqueda y puede haber algunos fotogramas o anuncios o contenido mostrado. Esto es una limitación de la plataforma y de la forma en que la inserción de publicidad funciona con TVSDK en iOS.
* La decisión de omitir se produce en el evento de búsqueda en este caso. Sin embargo, dado que las duraciones de los segmentos de publicidad en el manifiesto no representan con precisión la duración real del anuncio, la búsqueda no es precisa de fotogramas. Por lo tanto, se ven algunos fotogramas del anuncio cuando se aplican las políticas publicitarias.
* RECORDING_ERROR: Se ha producido un error al grabar la pantalla.
* Es posible que experimente que el vídeo de rotación de licencias no se reproduzca en iOS 11 y se reproducirá bien en iOS 9.x y iOS 10.x.
* En la compatibilidad con VPAID 2.0, si la reproducción está activa a través de AirPlay, se omiten los anuncios VPAID.
* drmNativeInterface.framework no se vincula correctamente cuando el destino mínimo se establece en iOS7 (o posterior).\
  Solución alternativa: especifique explícitamente la variable `libstdc++6`.  biblioteca dylib como se indica a continuación: Vaya a Target->Fases de compilación->Vincular binario con bibliotecas y añada `libstdc++.6.dylib`.

* El anuncio posterior a la emisión no se inserta para reemplazar la API.
* Al buscar en una pausa publicitaria (sin salir de ella), se emite una notificación de inicio de pausa publicitaria duplicada
* La configuración de currentTimeUpdateInterval no tiene ningún efecto.\
  Nota: En determinadas versiones de iOS, el sistema operativo no carga automáticamente los recursos dentro de PSDKLibrary.framework. Es importante copiar manualmente el paquete PSDKResources.bundle en los recursos del paquete de la aplicación: Vaya a &quot;Fases de compilación&quot; y copie los recursos del paquete.
* La aplicación de referencia no se puede crear con Xcode 8 o versiones anteriores. iOS TVSDK versión 1.4.41 en adelante, utilice Xcode 9 para compilar.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
