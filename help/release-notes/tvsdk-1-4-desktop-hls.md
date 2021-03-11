---
title: Notas de la versión de TVSDK 1.4 para Desktop HLS
description: Las notas de la versión de TVSDK para Desktop HLS describen las novedades o los cambios, los problemas resueltos y conocidos de TVSDK DHLS.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5196'
ht-degree: 0%

---


# Notas de la versión de TVSDK 1.4 para Desktop HLS {#tvsdk-for-desktop-hls-release-notes}

Las notas de la versión de TVSDK para Desktop HLS describen las novedades o los cambios, los problemas resueltos y conocidos de TVSDK DHLS.

## Nuevas funciones {#new-features}

**1,4,31**

* **Compatibilidad con varias CDN para anuncios CRS**

   * De forma predeterminada, todos los recursos transcodificados se alojan en CDN de propiedad de Adobe en Akamai. Con la última versión, el servicio de reempaquetado creativo de Adobe (CRS) ofrece la capacidad de cargar los elementos creativos transcodificados en varias CDN, según lo especificado por el cliente.
   * Se añaden nuevas API al TVSDK para permitir la especificación de la URL creativa CRS final cuando no se utiliza la URL predeterminada. Consulte la documentación para aprender a utilizar estas nuevas API.

### Nuevas funciones de las versiones anteriores {#new-features-previous}

**1,4,30**

* **Métricas de facturación**

Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, los Adobes recopilan métricas de uso y utilizan estas métricas para determinar cuánto facturar a los clientes.

**1,4,24**

* **Conexión de red persistente**

Importante: Debe tener instalado al menos la versión 22 o posterior del Flash Player de Adobe.
Las conexiones de red persistentes crean y almacenan una lista interna de conexiones de red que se puede reutilizar para varias solicitudes, en lugar de abrir una nueva conexión para cada solicitud de red. Las conexiones de red persistentes deberían aumentar la eficacia y reducir la latencia del código de red.

En esta versión, Apple Safari y Mozilla Firefox no admiten esta función en Mac.

**1.4.19**

* Compatibilidad con la integridad del flujo de anuncios VPAID.
* Se habilitó la opción de tabulación silenciar en el reproductor de Flash FP 20.0.0.267 para Firefox 42 y posteriores, corrigiendo el problema del bloqueo.

**1.4.18**

* El SDK TVSDK de Primetime Desktop para HLS ahora es compatible con los creativos SWF lineales de VPAID 2.0 para permitir una experiencia de publicidad interactiva y enriquecida en el flujo.

**1.4.10**

