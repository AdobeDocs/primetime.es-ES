---
title: Notas de la versión de TVSDK 1.4 para iOS
seo-title: Notas de la versión de TVSDK 1.4 para iOS
description: Las notas de la versión de TVSDK 1.4 para iOS describen las novedades o los cambios, los problemas conocidos y resueltos y los problemas de dispositivo en TVSDK iOS 1.4
seo-description: Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK iOS 1.4
uuid: c1df12bd-aa21-47e8-ade4-1e497882ce9b
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 452f8699-7857-49ab-9caa-22204b19fe4a
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '6578'
ht-degree: 0%

---


# Notas de la versión de TVSDK 1.4 para iOS {#tvsdk-for-ios-release-notes}

Las notas de la versión de TVSDK 1.4 para iOS describen las novedades o los cambios, los problemas conocidos y resueltos y los problemas de dispositivo en TVSDK iOS 1.4.

## Nuevas funciones {#new-features}

**Versión 1.4.45**

* Para cumplir con Xcode10, TVSDK se ha movido de &quot;`libstdc++`&quot; a &quot;`libc++`&quot; y, como resultado, la versión mínima admitida es iOS 7. Anteriormente era iOS 6.

**Versión 1.4.44**

* Esta versión no incorpora nuevas funciones ni mejoras.

**Versión 1.4.43**

* Experiencia similar a la televisión de poder unirse en medio de un anuncio sin activar el seguimiento parcial del anuncio.\
   Ejemplo: El usuario se une en el medio (a los 40 segundos) de una pausa publicitaria de 90 segundos que consta de tres anuncios de 30 segundos. Pasarán 10 segundos desde el segundo anuncio de la pausa.

   * El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.
   * Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Los rastreadores solo para el tercer anuncio se activan.

* Se Añadió la propiedad enableVodPreroll del tipo booleano en la interfaz PTAdMetadata. La propiedad se puede utilizar para habilitar el predesplazamiento en un flujo de VoD. Si enableVodPreroll es NO, PSDK no reproduce pre-roll. Esto, sin embargo, no afecta a los midrolls. El valor predeterminado de enableVodPreroll es YES.
* la API ClosedCaptionDisplayEnabled de la interfaz de PTMediaPlayer está marcada como obsoleta desde iOS v1.4.43 en adelante. Para determinar si hay subtítulos opcionales disponibles para un PTMediaPlayerItem determinado, examine la propiedad subtitlesOptions de PTMediaPlayerMediaItem.

**Versión 1.4.42**

Esta versión no incorpora nuevas funciones. Para obtener una lista de los problemas solucionados, consulte Problemas resueltos.

**Versión 1.4.41**

Cambios en la API:

* **isSecure**: Se ha introducido una nueva API isSecure para evitar que el reproductor grabe y genere un error. El valor predeterminado es true.
* **allowExternalRecording**: Se ha introducido una nueva API para permitir la creación de reflejo de reproducción aérea para un contenido seguro. El reflejo de reproducción aérea se trata como una grabación, por lo tanto el valor allowExternalRecording debe establecerse en &#39;True&#39;, para permitir el reflejo de reproducción aérea o establecerse en &#39;False&#39; para detener el reflejo de reproducción para contenido seguro. De forma predeterminada, el valor es true.

**Versión 1.4.40**

No hay nuevas funciones.

**Versión 1.4.39**

* iOS TVSDK está certificado con VHL 2.0.1 y con VHL 2.0.1 con Nielsen.
* iOS TVSDK se actualiza para realizar solicitudes CRS desde el nuevo host de Akamai `primetime-a.akamaihd.net`.
* La nueva configuración de nombre de host proporciona envío de recursos CRS a través de HTTP y HTTPS (SSL) a buena escala.

**Versión 1.4.36**

Integrar y certificar VHL 2.0 en iOS TVSDK : Reduzca la barrera en la implementación de VideoHeartbeatLibrary disminuyendo la complejidad de las API.

**Versión 1.4.34**

* Información de publicidad de red

   Las API de TVSDK ahora proporcionan información adicional sobre las respuestas de VAST de terceros. La ID de publicidad, el sistema de publicidad y las extensiones de publicidad VAST se proporcionan en `PTNetworkAdInfo` clase a la que se puede acceder mediante `networkAdInfo` la propiedad en un recurso de publicidad. Esta información se puede utilizar para la integración con otras plataformas de Ad Analytics como **Moat Analytics**.

**Versión 1.4.31**

* **Métricas** de facturación Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.

Cada vez que TVSDK genera un evento de inicio de flujo, el reproductor inicio enviar mensajes HTTP periódicamente al sistema de facturación de Adobe. El período, conocido como duración facturable, puede ser diferente para VOD estándar, VOD pro (anuncios intermedios habilitados) y contenido activo. La duración predeterminada para cada tipo de contenido es de 30 minutos, pero el contrato con Adobe determina los valores reales.

* **Compatibilidad con Multi-CDN para CRS** AdsTVSDK ahora es compatible con Multi-CDN para anuncios de CRS. Al proporcionar detalles de FTP para las publicidades de CRS, puede especificar ubicaciones de CDN distintas de la CDN predeterminada de propiedad de Adobe, como Akamai.

**Versión 1.4.29**

En la clase PTSDKConfig, se ha añadido la API forceHTTPS.

La clase PTSDKConfig proporciona métodos para aplicar SSL en las solicitudes realizadas a los servidores de Analytics, DRM y Video Primetime y de toma de decisiones. Para obtener más información, consulte los `forceHTTPS` métodos y `isForcingHTTPS` en esta clase. Si un manifiesto se carga a través de HTTPS, TVSDK conserva el uso de contenido de HTTPS y respeta este uso al cargar cualquier URL relativa de ese manifiesto.

**Nota**: Las solicitudes a dominios de terceros, como píxeles de seguimiento de publicidad, URL de publicidad y contenido, y solicitudes similares, no se modifican, y es responsabilidad de los proveedores de contenido y los servidores de publicidad proporcionar direcciones URL compatibles con HTTPS.

**Versión 1.4.18**

Primetime iOS TVSDK ahora es compatible con los elementos creativos de Javascript VPAID 2.0 para permitir una experiencia publicitaria interactiva y enriquecida.

Para obtener más información sobre VPAID 2.0, consulte Compatibilidad con [anuncios](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md)VPAID.

**Versión 1.4.17**

* tvOS

   El TVSDK admite aplicaciones nativas de tvOS.
* Se pueden reproducir los siguientes tipos de contenido:

   * VOD
   * Live Live
   * AES-128
   * Audio y subtítulos alternativos
   * FER

* Se pueden mostrar los siguientes tipos de publicidades:

   * Básico
   * VAST2
   * VAST3
   * VMA

* Actualmente no se admiten las siguientes funciones:

   * Administración de derechos digitales (DRM)
   * Letreros de publicidad
   * Lenguaje de marcado de TV (TVML)

**Versión 1.4.13**

**Nota**: El módulo Nielsen se ha eliminado de la compilación de TVSDK, el TVSDK se actualizará en un futuro próximo con un nuevo módulo de integración de Nielsen.