* **Abandono de anuncio, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103)**  En el caso de anuncios VAST (creativos) con la regla de reserva activada, TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Ad fallback for VAST and VMAP ads](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Video Heartbeats Library (VHL) actualizado a la versión 1.5**

   * Capacidad para enviar metadatos con el inicio de vídeo o el inicio de vídeo/anuncio/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño.

**1.4.7**

* **Compatibilidad de individualización local**

Compatibilidad con instalaciones locales del servidor de individualización de Adobe para personalizar la solicitud de personalización del cliente para ir a un punto final diferente.

**1.4.6**

* **Encriptado AES de muestra (requiere Flash Player versión 17.0.0.134)**

Ahora se admite el cifrado AES basado en muestras.

**1.4.2**

* **Actualización de Video Heartbeats Library (VHL) a la versión 1.4.0.1**

   * Se ha agregado la capacidad de agrupar diferentes casos de uso de análisis, de otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete . La pausa publicitaria se infiere de las llamadas de método trackAdStart y trackAdComplete .
   * La propiedad playhead ya no es necesaria al rastrear anuncios.

**1.4.0**

* **Señalización de interrupción con** reemplazo de contenido alternativoComo parte de la actualización 1.4 de TVSDK, ahora TVSDK también admite entrar y salir de interrupciones regionales con contenido lineal. Ahora, el TVSDK puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de bloqueo incluso cuando se muestra una programación alternativa en lugar de la programación original.

* **Elimine/reemplace C3** AdsAhora, no se necesita ningún trabajo de preparación adicional para insertar dinámicamente nuevos anuncios en recursos de vídeo bajo demanda (VOD) que salen de la ventana C3. El SDK de TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar de forma dinámica nuevos anuncios. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se emite durante la emisión y se baja inmediatamente para utilizarlo como contenido bajo demanda sin el tiempo adecuado para &quot;limpiar&quot; el recurso.

## Problemas resueltos {#resolved-issues}

>[!NOTE]
>
>Se recomienda encarecidamente a todos los clientes de TVSDK que utilicen CRS que actualicen al menos a TVSDK 1.4.32 en iOS, Android y Desktop HLS. Esta actualización sustituirá a la implementación de aplicación existente. Después de la actualización, compruebe las solicitudes de URL creativas de CRS en una herramienta de proxy (por ejemplo, Charles) para verificar que la versión en la ruta refleja la versión 3.1. Por ejemplo,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versión 1.4.41**

* Zendesk #33777 - SWF de token de host local para la compilación de distribución DHLS expiró.

   Actualización del token localhost para la demostración de PMP en DHLS.

### Problemas resueltos en versiones anteriores {#resolved-issues-previous}

**Versión 1.4.38**  (891)

* Zendesk #30731 - TVSDK no reproduce varias publicidades VPAID en un AdBreak.

   Se ha corregido la reproducción de varias publicidades VPAID en un AdBreak.

* Zendesk #29968 - Doble pizarra.

   El reproductor de vídeo puede repetir el último segmento de un punto cuando se produce un cambio de ABR. Debido a esto, a veces, el último segmento de preroll repetido. Esto se ha solucionado.

**Versión 1.4.35**  (879)

* Zendesk #26058 - Admite eventos VPAID nativos

**Versión 1.4.33**  (873)

* Zendesk #21701 - Envíe la URL creativa original para la solicitud CRS 1401 en lugar de la URL normalizada.

   Se ha corregido el problema en el que las URL ya empaquetadas se solicitaban para la transcodificación, según lo requerido por el servidor CRS.
* Zendesk #26197 - Compresión anamorfa no se reproduce en la resolución de visualización deseada.

   **Nota**: Este problema requiere el reproductor de Flash 24.0.0.194 o posterior.

   Se ha corregido el problema por el que se usaban entradas que faltaban en las tablas de relación de aspecto para calcular la anchura de salida.

* Zendesk #26840: la detección de HDCP falla en IE11 + Windows7 después del segundo intento.

   **Nota**: Este problema requiere el reproductor de Flash 24.0.0.218 o posterior.

   Este problema se ha resuelto modificando el procesamiento de la cola de mensajes principal de AdobeCP para que se repita en toda la cola, en lugar de simplemente bloquear el primer mensaje.

* Zendesk #27460 - La nueva cuenta de Akamai no puede gestionar una solicitud de CDN POST.

   La nueva cuenta de CDN no puede gestionar una solicitud de CDN de POST. Este problema se resolvió actualizando el código para que la solicitud de publicidad de cdn.auditude.com fuera GET en lugar de POST.
* Zendesk #27619 - Flash bloqueado en Windows 10

   **Nota**: Este problema requiere el reproductor de Flash 24.0.0.218 o posterior.

   Este problema se ha resuelto al evitar un error como resultado de direcciones URL largas.

* Zendesk #28218 - El evento de seguimiento no se activa mientras el reenvío desde el punto de reanudación

   Este problema es el mismo que en Zendesk #26592. Se ha corregido el problema en el que se permitían operaciones de búsqueda cuando el reproductor de medios está en el estado PREPARADO para flujos de VOD.

**Versión 1.4.32**  (867)

* El evento de seguimiento Zendesk #26592 no se activa cuando la reproducción comienza desde el punto de reanudación

El código no actualizaba el elemento de pausa publicitaria pre-roll cuando el punto de reanudación no era cero. Este problema se resolvió añadiendo lógica para actualizar el código cuando los tiempos de inicio del intervalo no coinciden.

* Zendesk #27022 Los anuncios no se están reproduciendo la segunda vez que se reproduce un recurso

Se han corregido las excepciones con los métodos de matriz.

**Versión 1.4.30**  (855)

En esta versión se han resuelto los siguientes problemas para TVSDK:

* Zendesk #22898 - Los subtítulos que faltan no deberían provocar errores en la reproducción.

**Nota**: Este problema requiere el reproductor de Flash 23.0.0.185 o posterior.

Este problema se ha resuelto permitiendo que TVSDK continúe la reproducción, incluso si el manifiesto no tiene el WebVTT M3U8, y solo registre una advertencia.

* Zendesk #23454 - Los anuncios de terceros (VPAID) no se gestionan correctamente

Este problema se resolvió administrando correctamente los anuncios de VPAID en función de los ID de contenido en lugar de intervalos de tiempo.

* Zendesk #24528 - Métricas de uso de TVSDK para la facturación.

Importante: Este problema requiere el reproductor de Flash 23.0.0.185 o posterior.

* Problema de Zendesk # 25432 Subtítulos durante el cambio de tamaño del reproductor.

Importante: Este problema requiere el reproductor de Flash 23.0.0.185 o posterior.

El código del mapa de textura de visualización del rótulo se ha corregido para controlar correctamente las coordenadas durante el cambio de tamaño del reproductor.

La biblioteca de Video Heartbeat (VHL) se ha actualizado a la versión 1.5.9 para resolver los siguientes problemas:

* Zendesk #23730 - Las métricas de velocidad de bits están vacías

Este problema se resolvió rastreando los cambios de velocidad de bits en VideoAnalyticsTracker.

* Se ha añadido una nueva API, assetDuration, a PTVideoAnalyticsTrackingMetadata para actualizar la duración de los recursos para las emisiones en directo/lineales.

**Versión 1.4.28**  (848)

* Zendesk #25027 - Auditude no funciona en la versión de escritorio 1.4.27

Este problema se resolvió añadiendo el código para comprobar AUDITUDE_METADATA_KEY y haciendo que AUDITUDE_METADATA_KEY y ADVERTISING_METADATA_KEY sean intercambiables.

* Zendesk #24428 - Problema frecuente de almacenamiento en búfer con TVSDK para reproducir un DRM HLS

Este problema se ha resuelto teniendo en cuenta que cuando no hay ninguna configuración de publicidad, TVSDK puede acelerar el procesamiento eliminando la retención de anuncios previos a la emisión y la retención de reservas activas en la línea de tiempo diseñada para sincronizar la inserción de anuncios.

* Zendesk #24344 - Desactive los archivos WebVTT para mejorar los tiempos de inicio.

**Nota**: Este problema requiere el reproductor de Flash 23 o posterior.

Este problema se ha resuelto cargando los archivos WebVTT solo cuando es necesario mostrar los subtítulos.

* Zendesk #24994 - Los subtítulos se retiran del reproductor cuando regresa de una pausa comercial

**Nota**: Este problema requiere el reproductor de Flash 23 o posterior.

El código EOC falso provocaba que desapareciera la visualización del rótulo. Este problema se resolvió obligando a los códigos de 608 subtítulos RU2, RU3 y RU4 a proporcionar la visibilidad correcta en la ventana activa actual.

**Versión 1.4.27**  (844)

* Zendesk #21554 - Las señalizaciones de error de TVSDK no se activan para el tipo de aplicación = video/mp4

Este problema se ha resuelto habilitando a TVSDK para que haga ping en las URL de seguimiento de errores correctas en formatos de recurso no válidos.

* Zendesk #23402: Reproducción de publicidad incompleta

**Nota**: Este problema requiere el reproductor de Flash 23 o posterior.

Después de obtener un error 404 en determinadas solicitudes, puede producirse un bloqueo. Este problema se ha resuelto asegurándose de que la conexión no se cierre mientras se gestiona la respuesta. La resolución garantiza que los archivos de publicidad VPAID no se contabilicen incorrectamente, por lo que no se lanzan mientras se descargan.

* Zendesk #23621 - Reintento está fallando en 400 y 404

**Nota**: Este problema requiere el reproductor de Flash 23 o posterior.

Se ha corregido un problema que provocaba la corrupción de metadatos DRM al cambiar entre perfiles diferentes.

* Zendesk #23705 - Anuncios de vídeo congelados durante las pausas con título publicitario

**Nota**: Este problema requiere el reproductor de Flash 23 o posterior.

Este problema es el mismo que en Zendesk #23621.

* Zendesk #23905 - Algunas pausas publicitarias se omiten en las pausas publicitarias

**Nota**: Este problema requiere el reproductor de Flash 23 o posterior.

El código de red nativa de Windows se ha corregido para garantizar que las conexiones no cierren controladores que otras conexiones estén usando actualmente.

* ticket #24029 - Los flujos FER HLS no reproducen todos los anuncios mid-roll en el archivo .json mid-roll.

Este problema se ha resuelto permitiendo a los clientes establecer parámetros personalizados por separado en la instancia de oportunidad para que los clientes no tengan que anular el generador de oportunidades.

**Versión 1.4.26**  (839)

* Zendesk #18854 - Actualización de la lógica de selección creativa basada en las reglas CRS
   * Se ha proporcionado asistencia para actualizar la lógica de selección creativa basada en las reglas CRS

* Implementación de Zendesk #22725 - playManager.beginPlayback() en la aplicación de ejemplo para escritorio

   * Se ha corregido eliminando esta llamada redundante al final de startPlaybackFromFlashVars, ya que el método se llama desde setupVideo()

* Zendesk #22807 - Excepción de referencia nula de SeekManager

   * Se ha corregido proporcionando la protección necesaria del puntero NULL dentro de SeekManager en relación con _dispatcher.

* Zendesk #22822 - Búfer frecuente al utilizar TVSDK para reproducir un HLS claro

   * Se ha corregido eliminando la oportunidad inicial generada por adSignalingModeOportunityGenerator si no hay publicidad

* Zendesk #23378 - Bloques de integridad de la emisión rules.xml

   * Se ha corregido cargando el archivo rules.xml a través del flujo de trabajo de integridad de la secuencia

**Versión 1.4.24**  (817)

* Zendesk #19851 - Cuando el reproductor se adapta a una velocidad de bits diferente, salta unos pocos fotogramas atrás en el tiempo con la nueva velocidad de bits, lo que hace una experiencia incómoda

**Nota**: Este problema requiere el reproductor de Flash 22.0.0.175 o posterior.

Se ha resuelto el problema en el que el adaptador DRM se restablece después de descargar una pequeña fracción de un segmento no se restaura correctamente.

* Zendesk #20784 - Análisis: Se completa la activación de contenido para transiciones de vídeo en directo

Este problema se ha resuelto añadiendo una API (trackVideoComplete) para almacenar en déclencheur manualmente la finalización del contenido durante una sesión de seguimiento de vídeo LINEAR/LIVE.

Se han actualizado las bibliotecas siguientes:

* Zendesk #21643 - Los anuncios VPAID no se reproducen completamente

   * Biblioteca AdobeMobile a 4.10.0
   * Biblioteca VHL a 1.5.6
   * Biblioteca VHL-Nielsen 1.6.7

Este problema se resolvió usando una ventanilla de altura cero para llenar el escenario cuando se está reproduciendo un anuncio VPAID.

* Zendesk #22110 - Analytics: Agregue un campo h:sc:ssl a las llamadas de seguimiento de Heartbeat

Se han corregido los problemas relacionados con SSL y la biblioteca VHL que se utiliza en TVSDK se ha actualizado a la última versión.

* Zendesk #22608 - El vídeo muestra de forma intermitente una pantalla negra (requiere el Flash Player 22.0.0.175 o posterior)

Durante la velocidad de bits adaptable, con el límite máximo de velocidad de bits, la recarga del vídeo muestra de forma intermitente una pantalla negra aunque el cliente vea actualizaciones de posición y se comporta como si estuviera reproduciendo contenido.

**Versión 1.4.23**  (809)

* Zendesk #2887 - Problema de omisión del anuncio posterior a la emisión cuando se aplicó la lógica de regla de anuncio al TVSDK

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Se ha corregido el problema por el que los anuncios posteriores a la emisión se omitían cuando se aplicaba la lógica de regla de anuncio al TVSDK.

* Zendesk #19863 - Anuncio con archivo multimedia VPAID descartado

Si un anuncio en línea amplio tiene varios archivos multimedia y el primer anuncio es un VPAID, el anuncio en línea no se reproduce para emisiones en directo. Este problema se resolvió seleccionando un archivo multimedia diferente en su lugar.

* Zendesk #21021 - Repetición de audio de enlace tardío

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Se ha corregido el problema de repetición de audio.

* Zendesk #21125 - Regreso desde una pausa publicitaria en directo/lineal temprano

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Esta versión es compatible con el retorno de una pausa publicitaria antes de que se reproduzca la pausa publicitaria hasta el final. El retorno anticipado se indica mediante una etiqueta de manifiesto personalizada.

* Zendesk # 21369 El audio de enlace tardío causa un tiempo inconsistente

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

El problema de repetición de audio que se ha solucionado también ha corregido este problema.

* Zendesk #21760, 20921 - Audio Video Desync on Seek.

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Se ha corregido el problema de repetición de audio.

* Zendesk #22024 - Error al ejecutar el TVSDK

Se ha corregido el problema por el que el reproductor de referencia no reproduciría ningún flujo y lanzaba una excepción al principio.

**Versión 1.4.22**  (791)

* Zendesk #17580 - Error de tiempo de ejecución de Primetime con código 3357

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.197 o posterior.

Se han corregido los errores aleatorios 3357 que se producían al inicializar correctamente el deviceID cuando se llama a storeVoucher() .

* Zendesk #21334 - Valor de tiempo de espera de solicitud de anuncio TVSDK para solicitudes de anuncios de terceros

En esta versión se ha agregado el tiempo de espera de solicitud de publicidad global.

**Versión 1.4.21**  (782)

* Zendesk #19580 TVSDK espera la finalización de la resolución de contenido antes de enviar `PTTimedMetadataChangedNotification` notificaciones

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

Este problema se resolvió en el reproductor de referencia de escritorio al proporcionar la capacidad de establecer etiquetas de anuncio y agregar un generador de oportunidades personalizado que muestre cómo suscribirse a señales personalizadas y cómo procesar estas señales en un archivo VOD.

* Zendesk #20806 Los futuros anuncios mid-roll en la ventana de DVR no se déclencheur después de intercambiar cámaras

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

Este problema se ha resuelto actualizando la aplicación para establecer _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) para deshabilitar la inserción de anuncios previos a la emisión en un intercambio PIP y, como resultado, no se genera ninguna oportunidad previa a la emisión.