* **Acontecimiento publicitario, encadenamiento margarita en la lógica de selección de anuncios (Zendesk #3103)**

En el caso de anuncios VAST (creativos) con la regla de reserva activada, el TVSDK trata una publicidad con un tipo MIME no válido como una publicidad vacía e intenta utilizar las publicidades de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Reproducción de anuncios para anuncios](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md)VAST y VMAP.

**Versión 1.4.9**

* **Señalización de interrupción con sustitución de contenido alternativo**

Como parte de la actualización 1.4 de TVSDK, ahora también se admite entrar y volver de los apagones regionales contra el contenido lineal. TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de interrupción incluso cuando se muestra una programación alternativa en lugar de la programación original.

**Versión 1.4.8**

* **Video Heartbeat Library (VHL) actualizado a la versión 1.5**

   * Capacidad para enviar metadatos con inicio de vídeo y/o inicio de vídeo/anuncio/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño

**Versión 1.4.7**

* **Asistencia para la individualización in situ**

Compatibilidad con instalaciones in situ de Adobe Individualization Server para personalizar la solicitud de individualización del cliente para ir a otro extremo.

* **Protección de salida basada en resolución**

Las directivas DRM ahora pueden especificar la resolución más alta permitida, según las capacidades de protección de salida del dispositivo. Por ejemplo: &quot;Si HDCP está disponible, permita que se reproduzca contenido de hasta 1080p de resolución y, si HDCP no está disponible, permita que se reproduzca contenido de hasta 480p de resolución&quot;.

**Versión 1.4.4**

* **Actualización de Video Heartbeat Library (VHL) a la versión 1.4.1.1**

   * Se Añadió la capacidad de compilar diferentes casos de uso de análisis, desde otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete. La pausa publicitaria se deduce de las llamadas a los métodos trackAdStart y trackAdComplete.
   * La propiedad playhead ya no es necesaria al rastrear anuncios.
   * Compatibilidad Añadida con el ID de Visitante de Marketing Cloud.

* **Integración del SDK de Nielsen**

   * TVSDK ahora admite el envío de señalizaciones mTVR y MDPR ID3 al SDK de Nielsen sin ninguna integración personalizada. Para empezar, descargue el SDK 3.1.2.19 de la aplicación Nielsen iOS.

**Versión 1.4.0**

* **Señalización de interrupción con sustitución de contenido alternativo**

   * Como parte de la actualización 1.4 del TVSDK, el TVSDK ahora también admite entrar y volver de los apagones regionales contra contenido lineal. TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de interrupción incluso cuando se muestra una programación alternativa en lugar de la programación original.

* **Eliminar/Reemplazar publicidades C3**

   * Ahora, no se necesita ningún trabajo previo adicional para insertar dinámicamente nuevos anuncios en recursos de vídeo a petición (VOD) que salen de la ventana C3. TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar publicidades nuevas de forma dinámica. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se transmite durante la retransmisión y se baja inmediatamente para utilizarlo como contenido a petición sin tiempo suficiente para &quot;limpiar&quot; el recurso.

## Compatibilidad y certificación de dispositivos en 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>TVSDK **no admite** las siguientes funciones:
>
>* Movimiento lento, en cualquier plataforma o versión.
>* Juego de trucos en vivo.


**Versión 1.4.43**

* TVSDK 1.4.43 está certificado para iOS 11.

**Versión 1.4.29**

* TVSDK 1.4.29 ha sido certificado para iOS 10.

**Versión 1.4.28**

* TVSDK 1.4.28 ha sido certificado para iOS 10 Beta 7.
* Compatibilidad con DRM para forzar HTTPS agregando forceHTTPS y las API isForcingHTTPS.
* Se han actualizado las bibliotecas de VHL a 1.5.8, las bibliotecas de Adobe Mobile a 4.8.4 y la biblioteca de utilidades de registro al destinatario de implementación de la versión 7.0.

**Versión 1.4.19**

Esta versión del TVSDK ha sido certificada con la compatibilidad FairPlay para iOS y tvOS.

**Versión 1.4.17**

* tvOS

   Esta versión de TVSDK incluye compatibilidad con tvOS y ha sido certificada para flujos HLS no cifrados.

   **Nota**: Recuerde las siguientes directrices de compilación:

   * La compatibilidad con tvOs de TVSDK está limitada a flujos cifrados que no son de Adobe DRM. Debe eliminar la referencia a drmNativeInterface.framework en la configuración de la compilación de tvOS. Los flujos cifrados AES siguen siendo compatibles.
   * Apple requiere que todas las aplicaciones de Apple TV estén habilitadas para el código de bits, por lo que debe activar este indicador en los ajustes del proyecto.

## Problemas resueltos en 1.4 {#resolved-issues-in}

<!-- 

Comment Type: draft

<note type="note"> 
 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
</note>

 -->

<!-- 

Comment Type: draft

<note type="note"> 
 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
</note>

 -->