Se introdujo una funcionalidad de clasificación para corregir la colocación de publicidad fuera de secuencia que resultó en una duración de contenido principal negativa.

* Zendesk #20522: No se pueden omitir los anuncios de VPAID 2.0

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

* Este problema se resolvió saltando los anuncios VPAID durante el perdón de anuncios.
* Cuando la política de adbreak está configurada para omitirse, los eventos de ad and ad break siguen enviándose. El estado del reproductor es incoherente.

Este problema se resolvió para comportarse correctamente y no distribuir eventos cuando se omite la pausa publicitaria.

* Zendesk #20955 Establezca pares de clave-valor en la propiedad customParameters a través del generador de oportunidades

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

La solicitud de audiencia analiza AuditudeSettings para ver parámetros personalizados al crear una unidad de publicidad para solicitudes de publicidad.

Este comportamiento se cambió para incluir parámetros personalizados del objeto de oportunidad en la solicitud. Además, no se pueden empaquetar varias oportunidades con diferentes parámetros personalizados en una solicitud de Auditude.

* Zendesk #21227 - m3u8 no juega consistentemente

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.211 o posterior.

Este problema se ha resuelto permitiendo que el TVSDK ignore el manifiesto (subperfiles HLS) que contiene el códec AC3 que el TVSDK no admite (envolvente).

**Versión 1.4.20**  (762)

* Zendesk #19181 - Trick juegue rápido hacia adelante para que el punto de vida se bloquee en la corriente.

**Nota**: Este problema requiere el reproductor de Flash 20.0.0.306 o posterior.

* Zendesk #19286 - Se produjo un accidente de Flash Player al buscar de ida y vuelta en un flujo FER.

**Nota**: Este problema requiere el reproductor de Flash 20.0.0.306 o posterior.

Las interrupciones ocasionales que se produjeron al buscar en Google Chrome se resolvieron cerrando las consultas, si tardan demasiado en obtener una respuesta o si el socket se está cerrando.

* Zendesk #19305 - Reproducción de disquete encontrada al reproducir un flujo con interrupciones A/V.

**Nota**: Este problema requiere el reproductor de Flash 20.0.0.306 o posterior.

Este problema se resolvió enviando una advertencia.

* Zendesk # 19359 - Flash Player colapsado debido a la posición de #EXT-X-FAXS-CM: en el manifiesto de nivel de conjunto.

Este problema se resolvió cuando la etiqueta #EXT-X-FAXS-CM aparece en la lista de reproducción superior antes de la velocidad de bits individual o los segmentos de la lista de reproducción.

* Zendesk #19489 - Fast Forward to Live Point stalls plugin (transmisión en vivo)

Este problema es el mismo que Zendesk #19181.

* Zendesk #19699 - TVSDK no cambia entre las pistas de subtítulos de WebVTT

Este problema se solucionó haciendo que el volcado del reproductor y recargue el manifiesto cuando cambia una pista y corrigiendo el problema de conversión de cadenas UTF8 que afectaba a los nombres de seguimiento de subtítulos WebVTT de doble byte.

**Versión 1.4.19**  (1.4.19.738)

* Zendesk #18234 - Flash Player se bloquea reproduciendo los flujos con cadenas Unicode en CC

Este problema requiere Flash Player FP 20.0.0.267 o posterior y se ha resuelto administrando correctamente la cadena Unicode.