**Versión 1.4.45{#ios-tvsdk}**

* ticket n.º 36294 - iOS TVSDK no funciona con Xcode 10

   * Se han corregido los problemas de compilación con TVSDK en XCode 10. Debido a los requisitos de XCode 10, las aplicaciones compiladas en TVSDK para iOS 1.4.45 y posteriores requieren un destinatario de implementación mínimo como iOS 7.0

* ticket #36321 - Discrepancia observada en el rango buscable entre la instancia de PTMediaPlayer y AVPlayer en el estado &quot;Reproduciendo&quot;.
* Billete n.º 36493 - `libstdc++` compatibilidad con iOS 12

   * Se han corregido los problemas de compilación con TVSDK en iOS 12. Las aplicaciones creadas a partir de TVSDK para iOS 1.4.45 requieren un destinatario de implementación mínimo como iOS 7.0

**Versión 1.4.44**

* Boleto #34683 - El Tiempo De Progreso De La Reproducción De Anuncios Va En Negativo

   * Se implementaron comprobaciones adicionales para tratar el caso cuando hay una discrepancia entre la duración informada por el servidor de publicidad y el contenido publicitario real.

* El vale #34801 - currentTime y localTime no se actualizaban al buscar una nueva posición durante el estado pausado

   * La hora actual del reproductor se puede establecer en cero si el reproductor está en estado de pausa; antes, la hora actual se establecía en cero solo en estado de reproducción.

* ticket #35037 - La reproducción se detiene con una dirección URL incorrecta al volver de la inserción de anuncios basada en señales.

   * Se ha mejorado la corrección proporcionada para el problema cerrado Nº 34385 en la versión 1.4.42. Se Añadió el código de control de excepciones y comprobaciones isCanceled para que la cola de operaciones sea más sólida.

**Versión 1.4.43**

* (ZD#32990) - iOS: Reproducción de contenido en lugar de anuncios en algunos puntos de referencia. La API &#39;selectedMediaOptionInMediaSelectionGroup&#39;, que formaba parte de la interfaz AVPlayerItem, ahora se ha movido bajo AVMediaSelection en iOS 11. El problema se resolvió con esta nueva API.
* (ZD#33683) TVSDK eliminado == sufijo de las cadenas de metadatos. El problema se ha corregido en la lógica de análisis.
* (ZD#33905): TVSDK de iOS realiza llamadas a los archivos de manifiesto con dos agentes de usuario. El problema del agente de usuario se ha solucionado en la primera llamada a m3u8 (caso de instalación nueva). Los M3u8 tienen los mismos agentes de usuario para todas las llamadas ahora.
* (ZD#34293): Los pre-rolls insertados en flujos LINEAR no se reproducen correctamente en iOS11. El problema se ha solucionado para los anuncios de preventa.
* (ZD#34684): cuando se aplica la directiva de omisiones de publicidad, los fotogramas de anuncios previos se muestran durante unos segundos. Se ha introducido una nueva API, enableVodPreroll, para desactivar la reproducción previa en la reproducción del vídeo. El valor predeterminado de esta API es &#39;Sí&#39;. La API garantiza que se omita la vinculación del contenido de la publicidad en el contenido principal.
* (ZD#34765) - Después de llamar a stop(), algunos segmentos de flujos de transporte todavía se descargan. Se ha mejorado la API Stop() para evitar la descarga de segmentos adicionales.
* (ZD#34865): los anuncios preliminares para la transmisión en directo se truncan en iOS. Relacionado con iOS11, y la adición de una verificación adicional para confirmar si el flujo es previo o de contenido principal, resuelve este problema.
* (ZD#35093): se corrigió un escenario de conmutación por error en el que, si falla la variante principal del flujo al inicio (devuelve 404), la reproducción no cambia al flujo de copia de seguridad.

**Versión 1.4.42 (1.4.42.118)**

* (ZD#34385): la reproducción se bloquea con una URL incorrecta al volver de la inserción de anuncios basada en señales.

   Aumente los recuentos simultáneos máximos de CustomAVAsetLoaderOperations, de modo que las lecturas de manifiesto puedan continuar ejecutándose.
* (ZD#34373): los usuarios finales no pueden realizar la secuencia a dispositivos conectados HDMI cuando la grabación de flujo no está permitida.
* (ZD#32678): TVSDK no recopila los ID de publicidad correctos en iOS.

   El ID de anuncio del elemento creativo de anuncio final ahora se recoge en pings de VHL en caso de redireccionamientos de VAST/VMAP.
* (ZD#33904): TVSDK no está registrado para las notificaciones AVFFoundation AVAudioSessionMediaServicesWasLostNotification y AVAudioSessionMediaServicesWasResetNotification.

   PTMediaServicesWasLostNotification y PTMediaServicesWasResetNotification ahora se pueden registrar en la aplicación del reproductor para obtener las notificaciones cuando se restablecen o pierden los servicios de medios.

* (ZD#33815): los clientes no pueden actualizar sus reglas de CRS de normalización y priorización sin necesidad de actualizar la aplicación.

   Se han Añadido las API getCRSRulesJsonURL y setCRSRulesJsonURL en iOS TVSDK.

**Versión 1.4.41 (1.4.41.76)**

* (ZD #34464) - Publicación de aplicaciones de referencia con TVSDK versión 1.4.41

   A partir de esta versión, Xcode 9 es necesario para compilar TVSDK para iOS.
* (ZD #29456) - Inicios de aerolíneas en estado de pausa

   Se ha corregido el problema de pausa que se producía cuando el vídeo se pausaba al entrar en reproducción aérea.
* (ZD #30371) - Cambios en el tiempo de inicio de AdBreak cuando insertamos más de 2 anuncios en flujo lineal

   Se ha corregido el error al intentar reproducir contenido en Apple TV, que impedía la reproducción completa
* (ZD #32146)- No se recibe PTMediaPlayerStatusError en el contenido de HLS Live al bloquear iOS 11 dev beta

   No se recibe PTMediaPlayerStatusError para contenido en directo y VOD de HLS al bloquear mediante Charles (conexión de eliminación y 403)
* (ZD #29242) - La reproducción de vídeo de reproducción de Airplay falla con las publicidades activadas

   Cuando los anuncios están activados y AirPlay está habilitado al iniciar la reproducción de un vídeo, la reproducción de vídeo nunca inicio y no se muestra ningún error
* (ZD#33341) - DRMInterface.h activa las advertencias de compilación en Xcode 9

   Se corrigieron dos prototipos de bloques en DRMInterface.h que no tenían la palabra &#39;void&#39; en sus listas de parámetros
* (ZD#31979): no se compila/ejecuta cuando es iOS 10 o posterior para iPhone 7/iPhone7+

   Se corrigió la compilación de documentos IB para versiones anteriores a iOS 7 que ya no se admite
* (ZD#32920): pantalla en blanco dentro de una pausa publicitaria y sin finalización de pausa publicitaria

   Cuando un salto de publicidad está presentando instancias de publicidad y una vez finalizada una instancia de publicidad, se muestra una pantalla en blanco
* (ZD#32509) - Deshabilitar grabación de pantalla en iOS 11 Deshabilitar grabación de pantalla en iOS 11

* (ZD#33179): error intermitente de evento en iOS11

   Se ha corregido el error de evento en iOS 11

**Versión 1.4.40** (1.4.40.72)

* (ZD #32465): el reproductor no puede gestionar listas de reproducción combinadas.

   Call FinishLoadingWithError(con: Error) para que la base de AV pruebe flujos alternativos/failover de activadores.

* (ZD #31951) - Error de TVSDK durante las rotaciones de licencia.

   Se corrigió el problema de rotación de licencia.
* (ZD #31951) - Pantalla en blanco dentro de una pausa publicitaria y sin finalización de pausa publicitaria.

   Se ha corregido un problema por el cual las publicidades VPAID de Facebook solían devolver varios bloques CDATA en un solo \&amp;lt;AdParameters\&amp;gt; Nodo VAST.
* (ZD #33336) - [iOS] TVSDK - Los pods de publicidad no se rellenan, a pesar de que FreeWheel devuelve suficientes anuncios.

   Se ha creado una relación principal-secundaria entre la publicidad de secuencia y la de reserva y una clasificación basada en la secuencia principal y el índice.

**Versión 1.4.39** (1.4.39.43)

* (ZD #32178): la versión de iOS TVSDK es incorrecta.

   El resultado de la versión de TVSDK en los archivos de registro era 1.0.211. Se corrige la salida de la versión correcta.

* (ZD #32199) - Carga de publicidad diferida - El vídeo no se muestra para el contenido.

   La línea de tiempo de Adbreak local que no se inicializaba anteriormente, ahora se actualiza antes del uso.

* (ZD #27528): el vídeo, el audio o ambos se bloquean de 1 a 45 segundos después de que se reproduzca un inicio de recursos, si el audio secundario se establece de forma no predeterminada en iOS 1.2.

   Prepare e informe las pistas de audio en estado Listo.

* (ZD #30411) - Puede obtener resultados inesperados, como audio sin audio o audio incorrecto, si elige un idioma Sap secundario.

   Prepare e informe las pistas de audio en estado Listo.

* (ZD #32199) - Carga de publicidad diferida - El vídeo no se muestra para el contenido.

   La línea de tiempo de Adbreak local que no se inicializaba anteriormente, ahora se actualiza antes del uso.

* (ZD #27528): el vídeo, el audio o ambos se bloquean de 1 a 45 segundos después de que se reproduzca un inicio de recursos, si el audio secundario se establece de forma no predeterminada en iOS 1.2.

   Prepare e informe las pistas de audio en estado Listo.

* (ZD #30411) - Puede obtener resultados inesperados, como audio sin audio o audio incorrecto, si elige un idioma Sap secundario.

   Prepare e informe las pistas de audio en estado Listo.

**Versión 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Añadir AdSystem e ID creativos a solicitudes de CRS

Uso de ID creativos y AdSystem en solicitudes CRS basadas en reglas de normalización CRS

* (ZD #29176) - Bloqueo en PTAdPolicyDeligate satAdBreakAsWatched:position

Ahora se controla el bloqueo debido a AdBreak vacío.

* (ZD #30125): Los anuncios programáticos no funcionan en la plataforma iOS

Compatibilidad Añadida con anuncios programáticos en iOS.

* (ZD #30782) - #EXT-X-PROGRAMA-Notificación de FECHA-HORA

El evento de metadatos temporizados no se activa para la etiqueta # EXT-X-PROGRAMA-DATE-TIME con flujos DRM en vivo.

**Versión 1.4.37 (1.4.37.842)**

* (ZD #28950) - Problema de reproducción de VOD

Problema de reproducción cuando la etiqueta # EXT-X-PLAYLIST-TYPE del flujo se establece en Evento en lugar de en VOD

* (ZD #29281) - iOS: Añadir AdSystem e ID creativos a solicitudes de CRS

Uso de ID creativos y AdSystem en solicitudes CRS basadas en reglas de normalización CRS.

* (ZD #29462) - La publicidad de TremorHub en A&amp;E VOD provoca un bloqueo en las aplicaciones de iOS

**Versión 1.4.36 (1.4.36.835)**

* (ZD #29418): Las señales con la duración 0 (#EXT-X-CUE-OUT:0.000) están provocando que TVSDK de iOS detenga o bloquee la reproducción.

El problema se ha solucionado y la reproducción inicio correctamente.

* (ZD #29462) - Anuncio en VOD que provoca un bloqueo en iOS TVSDK .

El problema se ha solucionado. iOS TVSDK está generando una excepción (AUDNetworkAdInfo::initWithAdId) y no la está controlando. La excepción se debe a un ID de publicidad vacío.

* (ZD #29281)- Añada AdSystem y el ID creativo a las solicitudes de CRS.

Incluya AdSystem y CreativeId como nuevos parámetros en las solicitudes 1401 y 1403 (todos los demás parámetros siguen siendo los mismos).

**Versión 1.4.35** (1.4.35.830)

* (ZD #27830): Es necesario determinar mediante programación la diferencia entre subtítulos y subtítulos en iOS.

TVSDK ahora expone los dos tipos que pueden utilizarse para filtrar el tipo de rótulo requerido.

* (ZD #29160): las indicaciones de anuncios EXT-X-CUE-OUT no se duplican correctamente en TVSDK iOS.

Con el anuncio del midroll EXT-X-CUE-OUT se está reproduciendo ahora.

* (ZD #29100): la aplicación se bloquea cuando el usuario se desplaza hasta el final de una película.

Se corrigieron varios bloqueos relacionados con la sincronización.

* (ZD #28785), (ZD #27712) y (ZD #25076) - La aplicación de iOS se bloquea durante los grandes eventos en directo.

Se corrigieron varios bloqueos relacionados con la sincronización.

**Versión 1.4.34** (1.4.34.815 para iOS 6.0+)

* (ZD# 28481) - Interrupción de las tarifas debido a que la clave incorrecta se anexa al final de una pausa publicitaria para esos flujos FER

Para un flujo FER, la clave antes de la pausa publicitaria se inserta después del final de la pausa publicitaria. Este problema se resolvió agregando la *última clave* vista al final de la pausa publicitaria.

**Versión 1.4.33** (1.4.33.803 para iOS 6.0+)

* (ZD# 21701) Habilitar CRS para subcuentas

Habilitado mediante el envío de la dirección URL creativa original para la solicitud de CRS 1401 en lugar de la dirección URL normalizada, según el requisito de CRS back-end.

* (ZD# 26218) - Problema de carga de PSDKResources.bundle

Este problema se resolvió actualizando la carga de recursos para que se vieran desde todos los paquetes disponibles.

* (ZD# 27460) Primera llamada de anuncio de mitad de carrera: POST a cdn.auditude<span></span>.com que devuelve 403.

La nueva cuenta de CDN no puede gestionar una solicitud de CDN POST. Este problema se resolvió actualizando el código para que la solicitud de `cdn.auditude.com` publicidad sea GET en lugar de POST.

**Versión 1.4.32** (1.4.32.792 para iOS 6.0+)

* (ZD# 27132) Compatibilidad con valores decimales para saltos de publicidad VMAP.

Cuando el contenido no se segmentaba a lo largo de los saltos de publicidad definidos, los enteros provocaban colocaciones de anuncios inesperadas. El problema se resolvió al no convertir los valores decimales en enteros.

* (ZD# 27189) El contenido AES con la etiqueta EXT-X-DISCONTINUITY-SEQUENCE no se reproduce correctamente.

El problema se resolvió colocando la etiqueta al principio de la lista de reproducción.

**Versión 1.4.31** (1.4.31.785 para iOS 6.0+)

* (ZD# 24528) Implementar métricas de uso de TVSDK para la facturación

Para obtener más información, consulte Métricas [de facturación](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md).

* (ZD# 24642) Compatibilidad con imágenes en imágenes para TVSDK

La función de imagen en imagen, que en algunos casos no funcionaba correctamente, se ha corregido.

* (ZD# 25246) Señales de pausa publicitaria incorrectas

Este problema se resolvió alineando las etiquetas de discontinuidad entre los manifiestos de variante.

* (ZD# 26218) El proceso de compilación de aplicaciones se complica al intentar incluir PSDKLibrary.framework en el marco de aplicaciones del cliente

Este problema se resolvió empaquetando el archivo PSDKLibrary.framework como se solicitó.

* (ZD# 26364) Compatibilidad con múltiples CDN para anuncios CRS
<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028) Retraso en la reproducción de algunos flujos en iOS 10.

Este problema se resolvió proporcionando una solución alternativa para los flujos que no tienen la extensión M3U8.

**Versión 1.4.30** (1.4.30.754 para iOS 6.0+)

En esta versión se han solucionado los siguientes problemas de TVSDK:

* (ZD# 24180) Añada un encabezado personalizado para permitir la lista

Se ha agregado un nuevo encabezado personalizado a la lista de permitidos de TVSDK.

* (ZD# 25016) El flujo de conmutación por error se selecciona de forma aleatoria cuando se establecen los parámetros de control de ABR

Este problema se resolvió manteniendo los flujos ABR en orden cuando la configuración ABR se proporciona con la configuración initialBitrate en un flujo que incluye direcciones URL de conmutación por error. Esto evitará reproducir los flujos de conmutación por error en lugar de los principales.

* (ZD# 25076) Bloqueo en PTAuditudeAdResolver loadComplete

Se ha solucionado el problema por el que se producía un bloqueo durante el rápido inicio/parada de varias instancias de PTMediaPlayer con anuncios.

* (ZD# 25960) No hay etiquetas suscritas adicionales que activen las retransmisiones de notificaciones de cambio de metadatos

Se ha solucionado el problema por el que no se notifica a una etiqueta suscrita cuando aparece antes de que se corrija el primer segmento del manifiesto.

* (ZD# 26084) PSDK lanzando un 106000.101000.Error de decodificador -11833 al realizar la transición de la última pausa publicitaria a contenido de entretenimiento

Cuando el tiempo de inicio de la última pausa publicitaria del VMAP cae antes de que se complete la duración total, en determinadas condiciones, la clave no se inserta hasta después del final de la última pausa publicitaria. Este problema se ha solucionado.

* Video Heartbeat Library (VHL) se ha actualizado a la versión 1.5.9 para resolver los siguientes problemas:

   * (ZD #22351) VHL - Analytics: Duración de recursos de vídeo en directo

Este problema se resolvió agregando la API assetDuration a `PTVideoAnalyticsTrackingMetadata` para actualizar la duración del recurso para flujos interactivos/lineales y proporcionar una lógica para comprobar el flujo en directo.

* (ZD# 22675) VHL - Analytics: Actualización de la duración de los recursos de vídeo en directo

Este problema es el mismo que ZD #22351.

* (ZD #25908) VHL - Analytics: Adobe Heartbeat Evento Crash

Este problema se resolvió actualizando la implementación para utilizar la última versión de VHL para iOS versión 1.5.9 con el fin de mejorar la estabilidad y el rendimiento.

* (ZD #25956) VHL - Analytics: Bloquear al reproducir vídeos repetidamente

Este problema es el mismo que ZD #25908.

**Versión 1.4.29** (1.4.29.743)

* (ZD# 23901) Los anuncios de terceros no se reproducen

Este problema se resolvió moviéndose a la estructura URL de CRS v3 para incluir el ID de zona en la URL reempaquetada.

* (ZD #25183) Problemas con la reproducción de DRM en tvOS e iOS

Este problema se resolvió proporcionando compatibilidad con varias etiquetas clave necesarias para la compatibilidad con varios DRM.

* (ZD# 25334) TVSDK no puede reproducir un contenido compartido cDVR

Este problema se resolvió impidiendo que TVSDK convirtiera cadenas vacías en direcciones URL absolutas.

* (ZD# 25347) Configure el encabezado HTTP personalizado en AVURLAsset

Se ha añadido la compatibilidad con encabezados personalizados en las solicitudes de segmentos a través de la clase PTNetworkConfiguration.

**Versión 1.4.28** (1.4.28.722)

* (ZD #24549) Varias llamadas de seguimiento de anuncios

Este problema se resolvió actualizando el administrador de la línea de tiempo para detectar notificaciones en un objeto específico cuando se crearon varios reproductores.

* (ZD #24758) PTManifestLogger no es compatible con iOS 8

Este problema se resolvió actualizando la biblioteca de utilidades del registrador al destinatario de implementación de la versión 7.0.

* (ZD #24775) Flujo retrasado debido a anuncios

Este problema se resolvió calculando correctamente la deriva de duración en las listas de reproducción de evento.

* (ZD #24799) Algunos de los episodios no se reproducen en la aplicación iOS

Este problema se resolvió usando el servidor web local para subtítulos cuando los archivos WebVTT están georestringidos.

**Versión 1.4.27** (1.4.27.711) para iOS 6.0+

* (ZD #24089) - Optimizaciones para la resolución de anuncios en flujos DVR largos

Este problema se resolvió añadiendo varias optimizaciones para reducir el tiempo necesario para procesar la ventana DVR en flujos en directo/lineales.

* (ZD #21554) - Las señalizaciones de error de TVSDK no se activan para el tipo de aplicación = vídeo/mp4

Este problema se resolvió habilitando el reproductor para hacer ping a las direcciones URL de seguimiento de errores correctas en formatos de recurso no válidos.

* (ZD #24424) - El bloqueo de tipo EXC_BAD_ACCESS KERN_INVALID_ADDRESS se origina desde PSDKLib para iOS en dispositivos de hardware más recientes.

Se ha corregido el bloqueo que se producía debido a una instancia de reproductor de medios desasignada, cuando la reproducción se cambia rápidamente entre diferentes flujos.

* (ZD #24575): bloqueo en TVSDK en dispositivos de 32 bits cuando enableDebugLog=true

Se ha solucionado el problema en el formato de registro que causaba el bloqueo en dispositivos de 32 bits al habilitar el registro.

**Versión 1.4.26** (1.4.26.702) para iOS 6.0+

* (ZD# 20213): El FW TVSDK debe ser dinámico/modularizado para XCode7

   * Se corrigió al actualizar las bibliotecas con compatibilidad con módulos

**Versión 1.4.25** (1.4.25.684) para iOS 6.0+

* (ZD #19629) - Pausas de vídeo en directo al entrar en el retransmisión a ATV 4

Este problema se resolvió agregando un período de espera después de eliminar elementos antiguos pero antes de agregar elementos nuevos a AVQueuePlayer. Sin el período de espera, las notificaciones se envían al elemento incorrecto.

* (ZD #19856): no se muestran subtítulos cuando están activados de forma predeterminada

Se han solucionado los problemas de la lista de reproducción de webvtt, que provocaban que los subtítulos no se mostraran correctamente.

* (ZD #21590) - Rendimiento y seguimiento de vídeo en los últimos Orígenes

Se ha solucionado el problema de la longitud de vídeo que falta en VideoAnalytics.

* (ZD #20202): la configuración del estilo de los subtítulos personalizados bloquea la aplicación de iOS

Este problema se resolvió añadiendo comprobaciones de objeto nulo adicionales al definir los estilos de subtítulo.

* (ZD #20709): duración del vídeo registrada como 0 en el seguimiento de inicios de vídeo

Este problema es el mismo que (ZD #21590).

* (ZD #22280) - Duración del vídeo de Analytics definida en 0

Este problema es el mismo que (ZD #21590).

* (ZD #22592) - Problemas con el juego aéreo en Primetime

Este problema es el mismo que (ZD #19629).

* (ZD#22922): conmutación de velocidad de bits manual para iOS

Este problema se resolvió proporcionando una opción para especificar la velocidad de bits máxima.

* (ZD #23084) - Cumplimiento de Apple para redes solo IPv6

Se han eliminado los símbolos que Apple no recomendaba para la compatibilidad con IPv6.

**Versión 1.4.24** (1.4.24.661) para iOS 6.0+

* ZD #2548) - Compatibilidad de Primetime con publicidad interactiva en dispositivos móviles - VPAID 2.0

Este problema se resolvió actualizando la lógica para mostrar la vista del reproductor si un anuncio de VPAID no se puede reproducir.

* (ZD #20101): la implementación de capítulo personalizado activa el evento de inicio de capítulo durante la reproducción del anuncio

Este problema se resolvió actualizando VideoAnalyticsTracker para detectar correctamente el inicio/finalización de capítulos al realizar la transición entre los límites de capítulos y no capítulos.

* (ZD #20784) - Analytics: Se completa el contenido de activación para transiciones de vídeo en directo

Este problema se resolvió agregando una lógica para activar manualmente la finalización de contenido durante una sesión de seguimiento de vídeo.

Se han actualizado las bibliotecas siguientes:

* Biblioteca de AdobeMobile a 4.10.0
* Biblioteca VHL a 1.5.6
* Biblioteca VHL-Nielsen a 1.6.7
* (ZD #21855) - Los subtítulos no se reproducen después de la mitad del ciclo

En este problema, las etiquetas de discontinuidad del duplicado provocaban que los subtítulos no aparecieran después de la mitad del desplazamiento. Este problema se resolvió eliminando las etiquetas de discontinuidad que están al lado unas de otras.

* (ZD #21994) - Cadena fuera de límite en PTHLSUtils

La causa más probable del bloqueo es cuando EXT-X-KEY tiene una dirección URL rodeada de comillas.

* ZD #22074) - El bloqueo de AUDVAST ocurre una vez por minuto en iOS

En la versión 1.4.23, se corrigió el bloqueo causado por la presencia de caracteres no seguros en una URL de redireccionamiento VAST. Sin embargo, TVSDK seguía omitiendo estas publicidades.

Este problema se resolvió administrando los caracteres no seguros y permitiendo que se reprodujeran los anuncios.

* (ZD #22694) - PTMediaPlayer.  El reproductor oculta la Vista

Este problema se resolvió actualizando la lógica para mostrar la vista del reproductor si un anuncio de VPAID no se puede reproducir.

**Versión 1.4.23** (1.4.23.641) para iOS 6.0+

* (ZD #18016) - Sin respuesta del SDK de Primetime con una condición de red incorrecta

Este problema se resolvió mejorando la notificación de errores cuando se producía un error fatal de AVFFoundation y permitiendo que la aplicación gestionara el reinicio después del error.

* (ZD #20580) - Bloqueo en PTSplicerManager

Este problema se resolvió proporcionando protección adicional frente a los problemas de concurrencia que causan el bloqueo.

* (ZD #21782) - Código de error de iOS 10100

Se ha solucionado el problema por el que el TVSDK devolvía un error 101000 al iniciar la reproducción en flujos DRM de Adobe Access.

* (ZD #21889): Falla la reproducción de anuncios en línea y contenido sin conexión

Se ha solucionado el problema por el que la reproducción fallaba después de que se corrigiera un anuncio en contenido sin conexión cifrado AES.

* (ZD #22074) - El bloqueo de AUDVAST se produce una vez al minuto en iOS

Este problema se resolvió mejorando el manejo de las etiquetas de publicidad VAST de terceros que tienen caracteres no válidos en la dirección URL.

* (ZD #22257) - El TVSDK no puede reproducir el flujo DRM

Se ha solucionado el problema del TVSDK que devolvía un error 101000 al iniciar la reproducción en flujos DRM de Adobe Access.

**Versión 1.4.22** (1.4.22.627) para iOS 6.0+

* (ZD #18709) - Bloqueo en TVSDK para iOS

Se ha solucionado el problema de un bloqueo que se producía en algunos flujos protegidos con DRM de Adobe Access.

* (ZD #18850) - Actualice la lógica de selección creativa basada en las reglas de CRS

Este problema se resolvió agregando un archivo de configuración .json para especificar la prioridad de selección creativa.

* (ZD #19770) - La fuente de vídeo AES protegida ya no se reproduce

Se ha solucionado el problema de ciertos flujos redirigidos 302 que no se reproducían.

* (ZD #19629) - Pausas de vídeo en directo al entrar en el retransmisión a ATV 4

Este problema se resolvió añadiendo una solución alternativa para la pausa de vídeo en directo cuando se activa la retransmisión para dispositivos Apple TV 4. El número parece ser AppleTV 4.

* (ZD #21119) - El TVSDK se detiene tras la reproducción del anuncio

Se ha añadido compatibilidad para flujos cifrados AES con una secuencia IV mientras se utiliza la inserción de anuncios.

* (ZD #21125) - Retorno de la pausa publicitaria en directo/lineal temprano

Se ha agregado compatibilidad para volver de una pausa publicitaria antes de que se reproduzca la pausa publicitaria hasta la finalización. La devolución anticipada se indica mediante una etiqueta de manifiesto personalizada.

* (ZD #21224) - Soporte de aerolíneas para transmisiones de flujo simulado desde Akamai

Se han agregado API a la clase PTNetworkConfiguration para anexar cookies como parámetros de URL en segmentos para determinados flujos con tokens de Akamai.

* (ZD #21287) - Registro externo

Se ha corregido un problema con algunas sentencias de registro que se mostraban de forma predeterminada en la consola xcode, incluso cuando el registro estaba deshabilitado.

* (ZD #21446) - eventos de pausa de publicidad a veces no activados por el TVSDK

En los flujos de EVENTO, los saltos de publicidad no se activan correctamente en la versión anterior. Esta compilación aborda este problema.

**1.4.21** (1.4.21.605) para iOS 6.0+

* (ZD #20749) - Fallback omite las respuestas VAST no vacías; Se activan las direcciones URL de seguimiento de anuncios adicionales

Se ha solucionado un problema con los pings de duplicados en las publicidades de reserva.

**1.4.20** (1.4.20.590) para iOS 6.0+

* (ZD #18639): El TVSDK utiliza recursos/CPU excesivos en un recurso de grabación en caliente de larga duración

El uso excesivo de CPU/recursos se ha corregido en los dos niveles. Primero, permitiendo que la función de actualización de tiempo se ejecute en una cola global, en lugar del subproceso principal, y optimizando el uso de CPU para analizar el manifiesto con m3u8 previamente procesado y en caché.

* (ZD #19349): los anuncios preliminares se omiten al limitar la conexión de red.

Este problema se resolvió proporcionando un evento de tiempo de espera (requestTimeout) a la aplicación y a adMetadata.  adRequestTimeout API para anular el tiempo de espera predeterminado de 10 segundos.

* (ZD #19446) - Falta notificación en flujos en directo

Este problema se resolvió permitiendo que la aplicación se suscribiera a EXT-X-PROGRAMA-DATE-TIME en flujos en vivo.

* (ZD #19459): bloqueo al preparar audio alternativo con PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Bloqueo - [PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]

Este problema es el mismo que Zendesk #19459.

* (ZD #19574) - El TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM

En la carga inicial del archivo de manifiesto en PTMediaPlayerItem.prepareToPlay, si se produce un error al cargar el manifiesto, TVSDK no informa del cuerpo de la respuesta de error a la aplicación.

Este problema se resolvió permitiendo que el TVSDK informara de la respuesta de error como un error en la aplicación.

* (ZD #19615) - La lógica de reserva no funciona

En la implementación actual, las publicidades de reserva se omitían y no se reempaquetaban a menos que estas publicidades estuvieran en formato m3u8. Este problema se resolvió agregando también la compatibilidad para volver a empaquetar publicidades de reserva.

* (ZD #19770) - El TVSDK no puede reproducir contenido AES protegido con redirección 302

Se ha solucionado el problema de redireccionamiento, ya que la dirección URL de redireccionamiento se eliminaba con cleanConnectionData antes de que se pudiera usar para analizar el manifiesto.

* (ZD #19856): los subtítulos no se muestran para algunas velocidades de bits cuando están activados de forma predeterminada

Este problema se resolvió gestionando el error de iOS para los segmentos de los flujos en los que no se muestran los subtítulos.

* (ZD #19868): El TVSDK se bloquea cuando se transmite un elemento creativo no válido

Se ha solucionado el bloqueo del TVSDK que se producía al deslocalizar incorrectamente una instancia del gran analizador.

* (ZD #20180) - Las publicidades VPAID se omiten ocasionalmente

El tipo MIME de JavaScript no siempre se incluía ni se consideraba como un tipo de MIME válido. Este problema se resolvió incluyendo JavaScript como un tipo de MIME válido.

* (ZD #20749) - Fallback omite las respuestas VAST no vacías; Se activan las direcciones URL de seguimiento de anuncios adicionales

Se ha solucionado el problema de algunos elementos creativos que no se están reempaquetando.

**Versión 1.4.19** (1.4.19.563) para iOS 6.0+

* ZD #18639) - El TVSDK utiliza recursos/CPU excesivos en un recurso de grabación en caliente de larga duración

Este problema se resolvió optimizando la reescritura de la lista de reproducción DRM m3u8 en bits de caché de la lista de reproducción que se habían reescrito anteriormente. Esto es más relevante cuando reproduce flujos m3u8 activos para los que se descarga m3u8 después de cada descarga de segmento.

* (ZD#18956) - player.drmManager es nil cuando el punto de interrupción se establece en iOS Demo Player

Este problema se resolvió actualizando la implementación de la API de PTMediaPlayer.drmManager para recoger DRMManager del marco de DRM.

**Versión 1.4.18** ( 1.4.18.557) para iOS 6.0+

* (ZD #18844) Seguimiento del cursor de reproducción para contenido activo en el reproductor de iOS.

Este problema se resolvió permitiendo que las aplicaciones establecieran su propio valor de cursor de reproducción.

* Zendesk #18518 - Si no se especifica el nombre del vídeo, el nombre del TVSDK se establece de forma predeterminada en el reproductor basado en *PSDK.*

Este problema se resolvió eliminando el valor predeterminado del nombre del reproductor.

**Versión 1.4.17** (1.4.17.545) para iOS 6.0+

* Zendesk #2228 - Mejore el TVSDK para devolver la respuesta JSON de la captura de un manifiesto

En lugar de enviar un error cuando el contenido no es M3U8, DRM Framework devuelve un valor nulo de DRMMetadata. El problema se resolvió agregando metadatos para exponer el contenido cuando se produce la notificación M3U8_PARSER_ERROR.

* Zendesk #2231 - Error al recuperar el manifiesto no disponible en MediaPlayerNotification

La misma resolución que Zendesk #2228

* No se rellena la macro de Zendesk #3304 - VAST 3.0 `[ERRORCODE]`

Se ha solucionado el problema por el que el SDK de Auditude no podía enviar un ping cuando la URL de seguimiento tenía espacios al principio.

* Zendesk #17294 - Bloqueo SecKeyRawSign

Se ha solucionado un posible bloqueo cuando el código del cliente utiliza la cadena de claves.

* Zendesk #18008 - Cookies compatibles con iOS8+ para admitir flujos con token

Los flujos con token de Akamai requieren que las cookies se envíen en solicitudes de segmento, lo cual no era posible en iOS 7 ni en versiones anteriores. A partir de iOS 8, Apple ha agregado una API que permite que las cookies se pasen para las solicitudes de segmentos. Esta compatibilidad ya está disponible en el SDK de TVSDK . También se ha agregado compatibilidad para enviar un usuario-agente, si está disponible.

* Zendesk #18166 - TVSDK 1.4.15 emite cientos de advertencias al compilar con DWARF con opciones de archivo dSYM

Se han resuelto todas las advertencias.

**Nota**: se han añadido bibliotecas compatibles con tvOS para TVSDK.

**Versión 1.4.16** (1.4.16.1454)

* Zendesk #3875 - La ficha S se bloquea durante la reproducción

Revertir la dependencia de OKHTTP en la audiencia para CRS porque TVSDK ahora está utilizando directamente httpurlconnection en lugar de curl. El problema se resolvió borrando las excepciones antes de realizar otra llamada de JNI.

* Zendesk #4487 - Seguimiento del Canal lineal del contenido

El problema se resolvió volviendo a inicializar el rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* Zendesk #17919 - Android: la búsqueda de contenido causa un error de latido

El problema era resolver el latido en un estado de error cuando hay una búsqueda en un capítulo

* Zendesk #18053 - Aplicación que utiliza el TVSDK se bloquea en el malvavisco

El TVSDK se bloqueaba en el sistema operativo Android M cuando la biblioteca TVSDK utiliza código neon que realiza la conversión de color YUV -> RGB. Este problema se resolvió actualizando las funciones que causan este problema mediante la utilización de una versión de código no neón.

* Zendesk #18072 - Android M - Bloqueo de aplicaciones

Este bloqueo se produce al llamar a las API de MediaCodecList y MediaCodecInfo al comprobar si el perfil y el nivel son compatibles. Adobe está buscando la asistencia técnica de Google para obtener información adicional. Este problema se resolvió proporcionando un trabajo temporal cargando toda la información del códec con antelación para evitar llamar a estas API solo cuando se necesita información del códec.

* Zendesk #18074 - Subtítulos en árabe que no funcionan en Nexus con Android 6.0

Este problema se resolvió proporcionando compatibilidad con el mapa de fuentes CTS de Android.

**Versión 1.4.15** (1.4.15.512) para iOS 6.0+

**Nota**: El módulo Nielsen se ha eliminado de la compilación de TVSDK, pero el TVSDK se actualizará en un futuro próximo con un nuevo módulo de integración de Nielsen.

* (ZD #2228): error al recuperar el manifiesto no disponible en MediaPlayerNotification

Metadatos Añadidos para exponer el contenido cuando se produce la notificación M3U8_PARSER_ERROR.

* (ZD #4437): errores dentro del SDK de Adobe Primetime

Se corrigió un bloqueo informado al preparar subtítulos o audio alternativo.

* (ZD #4487) - Seguimiento del Canal lineal del contenido

Se permite la reinicialización del rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

**Versión 1.4.14** (1.4.14.498) para iOS 6.0+

* (ZD #17260) - Bloqueo en playlistManagerForURL

Se corrigió un bloqueo intermitente debido a problemas de concurrencia.

**Versión 1.4.13** (iOS 6.0+)

* (ZD #3304): no se rellena la macro VAST 3.0 `[ERRORCODE]`

   * El código de error 400 se mostrará si la publicidad en línea tiene un elemento creativo incorrecto.
   * `[ERRORCODE]` la macro estará codificada en la dirección URL.

* (ZD #3865) Integración de Heartbeat con anuncios de IMA

Se corrigió un error en el cual la duración del vídeo se informaba incorrectamente.

* Se ha actualizado el reproductor de demostración TVSDK para que admita iOS 9

Para admitir correctamente iOS 9, debe configurar las excepciones de Application Transportation Security. A los efectos de la demostración, el ATS está completamente desactivado.

**Versión 1.4.12** (1.4.12.464) para iOS 6.0+

* (ZD #4521) CRS Prueba de cliente y SSAI

Se corrigió el MD5 inverso incorrecto en la URL 3P.

**Versión 1.4.12** (1.4.12.463) para iOS 6.0+

* (ZD #2751) CSAI y CRS | Mejorar: Gestionar elementos dinámicos en determinadas direcciones URL de archivos multimedia.

Se ha actualizado el servicio de reempaquetado creativo para gestionar correctamente las publicidades con direcciones URL creativas dinámicas.

* (ZD #3654) Pérdida de memoria en la versión PSDK después de 1.3.4.166

Se corrigió la pérdida de memoria en drmFramework con la reproducción regular en dispositivos iOS 8.2

* (ZD #3988) El predesplazamiento se omite al volver a buscarlo después de la primera reproducción

Se ha corregido un error para que las directivas de publicidad se pudieran deshabilitar correctamente.

* (ZD #4017) Solicitud de la API de iOS para forzar la reproducción del anuncio en la búsqueda hacia atrás

Resuelto con corrección para ZD #4279

* (ZD #4279) Inserción de anuncios HLS TVSDK -302 problema de redireccionamiento en iOS y escritorio

Se corrigió un error cuando un recurso de publicidad utilizaba una dirección URL de redirección relativa

**Versión 1.4.9** (1.4.9.427) para iOS 6.0+

* (ZD #3075) Problema de accesibilidad de Internet - iOS

Notificación Añadida para detectar si la reproducción se ha detenido.

* (ZD #3193) Solicitud de una API de cambio de Perfil en TVSDK

Se ha actualizado PTPlaybackInformation para exponer la información de la velocidad de bits indicada actualizada. Se ha actualizado la notificación BITRATE_CHANGE para que sea más confiable en el tiempo y precisa con respecto a las velocidades de bits notificadas por M3U8.

* (ZD #3324) Problema de sistema de informes de anuncios de Primetime cuando no hay medios publicitarios en VMAP

Compatibilidad con el ping de direcciones URL de seguimiento de errores de publicidad vacías, TVSDK ahora verificará el inicio de la pausa publicitaria y completará los pings para pausas publicitarias vacías

**Versión 1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7 se bloquea en reproducciones de Evento completo

**Versión 1.4.7** (1.4.7.382)

* (ZD #2197) Seguimiento de errores de publicidad. La notificación Añadida para el recurso no pudo cargar el manifiesto.
* (ZD #2894) Player Realiza 4 solicitudes de manifiesto de nivel superior durante la reproducción.
* (ZD #2992) Duraciones e identificadores extraños del Sistema de informes de la audiencia.

**Versión 1.4.6**(1.4.6.325)

* (ZD #2197) Seguimiento de errores de publicidad. La notificación Añadida para el recurso no pudo cargar el manifiesto

**Versión 1.4.5** (1.4.5.283)

* (ZD #2141) Implementación de Analytics para la aplicación TreeHouse, se agregó la biblioteca AdobeAnalyticsPlugin.a para crear el paquete .
* Actualización de la biblioteca de Video Heartbeat a 1.4.1.2
* [PTPALY-4226] [relacionada con ZD #2423) La restauración de DRM puede resultar en la eliminación de datos de Documento de aplicaciones.

**Versión 1.4.4** (1.4.4.242)

* Video Heartbeat Library (VHL) se actualiza a la versión 1.4.1.

* (ZD #2435) Documentación del SDK de TV sobre las actualizaciones de las necesidades de análisis

**Versión 1.4.2** (1.4.2.210: iOS 6.0+)

* (ZD #1129) _player.currentItem.audioOptions devuelve vacío
* (ZD #2109) Primetime PSDK 1.4.1.125 no funciona con Xcode 5.1.1
* (ZD #2137) Bloqueo en PSDK en iOS cuando no se pueden cargar metadatos DRM

**Versión 1.4.1** (1.4.1.125)

* (ZD #1107) Símbolos de duplicado CocoaLumberjack
* (ZD #1644) Modificación del agente de usuario de iOS para objetivos y Sistemas de informes
* (ZD #1850) Archivos Cocoa Lumberjack incluidos en el SDK para iOS
* (ZD#1908) PSDK ignora las etiquetas personalizadas si hay más de 1

**Versión 1.4.0** (1.4.0.32)

* Zendesk #1024 - Función para eliminar anuncios del flujo mediante manifiesto

## Problemas conocidos en 1.4 {#known-issues-in}

* En iOS TVSDK, todos los anuncios se vinculan al manifiesto de contenido. Los comportamientos de publicidad se implementan buscando en función de la duración del contenido y los segmentos de publicidad. Por lo tanto, si las duraciones de los segmentos no son precisas, es posible que la búsqueda no siempre termine en el marco exacto del comienzo o el final de la pausa publicitaria. Incluso si las duraciones van al marco, existe una tolerancia que la propia plataforma impone a la búsqueda y es posible que se muestren algunos marcos o publicidades o contenido. Se trata de una limitación de la plataforma y del modo en que la inserción de anuncios funciona con TVSDK en iOS.
* La decisión de omitir se produce en el evento de búsqueda en este caso. Sin embargo, dado que las duraciones del segmento de publicidad en el manifiesto no representan con precisión la duración real de la publicidad, la búsqueda no es precisa para el marco. Por lo tanto, verá algunos fotogramas de la publicidad cuando se apliquen las directivas de publicidad.
* RECORDING_ERROR: Error al grabar la pantalla.
* Es posible que el vídeo de rotación de licencia no se reproduzca en iOS 11 y que se reproduzca correctamente en iOS 9.x e iOS 10.x.
* En la compatibilidad con VPAID 2.0, si la reproducción está activa en AirPlay, se omiten las publicidades VPAID.
* drmNativeInterface.framework no se vincula correctamente cuando el destinatario mínimo se establece en iOS7 (o posterior).\
   Solución: Especifique explícitamente el `libstdc++6`.  biblioteca dylib de la siguiente manera: Vaya a Destinatario->Generar fases->Vincular binario con bibliotecas y agregar `libstdc++.6.dylib`.

* No se insertó la publicidad posterior para reemplazar la API.
* Al buscar en una pausa publicitaria (sin salir de ella) se emite una notificación de inicio de anuncios de duplicado y pausa publicitaria
* La configuración de currentTimeUpdateInterval no tiene ningún efecto.\
   Nota: En determinadas versiones de iOS, el sistema operativo no carga automáticamente los recursos dentro de PSDKLibrary.framework. Es importante copiar manualmente el archivo PSDKResources.bundle en los recursos del paquete de la aplicación: Vaya a &quot;Fases de compilación&quot; y copie los recursos del paquete.
* La aplicación de referencia no se puede crear con Xcode 8 o versiones inferiores. A partir de la versión 1.4.41 de iOS TVSDK, utilice Xcode 9 para compilar.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.