* Zendesk #18304 - Compatibilidad de integridad de flujo para anuncios VPAID

Esta función requiere Flash Player FP 20.0.0.267 o posterior y se introdujo en la versión 1.4.19.

* Zendesk #18766 - El reproductor de referencia no puede mostrar caracteres Unicode no latinos en los nombres de pistas CC

Esta función requiere Flash Player FP 20.0.0.267 o posterior y se ha corregido manejando correctamente la cadena Unicode.

* Zendesk #18804 - El reproductor se bloquea en Firefox 42

Este problema requiere el Flash Player FP 20.0.0.235 o posterior y es el mismo problema que Zendesk #18723.

* Zendesk #18864 - Bloqueo de plugin completo de Flash Player

Este problema requiere el Flash Player FP 20.0.0.235 o superior y es el mismo que Zendesk #18723.

* Zendesk #18998 - Si las marcas de tiempo de audio y vídeo no coinciden, se produce una descarga interminable de segmentos en caso de discontinuidad.

Este problema se ha resuelto ignorando la brecha entre las marcas de tiempo y reproduciendo el contenido descargado.

* Zendesk #19093 - Los anuncios mid-roll solo se pueden ver una vez con contenido de reproducción en directo y de eventos completos (FER), pero estos anuncios no se pueden ver de nuevo cuando se redirigen rápidamente o se buscan más allá de los anuncios

En el selector predeterminado de adPolicy de Primetime, si se ve un anuncio mid-roll, el adBreak no se mueve a la posición buscada al completar una búsqueda. Para volver a reproducir el anuncio, después de la búsqueda, la aplicación necesita anular la función selectAdBreaksToPlay() .

* Zendesk #19101 - Al rebobinar en anuncios Midroll sin resolver, se elimina la ubicación de la publicidad.

Este problema se resolvió permitiendo al reproductor actualizar la hora de playMetrics, la hora mínima de oportunidad y la línea de tiempo.

* Zendesk #19102 - Problemas con FER y modo de truco

Este problema requiere el Flash Player FP 20.0.0.267 o posterior y se ha resuelto estableciendo correctamente advertisingMetadata.adSignalingMode .

* Zendesk #19175 - A veces, los anuncios previos a la emisión no se muestran la primera vez que se reproduce la emisión.

Este problema se resolvió añadiendo una nueva API, adRequestTimeout, a AuditudeSettings para un tiempo de espera de solicitud de publicidad. Los usuarios ahora pueden anular el tiempo de espera predeterminado de las solicitudes de publicidad de los 10 segundos.

**Versión 1.4.18**  (1.4.18.722)

* Zendesk #3324 - El informe de anuncios de Primetime no rastrea pausas publicitarias cuando no hay medios publicitarios en un VMAP.

Cuando una pausa publicitaria está vacía, los eventos de seguimiento de inicio y finalización de la pausa publicitaria no se estaban agrupando. Este problema se resolvió enviando pings de inicio de pausa publicitaria en pausas publicitarias vacías, como VMAP AdBreak, con un nodo AdSource válido.

**Versión 1.4.17**  (1.4.17.702)

* Zendesk #17168: los subtítulos no aparecen durante 10 segundos más o menos después de alternar la visibilidad

Este problema se resolvió proporcionando compatibilidad para la etiqueta EXT-X-MEDIA-TIME para archivos de subtítulos vtt.

* Zendesk #17983 - La falta de descarga de claves para un manifiesto provoca que falle toda la reproducción del manifiesto

**Nota**: Debe tener al menos el Flash Player FP 19.0.0.245 o superior.

A veces, al reproducir contenido en directo, puede haber claves no válidas en el manifiesto (por ejemplo, en los periodos de bloqueo), pero otros intervalos de tiempo pueden tener claves válidas y se seguirán reproduciendo. Anteriormente, cuando no se podía descargar una clave incluida en un manifiesto, se producía un error en todo el manifiesto. Ahora, el manifiesto solo falla cuando no se pueden descargar todas las claves de la lista. Si algunas claves son válidas, pero no se pudieron descargar algunas, se reproducirá el contenido. Seguiremos fallando si intentamos reproducir un segmento que requiera una clave que no tenemos.

* Zendesk #18554 - Integridad de la emisión recortando las cookies en algunos casos

**Nota**: Debe tener al menos el Flash Player FP 19.0.0.245 o superior.

Se ha corregido un error en el código de manipulación de cookies que podía truncar valores de cookies.

**Versión 1.4.16**  (1.4.16.684)

* Zendesk #3732 - Añada compatibilidad con proxies en Chrome para la integridad de la emisión (requiere Flash Player FP 19.0.0.207 o bueno)

Esta es una mejora.

* Zendesk #4244 - Problemas de transmisión al pasar de PTS

Este problema se resolvió detectando el rollover y administrando la discontinuidad por tipo de carga útil y no de forma genérica.

* Zendesk #4487 - Seguimiento del canal de contenido lineal

Este problema se resolvió reiniciando el rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* Zendesk #17427 - Integridad del flujo de Adobe no funciona a través de un proxy en Chrome (Win7) ()

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o buenos.

Este problema es el mismo que Zendesk #3732.

* Zendesk #17907 - Retraso en la emisión en directo de pHLS con Flash Player 19

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o buenos.

Este problema se resolvió gestionando los flujos en directo en los que los dominios de los archivos TS cambian al volver a cargar el manifiesto en directo y los archivos se descargan dos veces.

* Zendesk #17931 - El contenido HLS con pizarra al principio falla en la reproducción

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o buenos.

El problema se resolvió al gestionar flujos sin audio en los primeros 2 segundos del primer archivo TS.

* Zendesk #17934 - Fallo de transmisión en directo con Flash 19.0.0.185

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o buenos.

El problema se resolvió al gestionar emisiones en directo con intervalos de tiempo entre fotogramas de audio y vídeo en los límites de segmentos.

* Zendesk #17973 - Último Flash Player 19.0.0.185 se bloquea durante la mitad de la emisión

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o buenos.

El problema se resolvió al administrar audio no mezclado con inserción de anuncio mid-roll. (Se produce el conmutador de analizador y, en cualquier momento de la reproducción, el contenido pasa al anuncio mid-roll, o a mitad de la reproducción del anuncio, etc.)

* Zendesk #18049 - Flash 19 bloqueado con Firefox 42 beta

Este problema es el mismo que Zendesk #17973.

**Versión 1.4.15**  (1.4.15.678)

* Zendesk #4377: Active el evento AD_BREAK_SKIPPED cuando omita una pausa publicitaria debido a la política publicitaria.

La corrección era añadir AD_BREAK_SKIPPED si se omitía un anuncio.

* Zendesk #4496 - Integridad de la transmisión: Error 102100 con redirecciones a flujos tokenizados.

La corrección era añadir compatibilidad para establecer la propiedad AVNetworkConfiguration useCookieHeaderForAllRequests a través de TVSDK.

* Zendesk #17179 - El reproductor de Flash se bloquea en varios cambios de SAP para contenido cifrado.

Se corrigió un bloqueo durante la reproducción de contenido cifrado.

**Nota**: La corrección requiere el Flash Player 19.0.0.200 o superior.

* Zendesk #17499 - cómo no eliminamos los midrolls después del reloj, sino que eliminamos el preroll del contenido del fer

Se ha agregado un tipo a AdBreakTimelineItem (AdBreakTimelineItem.placementType) para que AdPolicySelector pueda devolver una política diferente para contenido pre-roll, mid-roll y post-roll.

* Zendesk #17665 - Regulación del ancho de banda

La corrección era eliminar la lógica para cambiar el tamaño del búfer de destino al tamaño inicial del búfer cuando comienza el almacenamiento en búfer.

**Versión 1.14.14**  (1.4.14.771)

* Zendesk #17363 - Corrección de la documentación de README para reproductor de referencia

   * Aclarar las instrucciones para descargar e instalar playerglobal.swc.
   * Añada instrucciones para actualizar la configuración del proyecto con una versión específica del reproductor Flash.
   * Actualice la configuración del proyecto AdvertisingOverlay para utilizar la versión mínima del reproductor.
   * Actualizar la configuración del proyecto principal de referencia para utilizar la versión 11.9 específica del reproductor

* Zendesk #17471 - Congelación de reproductor

Corrección parcial para un problema en el que un anuncio no se reproduce desde el principio después de la búsqueda.

* Zendesk #17496 - Podbuster no se resuelve cuando vuelve a buscar en la ventana DVR

Proporcione parámetros personalizados para cada pausa publicitaria.

**Versión 1.4.13**  (1.4.13.660)

* Zendesk #4037 - No se puede usar el error de perfil (requiere Flash Player 18.0.0.232 o bueno)

corrección del problema de análisis de url cuando el parámetro de consulta contiene &quot;http&quot;

* Zendesk #4260 - Flash Player 18 se bloquea en IE11 (requiere Flash Player 18.0.0.232 o bueno)

Se ha corregido un bloqueo al reproducir vídeo en modo de pantalla completa con IE11

* Zendesk #4262 - El reproductor Adobe Primetime se bloquea en windows 10 (requiere el Flash Player 18.0.0.232 o bueno)

Se ha corregido un bloqueo al reproducir vídeo en modo de pantalla completa con FireFox en Windows.

* Zendesk #4279 - Inserción de anuncios de HLS TVSDK -302 problema de redireccionamiento en iOS y escritorio

Se ha corregido un problema por el que una URL no obtenía el tipo de URL reconocido correctamente porque no tenía extensión

* Zendesk #4306 - Bloqueo de Flash Player al pasar solo a pantalla completa en Win (requiere Flash Player 18.0.0.232 o bueno)

Se ha corregido un bloqueo al reproducir vídeo en modo de pantalla completa en Windows.

* Zendesk #4480 - Faltan eventos de etiqueta ID3 (requiere Flash Player 18.0.0.232 o bueno)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI y CRS | Mejora: Gestione elementos dinámicos en determinadas direcciones URL de archivos multimedia.

Se ha actualizado el servicio de reempaquetado creativo para que gestione correctamente los anuncios con direcciones URL creativas dinámicas.

* PTPLAY - 2114 - Compatibilidad con reproducción MP4.

Ahora se admite la reproducción básica del contenido de MP4, que incluye la reproducción, la pausa y la búsqueda.

Los siguientes requisitos son los Flashes Player 18.0.0.225 o buenos:

* Zendesk #3992 - Velocidad TrickPlay adicional.

TrickPlay ahora acepta tasas superiores a 16x: +/- 32, +/-64 y +/-128.

* Zendesk #3113 - Bloqueo del complemento de Flash Player

Se ha corregido un bloqueo al intentar reproducir un anuncio de redireccionamiento en Mac Firefox.

* Zendesk #4037 - Sin error de perfil utilizable
* Zendesk #4262 - El reproductor Adobe Primetime se bloquea en windows 10

Se corrigió un error en Windows Firefox durante la reproducción en pantalla completa.

**Versión 1.4.11**  (1.4.11.648)

* Zendesk #1869 - Problema que cambia el tamaño de la fuente (requiere el Flash Player 18.0.0.200)

Permiten que se utilicen tamaños de rótulos en el código de subtítulos WebVTT.

* Zendesk #3113 - Bloqueo del complemento de Flash Player (requiere Flash Player 18.0.0.200)
* Zendesk #3268 - Escritorio: El reproductor de vídeo comienza a parpadear después de +- 40/50 segundos y comienza a quedar negro después de +- 90 segundos (requiere Flash Player 18.0.0.200)

Se ha corregido un error de vídeo de etapa.

* Zendesk #3670 - Error INVALID_PARAMETER en VOD al buscar en el reproductor de referencia (requiere Flash Player 18.0.0.200)

InvalidateProfiles en ThreadSeek cuando se detecta un nuevo periodo.

* Zendesk #3896 - Bloqueo de Flash Player con la integridad de la emisión activada en Chrome (requiere Flash Player 18.0.0.200)

Se ha corregido un bloqueo en el modo de red nativo en pimienta

* Zendesk #3905 - El reproductor TVSDK no se carga cuando está alojado en CDN

Se han corregido problemas para encontrar el token comodín cuando pageDomain es diferente del dominio swf.

**Versión 1.4.10**  (1.4.10.642)

* Zendesk #3249 - El reproductor web TVSDK bloquea el Flash en Firefox

Se ha corregido un bloqueo ocasional del Flash Player con Firefox en Mac cuando un flujo, que se reproducía en un monitor externo, cambiaba a un flujo de velocidad de bits superior.(requiere el Flash Player 18.0.0.160)

* Zendesk #3268 - Escritorio: El reproductor de vídeo comienza a parpadear después de `+-` 40/50 segundos y comienza a quedar negro después de `+-` 90 segundos

Se ha corregido un problema en Mac Chrome por el que la emisión empezaba a parpadear y, finalmente, se volvía negra. (requiere el Flash Player 18.0.0.161)

* No se rellena la macro de Zendesk #3304 - VAST 3.0 `[ERRORCODE]`

   * el código de error 400 se expondrá si el anuncio en línea tiene un elemento creativo incorrecto.
   * `[ERRORCODE]` la macro estará codificada en la dirección URL

* Zendesk #3601 - Solicitud de mejora: Administración del complemento de envoltura

   * TVSDK mostrará envoltorios complementarios que contengan recursos (html, iframe o static ) que se cerrarán en línea. (si la línea en línea no contiene una para ese tamaño)
   * Se ignorarán los acompañantes con recurso, a menos que se usen para la visualización. (no se usa para el seguimiento )
   * Solo se utilizarán complementos envolventes sin recurso para fines de seguimiento. ( complemento envolvente que solo contiene seguimiento )

**Versión 1.4.9**

* Zendesk #2615 - problema al eliminar la vista HLS de la pantalla de escritorio

Se ha agregado el método clearVideo() a MediaPlayer. Borra el fotograma de vídeo mostrado borrando AVStream del objeto StageVideo. Solo debe llamarse si el vídeo está en pausa y debe llamarse a replaceCurrentResource o replaceCurrentItem antes de que se pueda volver a llamar a play() .

* Zendesk #3169 - Actualización del reproductor de referencia con la integración de Adobe Analytics

El reproductor de referencia se ha actualizado con la integración de Adobe Analytics

* Zendesk #3296 - Desktop HLS TVSDK - VAST Anuncios de terceros no reproducidos

los tipos de mime para el formato HLS distinguían entre mayúsculas y minúsculas, esto era incorrecto y se ha cambiado, por lo que ya no distinguen entre mayúsculas y minúsculas

**Versión 1.4.8**

* Zendesk #2737 - Reproductor de escritorio - Error 106000 (requiere Flash Player 17.0.0.184)
* Zendesk #3007 - Los anuncios previos a la emisión no aparecen después de actualizar al Flash Player 17 (requiere el Flash Player 17.0.0.184)
* Zendesk #3085 - Reproductor HLS de escritorio lanza 106000 Error después de 60 segundos (requiere Flash Player 17.0.0.184)

**Versión 1.4.7**

* Zendesk #2760 - Etiqueta DISCONTINUITY ignorada durante el modo TrickPlay (requiere la versión de Flash Player 17.0.0.158)
* Zendesk #2760 - Etiqueta DISCONTINUITY ignorada durante el modo TrickPlay (requiere la versión de Flash Player 17.0.0.158)

**Versión 1.4.6**

* Zendesk #2652: Documentación de Auditude para escritorio HLS, documentación de Auditude aclarada de media_id para escritorio HLS

**Versión 1.4.5**

* Zendesk #2256 - Acceso a la lista de reproducción maestra, PSDK actualizado para distribuir eventos timedMetadata para etiquetas suscritas en la lista de reproducción maestra. (requiere la versión 17.0.0.134 de Flash Player)
* Zendesk #2417 - El reproductor que intenta descargar subtítulos antes del inicio de la reproducción, WebVTT estaba usando una variable de número de segmento incorrecta para la coincidencia de números de segmento. El error solo aparecería para los medios que tienen índices de segmento que comienzan en cero. (requiere la versión 17.0.0.134 de Flash Player)
* Zendesk #2537 - El reproductor de Flash se bloquea al utilizar el plugin de pimienta con Chrome (requiere la versión de Flash Player 17.0.0.134)
* Zendesk #2547 - subtítulos en árabe: El texto debe alinearse con la justificación correcta (requiere la versión 17.0.0.134 del Flash Player)

**Versión 1.4.4**

* Zendesk #1561 - Re: `[Adobe Primetime]` Actualización: Soporte de conmutación por error basado en el cliente HLS para PROGRAM-DATE-TIME en el PSDK de escritorio (requiere la versión de Flash Player 16.0.0.305 o bueno)
* Zendesk #2197 - `[Ads]` Seguimiento de errores de publicidad
* Zendesk #2286 - Solicitud de funciones: Proporcionar información sobre el estado de carga de la publicidad (VPAID)
* Zendesk #2285 - Solicitud de funciones: Omitir publicidad después de una duración de tiempo de espera especificada
* Error #3921755 - Actualización de la biblioteca OpenSSL a la versión 1.0.1L de Flash Player (requiere la versión de Flash Player 16.0.0.305 o bueno)

**Versión 1.4.2**

* Zendesk #1303 - Desplazamiento vertical para subtítulos (requiere la versión de Flash Player 16.0.0.235 o la fecha buena de lanzamiento prevista: Diciembre de 2014)
* Zendesk #1870 - Activación y desactivación de subtítulos (requiere la versión de Flash Player 16.0.0.235 o la fecha buena de lanzamiento prevista: Diciembre de 2014)
* Zendesk #2110 - La reproducción se atasca después de intentar entrar a pantalla completa durante un anuncio VPAID (requiere la versión de Flash Player 16.0.0.235 o la fecha de lanzamiento esperada buena: Diciembre de 2014)
* Zendesk #2199 - `[VPAID]` Reproductor no responde al buscar una pausa publicitaria anterior
* Zendesk #2358 - Re: `[Analytics]` Datos de capítulo incorrectos

**Versión 1.4.1**

* Se ha actualizado la API de apagones para que sea coherente con la implementación de Android e iOS.

**Versión 1.4.0**

* Zendesk #1024 - Función para eliminar un anuncio del flujo a través de un manifiesto
* Zendesk #1423 - El fallo de reproducción de HLS está bloqueando el Flash Player (sin error notificado)
* Zendesk #1674 - ClosedCaption No aparece, se muestran correctamente los 708 subtítulos cuando faltan los códigos 0x03 ETX.

## Problemas conocidos {#known-issues}

* Subtítulos no funcionarán con contenido de solo audio porque el sistema de subtítulos necesita que el vídeo funcione.
Sin vídeo, no hay ninguna dimensión de ventanilla móvil y sin una dimensión de ventanilla móvil, no se puede mostrar ningún gráfico para los rótulos.
* La integridad del flujo es ligeramente más lenta en Google Chrome debido a las restricciones del entorno limitado de Chrome.
* En TVSDK 1.4, si desactiva autoPlay, puede producirse un error de DRM cuando el reproductor permanece inactivo durante al menos un minuto. Para solucionar este problema, al deshabilitar autoPlay pero precargar recursos, modifique `ReferenceCore.as` cambiando el contenido de `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versión 1.4.13** PTPLAY-8501: cuando VMAP devuelve dos anuncios directos no transcodificados MP4, la misma visita en el orden previsto se reproduce dos veces.

* **Versión 1.4.2** En la versión 16 del Flash Player, se identificó un problema con la lógica ABR &quot;apagándose&quot;, después de que el reproductor entrara en un evento de almacenamiento en búfer vacío. El problema evita que la velocidad de bits se apague en entornos de ancho de banda incorrecto una vez que el reproductor entra en estado de almacenamiento en búfer. Para solucionar el problema, haga que la aplicación establezca el `BufferControlParameters.initialBufferTime` de forma temporal como `BufferControlParameters.playbackBufferTime` durante el estado de almacenamiento en búfer (es decir, en un evento `BufferEvent.BUFFERING_BEGIN` ) y luego restablézcalo de nuevo en los valores establecidos en el evento `BufferEvent.BUFFERING_END` . La solución para este problema estará disponible en la próxima versión de parches de la versión 16 del Flash Player.

* **Versión 1.4.0**

   * PTPLAY-1634 - La misma etiqueta suscrita tiene diferentes marcas de hora en diferentes ventanas en vivo. Cuando se mueven ventanas en vivo, la misma etiqueta en cada una de ellas debe tener las mismas marcas de tiempo. Sin embargo, a veces las mismas etiquetas tienen diferentes marcas de tiempo.
   * PTPLAY-28 - La cronología de MediaPlayer no incluye saltos vacíos.
   * Se requiere un archivo de directiva entre dominios (cross-domain.xml) para que el permiso pueda transmitir contenido desde un dominio diferente. [Configuración de un archivo cross-domain.xml para la transmisión](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html) HTTP.
   * Error #3694203 - En un flujo DVR, la búsqueda desde dentro de un anuncio de reproducción a mitad de la emisión puede provocar la congelación del navegador
   * Error #3753725 - selectPolicyForSeekIntoAd no tiene en cuenta si se ha visto la pausa publicitaria
   * Error #3754529 - Los anuncios previos a la emisión no se eliminan del flujo cuando se vuelve a buscar en un flujo DVR en directo
   * Error #3761896 - Si se permite la búsqueda durante la reproducción del anuncio, los marcadores de anuncio se ajustarán de nuevo después de la búsqueda. La solución es no utilizar la rellamada ITEM_UPDATED durante la búsqueda
   * Error #3779889 : La llamada completa no se realiza cuando se llega al final del truco en Video Analytics
   * Error #VA-779 - El latido de evento de cambio de velocidad de bits no se envía para la implementación de referencia de compatibilidad de vídeo mejorada con Heartbeat. La reproducción incorrecta no se implementa en la aplicación de ejemplo.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
