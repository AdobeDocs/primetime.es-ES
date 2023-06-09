---
title: Notas de la versión de TVSDK 1.4 para HLS de escritorio
description: Las notas de la versión de TVSDK para Desktop HLS describen las novedades o los cambios, los problemas resueltos y conocidos de TVSDK DHLS.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 5e227c99-acf6-4b16-a35a-68e2928fdbfd
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '5194'
ht-degree: 0%

---

# Notas de la versión de TVSDK 1.4 para HLS de escritorio {#tvsdk-for-desktop-hls-release-notes}

Las notas de la versión de TVSDK para Desktop HLS describen las novedades o los cambios, los problemas resueltos y conocidos de TVSDK DHLS.

## Nuevas funciones {#new-features}

**1.4.31**

* **Compatibilidad con varias CDN para anuncios CRS**

   * De forma predeterminada, todos los recursos transcodificados se alojarán en CDN propiedad del Adobe en Akamai. Con la última versión, el servicio de reempaquetado creativo de Adobe (CRS) permite cargar los elementos creativos transcodificados en varias CDN según especifique el cliente.
   * Se añaden nuevas API al TVSDK para permitir la especificación de la URL creativa final de CRS cuando no se utiliza la URL predeterminada. Consulte la documentación para aprender a utilizar estas nuevas API.

### Nuevas funciones en las versiones anteriores {#new-features-previous}

**1.4.30**

* **Métricas de facturación**

Para dar cabida a los clientes que desean pagar únicamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, los Adobes recopilan las métricas de uso y las utilizan para determinar cuánto facturar a los clientes.

**1.4.24**

* **Conexión de red persistente**

Importante: Debe tener instalado al menos la versión 22 o posterior del Flash Player de Adobe.
Las conexiones de red persistentes crean y almacenan una lista interna de conexiones de red que se pueden reutilizar para varias solicitudes, en lugar de abrir una nueva conexión para cada solicitud de red. Las conexiones de red persistentes deberían aumentar la eficacia y reducir la latencia del código de red.

En esta versión, esta función no es compatible con Apple Safari y Mozilla Firefox en Mac.

**1.4.19**

* Compatibilidad de integridad de flujo para anuncios VPAID.
* Se habilitó la opción de tabulación silenciosa en el reproductor de Flash FP 20.0.0.267 para Firefox 42 y posterior al corregir el problema de bloqueo.

**1.4.18**

* Primetime Desktop HLS TVSDK ahora es compatible con los creativos del SWF lineal VPAID 2.0 para permitir una experiencia de anuncio en flujo enriquecida e interactiva.

**1.4.10**

* **Reserva de anuncio, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103)** Para los anuncios VAST (creativos) con la regla de reserva habilitada, TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Anuncio alternativo para anuncios VAST y VMAP](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Biblioteca de Video Heartbeats (VHL) actualizada a la versión 1.5**

   * Capacidad para enviar metadatos con inicio de vídeo o inicio de vídeo/publicidad/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño.

**1.4.7**

* **Soporte de individualización local**

Compatibilidad con instalaciones on-premise del servidor de individualización de Adobe para personalizar la solicitud de individualización del cliente para ir a un punto final diferente.

**1.4.6**

* **Cifrado AES de muestra (requiere la versión 17.0.0.134 del Flash Player)**

Ahora se admite el cifrado AES basado en muestras.

**1.4.2**

* **Actualización de la biblioteca de Video Heartbeats (VHL) a la versión 1.4.0.1.**

   * Se ha añadido la capacidad de combinar diferentes casos de uso de análisis, de otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete. La pausa publicitaria se deduce de las llamadas a los métodos trackAdStart y trackAdComplete.
   * La propiedad cabezal de reproducción ya no es necesaria al rastrear anuncios.

**1.4.0**

* **Señalización De Interrupción Con Sustitución De Contenido Alternativo** Como parte de la actualización de TVSDK 1.4, TVSDK ahora también admite la inclusión y la devolución de interrupciones regionales en contenido lineal. El TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para monitorizar las señales de interrupción incluso cuando se muestra programación alternativa en lugar de la programación original.

* **Eliminar/reemplazar anuncios C3** Ahora, no se necesita ningún trabajo de preparación adicional para insertar dinámicamente nuevos anuncios en recursos de vídeo bajo demanda (VOD) que salen de la ventana de C3. TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar dinámicamente nuevos anuncios. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se emite durante la emisión y se extrae inmediatamente para su uso como contenido bajo demanda sin el tiempo adecuado para &quot;limpiar&quot; el recurso.

## Problemas resueltos {#resolved-issues}

>[!NOTE]
>
>Se recomienda encarecidamente a todos los clientes de TVSDK que utilicen CRS que actualicen al menos a TVSDK 1.4.32 en iOS, Android y Desktop HLS. Esta actualización sustituirá a la implementación de la aplicación existente. Después de la actualización, compruebe las solicitudes de URL creativas de CRS en una herramienta proxy (por ejemplo, Charles) para verificar que la versión de la ruta refleje la versión 3.1. Por ejemplo,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versión 1.4.41**

* #33777 de Zendesk: La versión del SWF de tokens de Localhost para la distribución DHLS ha caducado.

  Actualización del token localhost para la demostración de PMP en DHLS.

### Problemas resueltos en las versiones anteriores {#resolved-issues-previous}

**Versión 1.4.38** (891)

* Zendesk #30731 - TVSDK no reproduce varios anuncios VPAID en un AdBreak.

  Se ha corregido la reproducción de varios anuncios VPAID en un AdBreak.

* Zendesk #29968 - Cartel doble.

  El reproductor de vídeo puede repetir el último segmento de un periodo cuando se produce un cambio ABR. Debido a esto, a veces, se repite el último segmento del preroll. Esto se ha corregido.

**Versión 1.4.35** (879)

* Zendesk #26058: admite eventos VPAID nativos

**Versión 1.4.33** (873)

* Zendesk #21701: envíe la URL creativa original para la solicitud CRS 1401 en lugar de la URL normalizada.

  Se ha corregido el problema por el que se solicitaban direcciones URL ya empaquetadas para su transcodificación, según lo requerido por el back-end CRS.
* Zendesk #26197: la compresión anamórfica no se reproduce en la resolución de pantalla deseada.

  **Nota**: Este problema requiere el reproductor de Flash 24.0.0.194 o posterior.

  Se ha corregido el problema por el que se usaban entradas que faltaban en las tablas de proporción de aspecto para calcular la anchura de salida.

* Zendesk #26840: Detección de HDCP que falla en IE11 + Windows7 después de un segundo intento.

  **Nota**: Este problema requiere el reproductor de Flash 24.0.0.218 o posterior.

  Este problema se resolvió modificando el procesamiento de cola de mensajes principal de AdobeCP para iterar en toda la cola, en lugar de bloquear en el primer mensaje.

* #27460 de Zendesk: La nueva cuenta de Akamai no puede gestionar una solicitud de CDN de POST.

  La nueva cuenta de CDN no puede gestionar una solicitud de CDN de POST. Este problema se resolvió actualizando el código para que la solicitud de publicidad de cdn.auditude.com fuera GET en lugar de POST.
* Zendesk #27619: caída de Flash en Windows 10

  **Nota**: Este problema requiere el reproductor de Flash 24.0.0.218 o posterior.

  Este problema se resolvió evitando un error como resultado de direcciones URL largas.

* #28218 de Zendesk: El evento de seguimiento no se activa mientras se realiza el reenvío desde el punto de reanudación

  Este problema es el mismo que en Zendesk #26592. Se ha corregido el problema por el que se permitían las operaciones de búsqueda cuando el reproductor de medios estaba en el estado PREPARADO para flujos de VOD.

**Versión 1.4.32** (867)

* El evento #26592 Tracking de Zendesk no se activa cuando la reproducción comienza desde el punto de reanudación

El código no actualizaba el elemento de pausa del anuncio previo a la emisión cuando el punto de reanudación no era cero. Este problema se resolvió agregando lógica para actualizar el código cuando los tiempos de inicio del intervalo no coinciden.

* Zendesk #27022 Ads no se reproduce la segunda vez que se reproduce un recurso

Se han corregido las excepciones con los métodos de matriz.

**Versión 1.4.30** (855)

Los siguientes problemas se resolvieron para TVSDK en esta versión:

* Zendesk #22898 - La falta de subtítulos no debería provocar un fallo en la reproducción.

**Nota**: Este problema requiere el reproductor de Flash 23.0.0.185 o posterior.

Este problema se resolvió permitiendo que TVSDK continuara la reproducción, incluso si al manifiesto le faltaba el WebVTT M3U8, y simplemente registrara una advertencia.

* Zendesk #23454: Los anuncios de terceros (VPAID) no se gestionan correctamente

Este problema se resolvió gestionando correctamente los anuncios VPAID en función de los ID de contenido, en lugar de los intervalos de tiempo.

* Zendesk #24528 - Métricas de uso de TVSDK para facturación.

Importante: Este problema requiere el reproductor de Flash 23.0.0.185 o posterior.

* Zendesk # 25432 Problema con los subtítulos durante el cambio de tamaño del reproductor.

Importante: Este problema requiere el reproductor de Flash 23.0.0.185 o posterior.

El código del mapa de textura de visualización de rótulo se ha corregido para gestionar correctamente las coordenadas durante el cambio de tamaño del reproductor.

La biblioteca de Video Heartbeat (VHL) se ha actualizado a la versión 1.5.9 para resolver los siguientes problemas:

* #23730 de Zendesk: Las métricas de velocidad de bits están vacías

Este problema se resolvía realizando un seguimiento de los cambios en la velocidad de bits de VideoAnalyticsTracker.

* Se ha agregado una nueva API, assetDuration, a PTVideoAnalyticsTrackingMetadata para actualizar la duración de los recursos para emisiones en directo/lineales.

**Versión 1.4.28** (848)

* Zendesk #25027: Auditude no funciona en la versión de escritorio 1.4.27

Este problema se solucionó añadiendo el código para comprobar el valor de AUDITUDE_METADATA_KEY y haciendo que AUDITUDE_METADATA_KEY y ADVERTISING_METADATA_KEY sean intercambiables.

* Zendesk #24428: Problema frecuente de almacenamiento en búfer al utilizar TVSDK para reproducir un HLS de DRM

Este problema se resolvió teniendo en cuenta que, cuando no hay ninguna configuración de publicidad, TVSDK puede acelerar el procesamiento al eliminar la retención de anuncio previo a la emisión y la retención de reserva en directo en la cronología diseñada para sincronizar la inserción de publicidad.

* Zendesk #24344 - Desactivar archivos WebVTT para mejorar los tiempos de inicio.

**Nota**: este problema requiere el reproductor de Flash 23 o posterior.

Este problema se solucionaba cargando los archivos WebVTT solo cuando era necesario mostrar los subtítulos.

* Zendesk #24994: Los subtítulos opcionales se dejan al jugador cuando regresa del descanso comercial

**Nota**: este problema requiere el reproductor de Flash 23 o posterior.

El falso código EOC hizo que desapareciera la pantalla de subtítulos. Este problema se resolvió forzando los códigos de subtítulos 608 RU2, RU3 y RU4 para proporcionar la visibilidad correcta en la ventana activa actual.

**Versión 1.4.27** (844)

* Zendesk #21554: Las señalizaciones de error de TVSDK no se activan para el tipo de aplicación = video/mp4

Este problema se resolvió habilitando TVSDK para que haga ping a las direcciones URL de seguimiento de errores correctas en los formatos de recurso no válidos.

* Zendesk #23402 - Reproducción incompleta del anuncio

**Nota**: este problema requiere el reproductor de Flash 23 o posterior.

Después de obtener un error 404 en ciertas solicitudes, puede ocurrir un bloqueo. Este problema se ha resuelto asegurándose de que la conexión no se cierre mientras se gestiona la respuesta. La resolución garantiza que los archivos de anuncios VPAID no se contabilicen incorrectamente, por lo que no se liberan mientras se descargan.

* Zendesk #23621: Reintento está fallando en 400 y 404

**Nota**: este problema requiere el reproductor de Flash 23 o posterior.

Se ha corregido el problema que provocaba que se dañaran los metadatos de DRM al cambiar entre perfiles diferentes.

* Zendesk #23705 - Anuncios de vídeo congelándose durante las pausas de AdStitched

**Nota**: este problema requiere el reproductor de Flash 23 o posterior.

Este problema es el mismo que en Zendesk #23621.

* Zendesk #23905: Algunas pausas publicitarias se saltan en las pausas publicitarias

**Nota**: este problema requiere el reproductor de Flash 23 o posterior.

El código de red nativo de Windows se ha corregido para garantizar que las conexiones no cierren los identificadores que están utilizando actualmente otras conexiones.

* #24029 de tickets: los flujos FER de HLS no reproducen todos los anuncios mid-roll del archivo .json mid-roll.

Este problema se resolvió permitiendo a los clientes establecer parámetros personalizados por separado en la instancia de oportunidad para que los clientes no tengan que anular OpportunityGenerator.

**Versión 1.4.26** (839)

* Zendesk #18854: Actualice la lógica de selección creativa basada en las reglas de CRS
   * Se ha proporcionado la compatibilidad para actualizar la lógica de selección creativa basada en reglas CRS

* Implementación de Zendesk #22725 - playbackManager.beginPlayback() en la aplicación de ejemplo para escritorio

   * Se ha corregido eliminando esta llamada redundante al final de startPlaybackFromFlashVars, ya que el método se llama desde setupVideo()

* #22807 de Zendesk: excepción de referencia nula de SeekManager

   * Se corrigió al proporcionar la protección de puntero NULL necesaria dentro de SeekManager relacionada con _dispatcher

* Zendesk #22822: Almacenamiento en búfer frecuente al utilizar TVSDK para reproducir un HLS claro

   * Se corrigió eliminando la oportunidad inicial generada por adSignalingModeOpportunityGenerator si no hay anuncio

* Zendesk #23378: La integridad de la transmisión bloquea rules.xml

   * Se corrigió cargando el archivo rules.xml a través del flujo de trabajo de integridad de secuencia

**Versión 1.4.24** (817)

* Zendesk #19851: Cuando el reproductor se adapta a una velocidad de bits diferente, salta unos cuantos fotogramas en el tiempo con la nueva velocidad de bits, lo que lo convierte en una experiencia incómoda

**Nota**: Este problema requiere el reproductor de Flash 22.0.0.175 o posterior.

Se ha resuelto el problema en el cual el adaptador DRM se restablece después de descargar una pequeña fracción de un segmento no se restaura correctamente.

* Zendesk #20784 - Analytics: La activación de contenido se completa para las transiciones de vídeo en directo

Este problema se solucionó añadiendo una API (trackVideoComplete) para almacenar en déclencheur manualmente la finalización del contenido durante una sesión de seguimiento de vídeo LINEAR/LIVE.

Se han actualizado las bibliotecas siguientes:

* Zendesk #21643 - Los anuncios VPAID no se reproducen en su totalidad

   * Biblioteca de Adobe Mobile a 4.10.0
   * Biblioteca VHL a 1.5.6
   * Biblioteca VHL-Nielsen a 1.6.7

Este problema se solucionó usando una ventanilla de altura cero para rellenar el escenario cuando se estaba reproduciendo un anuncio VPAID.

* Zendesk #22110 - Analytics: Añadir una hora:sc:campo ssl para las llamadas de seguimiento de heartbeat

Los problemas relacionados con SSL se han corregido y la biblioteca VHL que se utiliza en TVSDK se ha actualizado a la última versión.

* Zendesk #22608: el vídeo muestra intermitentemente una pantalla en negro (requiere el Flash Player 22.0.0.175 o posterior)

Durante la velocidad de bits adaptable, con el límite máximo de velocidad de bits, la recarga del vídeo muestra intermitentemente una pantalla en negro, aunque el cliente vea las actualizaciones en la posición, y el cliente se comporte como si estuviera reproduciendo contenido.

**Versión 1.4.23** (809)

* #2887 de Zendesk: Problema posterior a la emisión y al omitir un anuncio cuando se aplica la lógica de reglas de publicidad al TVSDK

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Se ha corregido el problema por el cual los anuncios posteriores a la emisión se omitían cuando se aplicaba la lógica de regla de publicidad al TVSDK.

* #19863 de Zendesk: anuncio con archivo multimedia VPAID descartado

Si un anuncio en línea extenso tiene varios archivos multimedia con un anuncio VPAID que es el primer anuncio, el anuncio en línea no se reproduce para emisiones en directo. Este problema se resolvió recogiendo un archivo multimedia diferente.

* Zendesk #21021 - Audio de enlace tardío que provoca repeticiones de segmentos de audio

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Se ha corregido el problema de repetición de audio.

* Zendesk #21125 - Regreso temprano de la pausa publicitaria en vivo/lineal

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Esta versión es compatible con la devolución de una pausa publicitaria antes de que se reproduzca hasta su finalización. El retorno anticipado se indica mediante una etiqueta de manifiesto personalizada.

* Zendesk # 21369 El audio de enlace tardío causa un tiempo inconsistente

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

El problema de repetición de audio que se corrigió también ha corregido este problema.

* Zendesk #21760, 20921 - Desincronización de audio y vídeo en Seek.

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.240 o posterior.

Se ha corregido el problema de repetición de audio.

* #22024 de Zendesk: error al ejecutar el TVSDK

Se ha corregido el problema por el que el reproductor de referencia no reproducía ningún flujo y lanzaba una excepción al inicio.

**Versión 1.4.22** (791)

* Zendesk #17580: Error de tiempo de ejecución de Primetime con código 3357

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.197 o posterior.

Se han corregido los errores aleatorios 3357 que se producían al inicializar correctamente el deviceID cuando se llama a storeVoucher().

* #21334 de Zendesk: valor de tiempo de espera de solicitud de anuncio de TVSDK para solicitudes de publicidad de terceros

En esta versión, se ha añadido el tiempo de espera de solicitud de anuncio global.

**Versión 1.4.21** (782)

* Zendesk #19580 TVSDK espera a que se complete la resolución de contenido antes de enviarlo `PTTimedMetadataChangedNotification` notificaciones

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

Este problema se resolvió en el reproductor de referencia de escritorio de al proporcionar la capacidad de establecer etiquetas de publicidad y al agregar un generador de oportunidades personalizado que muestra cómo suscribirse a señales personalizadas y cómo procesarlas en un archivo VOD.

* Los anuncios mid-roll de Zendesk #20806 Future en la ventana de DVR no déclencheur después de intercambiar cámaras

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

Este problema se solucionó actualizando la aplicación para establecer _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) para deshabilitar la inserción de anuncios previos a la emisión en un intercambio de PIP y, como resultado, no se genera ninguna oportunidad previa a la emisión.

Se ha introducido una funcionalidad de ordenación para corregir la ubicación de anuncios fuera de secuencia que resultaba en una duración de contenido principal negativa.

* Zendesk #20522: No se pueden omitir los anuncios de VPAID 2.0

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

* Este problema se resolvió omitiendo los anuncios VPAID durante la cancelación del anuncio.
* Cuando la directiva de pausa publicitaria está establecida en Omitir, los eventos de pausa publicitaria y de pausa publicitaria se siguen distribuyendo. El estado del reproductor es inconsistente.

Se ha resuelto este problema para que se comporte correctamente y no distribuya eventos cuando se omita una pausa publicitaria.

* Zendesk #20955 Establecer pares de clave-valor en la propiedad customParameters a través del generador de oportunidades

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.182 o posterior.

La solicitud del Auditude analiza AuditudeSettings en busca de parámetros personalizados al crear una unidad de anuncio para solicitudes de publicidad.

Este comportamiento se ha cambiado para incluir parámetros personalizados del objeto de oportunidad en la solicitud. Además, no se pueden empaquetar varias oportunidades con diferentes parámetros personalizados en una sola solicitud de Auditude.

* Zendesk #21227 - m3u8 no puede jugar consistentemente

**Nota**: Este problema requiere el reproductor de Flash 21.0.0.211 o posterior.

Este problema se resolvió permitiendo que TVSDK ignorara el manifiesto (subperfiles HLS) que contiene el códec AC3 no compatible con TVSDK (surround).

**Versión 1.4.20** (762)

* Zendesk #19181 - Trick play fast forward to live point locks up stream.

**Nota**: Este problema requiere el reproductor de Flash 20.0.0.306 o posterior.

* Zendesk #19286 - Se produjo un accidente de Flash Player mientras buscaba hacia atrás y adelante en un flujo FER.

**Nota**: Este problema requiere el reproductor de Flash 20.0.0.306 o posterior.

Los bloqueos ocasionales que se producían al buscar en Google Chrome se resolvían cerrando las consultas, si tardaban demasiado en obtener una respuesta o si se cerraba el socket.

* Zendesk #19305: Se detecta una reproducción entrecortada al reproducir un flujo con discontinuidades A/V.

**Nota**: Este problema requiere el reproductor de Flash 20.0.0.306 o posterior.

Este problema se resolvió mediante el informe de una advertencia.

* Zendesk # 19359: el Flash Player se bloqueó debido a la posición de #EXT-X-FAXS-CM: attribute en el manifiesto de nivel de conjunto.

Este problema se resolvía cuando #EXT-X-FAXS-CM etiqueta aparecía en la lista de reproducción superior antes de la velocidad de bits individual o de los segmentos en la lista de reproducción.

* Zendesk #19489 - Fast Forward to Live Point stalls plugin (transmisión en vivo)

Este problema es el mismo que el de Zendesk #19181.

* Zendesk #19699: TVSDK no puede cambiar entre las pistas de subtítulos WebVTT

Este problema se resolvió volcando el reproductor y recargando el manifiesto cuando cambia una pista y corrigiendo el problema de conversión de cadenas UTF8 que afectaba a los nombres de pistas de subtítulos WebVTT de doble byte.

**Versión 1.4.19** (1.4.19.738)

* Zendesk #18234: El Flash Player se bloquea al reproducir los flujos con cadenas Unicode en CC

Este problema requiere el Flash Player FP 20.0.0.267 o posterior y se resolvió administrando la cadena Unicode correctamente.

* Zendesk #18304 - Soporte de integridad de transmisión para anuncios VPAID

Esta función requiere el Flash Player FP 20.0.0.267 o posterior y se introdujo en la versión 1.4.19.

* Zendesk #18766 - El reproductor de referencia no puede mostrar caracteres unicode no latinos en los nombres de las pistas CC

Esta función requiere el Flash Player FP 20.0.0.267 o posterior y se corrigió administrando correctamente la cadena Unicode.

* Zendesk #18804 - Se bloquea el reproductor en Firefox 42

Este problema requiere el Flash Player FP 20.0.0.235 o posterior y es el mismo problema que Zendesk #18723.

* Zendesk #18864 - Flash Player full plugin crash

Este problema requiere el Flash Player FP 20.0.0.235 o superior y es el mismo que Zendesk #18723.

* Zendesk #18998: Si las marcas de tiempo de audio y vídeo no coinciden, se produce una descarga interminable de segmentos en caso de discontinuidad.

Este problema se resolvió ignorando la brecha entre las marcas de tiempo y reproduciendo el contenido descargado.

* Zendesk #19093: Los anuncios mid-roll solo se pueden ver una vez con contenido de reproducción de eventos en directo y completos (FER), pero estos anuncios no se pudieron ver de nuevo cuando se reenvía rápido o se busca más allá de los anuncios

En el selector predeterminado de políticas de publicidad de Primetime, si se ve un anuncio durante la emisión, el desglose de anuncios no se mueve a la posición buscada cuando se completa una búsqueda. Para volver a reproducir el anuncio, después de la búsqueda, la aplicación debe anular la función selectAdBreaksToPlay().

* #19101 de Zendesk: al rebobinar a anuncios Midroll sin resolver, se elimina la ubicación del anuncio.

Este problema se resolvió permitiendo que el reproductor actualizara el tiempo de playbackMetrics, el minimumOpportunityTime y la Timeline.

* Zendesk #19102 - Problemas con FER y el modo truco

Este problema requiere el Flash Player FP 20.0.0.267 o posterior y se resolvió configurando advertisingMetadata.adSignalingMode correctamente.

* Zendesk #19175: A veces, los anuncios de preroll no se muestran la primera vez que se reproduce el flujo.

Este problema se resolvió agregando una nueva API, adRequestTimeout, a AuditudeSettings para un tiempo de espera de solicitud de anuncio. Los usuarios ahora pueden anular el tiempo de espera predeterminado de 10 anuncios y solicitudes.

**Versión 1.4.18** (1.4.18.722)

* Zendesk #3324: La creación de informes de anuncios de Primetime no realiza un seguimiento de las pausas publicitarias cuando no hay medios publicitarios en un VMAP.

Cuando una pausa publicitaria está vacía, los eventos de seguimiento de inicio y finalización de la pausa publicitaria no se rastreaban. Este problema se resolvió enviando pings de inicio de pausa publicitaria en pausas publicitarias vacías, como VMAP AdBreak, con un nodo de AdSource válido.

**Versión 1.4.17** (1.4.17.702)

* #17168 de Zendesk: Los subtítulos no aparecen durante 10 segundos después de alternar la visibilidad

Este problema se resolvió al proporcionar compatibilidad con la etiqueta EXT-X-MEDIA-TIME para archivos de subtítulos vtt.

* Zendesk #17983: Si no se descargan las claves de un manifiesto, la reproducción completa del manifiesto falla

**Nota**: Debe tener al menos el Flash Player FP 19.0.0.245 o superior.

A veces, al reproducir contenido en directo, puede haber claves no válidas en el manifiesto (por ejemplo, para periodos de interrupción), pero otros intervalos de tiempo pueden tener claves válidas y seguir reproduciéndose. Anteriormente, cuando una clave enumerada en un manifiesto no se podía descargar, se producía un error en todo el manifiesto. Ahora, el manifiesto falla únicamente cuando no se pueden descargar todas las claves enumeradas. Si algunas claves son válidas, pero algunas de ellas no se han podido descargar, se reproducirá el contenido. Seguiremos fallando si intentamos reproducir un segmento que requiera una clave que no tenemos.

* Zendesk #18554 - Integridad de la transmisión recortando las cookies en algunos casos

**Nota**: Debe tener al menos el Flash Player FP 19.0.0.245 o superior.

Se ha corregido un error en el código de manipulación de cookies que podría truncar los valores de las cookies.

**Versión 1.4.16** (1.4.16.684)

* Zendesk #3732: Añada compatibilidad con proxies en Chrome para la integridad del flujo (requiere Flash Player FP 19.0.0.207 o bueno)

Esto es una mejora.

* Zendesk #4244 - Problemas de transmisión en la rollover de PTS

Este problema se resolvió al detectar rollover y administrar la discontinuidad por tipo de carga útil, y no de forma genérica.

* Zendesk #4487 - Seguimiento del canal lineal de contenido

Este problema se resolvió reinicializando el rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* Zendesk #17427: La integridad de la emisión de Adobe no funciona a través de un proxy en Chrome (Win7) ()

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o bueno.

Este problema es el mismo que el de Zendesk #3732.

* Zendesk #17907 - Retraso en la transmisión en vivo de pHLS con el Flash Player 19

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o bueno.

Este problema se resolvió administrando los flujos en directo donde los dominios de los archivos TS cambian al volver a cargar el manifiesto en directo y los archivos se descargan dos veces.

* Zendesk #17931: El contenido HLS con pizarra al principio falla en la reproducción

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o bueno.

El problema se resolvió gestionando flujos sin audio en los primeros 2 segundos del primer archivo TS.

* Zendesk #17934: Error en el streaming en directo con el Flash 19.0.0.185

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o bueno.

El problema se resolvía gestionando emisiones en directo con intercalación temporal entre fotogramas de audio y vídeo en los límites de los segmentos.

* Zendesk #17973: El último Flash Player 19.0.0.185 se bloquea durante el anuncio

**Nota**: La resolución requiere el Flash Player FP 19.0.0.207 o bueno.

El problema se resolvió gestionando el audio sin mezclar con la inserción del anuncio durante la emisión. (Se produce el cambio de analizador; en cualquier momento de la reproducción, el contenido pasa al anuncio mid-roll o en mitad de la reproducción del anuncio, etc.).

* Zendesk #18049: caída del Flash 19 con Firefox 42 beta

Este problema es el mismo que el de Zendesk #17973.

**Versión 1.4.15** (1.4.15.678)

* Zendesk #4377: Activa el evento AD_BREAK_SKIPPED cuando se omite una pausa publicitaria debido a la política de publicidad.

La corrección era agregar AD_BREAK_SKIPPED si se omitía un anuncio.

* Zendesk #4496 - Integridad de la transmisión: error 102100 con redirecciones a transmisiones con token.

La corrección se realizó para agregar compatibilidad con el establecimiento de la propiedad AVNetworkConfiguration useCookieHeaderForAllRequests a través de TVSDK.

* Zendesk #17179: Reproductor de Flash que se bloquea en varios cambios de SAP para contenido cifrado.

Se corrigió un bloqueo durante la reproducción de parte del contenido cifrado.

**Nota**: la corrección requiere el Flash Player 19.0.0.200 o superior.

* Zendesk #17499: ¿cómo no eliminamos los midrolls después del reloj, sino el preroll del contenido del fer?

Se ha agregado un tipo a AdBreakTimelineItem (AdBreakTimelineItem.placementType) para que AdPolicySelector pueda devolver una política diferente para el contenido previo a la emisión, durante la emisión y después de la emisión.

* Zendesk #17665 - Aceleración del ancho de banda

La corrección consistió en quitar la lógica para cambiar el tamaño del búfer de destino al tamaño inicial del búfer cuando comienza el almacenamiento en búfer.

**Versión 1.14.14** (1.4.14.771)

* Zendesk #17363 - Corregir la documentación de README para el reproductor de referencia

   * Aclarar instrucciones para descargar e instalar playerglobal.swc.
   * Añada instrucciones para actualizar la configuración del proyecto con una versión específica de Flash Player.
   * Actualice la configuración del proyecto AdvertisingOverlay para utilizar la versión mínima del reproductor.
   * Actualizar la configuración del proyecto principal para utilizar la versión 11.9 específica del reproductor

* Zendesk #17471 - Jugador se congela

Corrección parcial de un problema en el que un anuncio no se reproduce desde el principio después de la búsqueda.

* Zendesk #17496 - Podbuster no se resuelve cuando se busca de nuevo en la ventana de DVR

Proporcione parámetros personalizados para cada pausa publicitaria.

**Versión 1.4.13** (1.4.13.660)

* Zendesk #4037: Error de perfil no utilizable (requiere el Flash Player 18.0.0.232 o bueno)

se corrigió un problema con el análisis de url cuando el parámetro de consulta contiene &quot;http&quot;

* Zendesk #4260: el Flash Player 18 se bloquea en IE11 (requiere el Flash Player 18.0.0.232 o bueno)

Se corrigió un bloqueo al reproducir vídeo en modo de pantalla completa con IE11

* Zendesk #4262: El reproductor de Adobe Primetime se bloquea en windows 10 (requiere el Flash Player 18.0.0.232 o bueno)

Se corrigió un bloqueo al reproducir vídeo en modo de pantalla completa con FireFox en Windows.

* Zendesk #4279 - Inserción de publicidad de TVSDK de HLS -302 problema de redirección en iOS y escritorio

Se ha corregido un problema por el cual una dirección URL no reconocía correctamente su tipo porque no tenía extensión

* Zendesk #4306: Se bloquea el Flash Player cuando se pasa a pantalla completa solo en Win (requiere el Flash Player 18.0.0.232 o bueno)

Se ha corregido un bloqueo al reproducir vídeo en modo de pantalla completa en Windows.

* Zendesk #4480: Faltan eventos de etiquetas ID3 (requiere el Flash Player 18.0.0.232 o bueno)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI y CRS | Mejorar: Gestionar elementos dinámicos en determinadas URL de archivos multimedia.

Se ha actualizado el servicio de reempaquetado creativo para que gestione correctamente los anuncios con direcciones URL creativas dinámicas.

* PTPLAY - 2114 - Soporte de reproducción MP4.

Ahora se admite la reproducción básica del contenido MP4, incluidas reproducción, pausa y búsqueda.

Lo siguiente requiere el Flash Player 18.0.0.225 o bueno:

* Zendesk #3992 - Velocidades adicionales de TrickPlay.

TrickPlay ahora acepta tasas superiores a 16x: +/- 32, +/-64 y +/-128.

* #3113 de Zendesk: error del complemento de Flash Player

Se ha corregido un bloqueo al intentar reproducir un anuncio de redireccionamiento en Mac Firefox.

* #4037 de Zendesk: error de perfil no utilizable
* Zendesk #4262: El reproductor de Adobe Primetime se bloquea en Windows 10

Se corrigió un error en Windows Firefox durante la reproducción a pantalla completa.

**Versión 1.4.11** (1.4.11.648)

* Zendesk #1869 - Cambio de tamaño de fuente de problema (requiere el Flash Player 18.0.0.200)

Permitir el uso de tamaños de rótulo en el código de rótulo WebVTT.

* Zendesk #3113 - Flash Player Plugin Crashing (requiere Flash Player 18.0.0.200)
* Zendesk #3268 - Escritorio: El reproductor de vídeo comienza a parpadear después de +- 40/50 segundos y comienza a oscurecer después de +- 90 segundos (requiere Flash Player 18.0.0.200)

Se ha corregido un error de vídeo de fase.

* Error de Zendesk #3670 - INVALID_PARAMETER en VOD al buscar en el reproductor de referencia (requiere Flash Player 18.0.0.200)

InvalidateProfiles en ThreadSeek cuando se detecta un nuevo período.

* Zendesk #3896: Bloqueo de Flash Player con Stream Integrity establecido en ON en Chrome (requiere Flash Player 18.0.0.200)

Se corrigió un bloqueo en el modo de red nativa en pepper

* Zendesk #3905: El reproductor de TVSDK no se carga cuando se aloja en CDN

Se han corregido problemas al buscar el token comodín cuando pageDomain es diferente del dominio swf.

**Versión 1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player bloquea el Flash en Firefox

Se ha corregido un bloqueo ocasional de Flash Player con Firefox en Mac cuando un flujo, que se reproducía en un monitor externo, cambiaba a un flujo de velocidad de bits más alto.(requiere el Flash Player 18.0.0.160)

* Zendesk #3268 - Escritorio: El reproductor de vídeo comienza a parpadear después de `+-` 40/50 segundos y empieza a oscurecer después `+-` 90 segundos

Se ha corregido un problema en Mac Chrome por el cual el flujo empezaba a parpadear y, finalmente, se volvía negro. (requiere el Flash Player 18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` la macro no se rellena

   * el código de error 400 se expone si el anuncio en línea tiene un error creativo.
   * `[ERRORCODE]` La macro tendrá codificación URL

* Zendesk #3601 - Solicitud de mejora: Gestión de complemento de envoltorio

   * TVSDK mostrará los contenedores complementarios que contienen recursos (html, iframe o estático ) cerca de la línea. ( si la línea no contiene una para ese tamaño)
   * Los envoltorios acompañantes con el recurso, a menos que se utilice para la visualización, se ignorarán. (no se usa para el seguimiento )
   * Solo se utilizarán los compañeros de envoltorio sin recurso para realizar el seguimiento. ( complemento de envoltorio que solo contiene seguimiento )

**Versión 1.4.9**

* Zendesk #2615: problema al eliminar la vista HLS de la pantalla de escritorio

Se ha agregado el método clearVideo() a MediaPlayer. Borra el fotograma de vídeo mostrado borrando AVStream del objeto StageVideo. Solo debe invocarse si el vídeo está en pausa y debe llamarse a replaceCurrentResource o replaceCurrentItem antes de volver a llamar a play().

* Zendesk #3169: Actualización del reproductor de referencia con la integración de Adobe Analytics

El reproductor de referencia se ha actualizado con la integración de Adobe Analytics

* Zendesk #3296 - TVSDK de HLS de escritorio - No se reproducen los anuncios de terceros de VAST

Los tipos MIME para el formato HLS distinguían entre mayúsculas y minúsculas, esto era incorrecto y se ha cambiado para que ya no distingan entre mayúsculas y minúsculas

**Versión 1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000 (requiere el Flash Player 17.0.0.184)
* Zendesk #3007: Los anuncios previos a la emisión no aparecen después de actualizar al Flash Player 17 (requiere el Flash Player 17.0.0.184)
* Zendesk #3085 - Desktop HLS Player genera 106000 error después de 60 segundos (requiere el Flash Player 17.0.0.184)

**Versión 1.4.7**

* #2760 de Zendesk: etiqueta DISCONTINUITY ignorada durante el modo TrickPlay (requiere la versión de Flash Player 17.0.0.158)
* #2760 de Zendesk: etiqueta DISCONTINUITY ignorada durante el modo TrickPlay (requiere la versión de Flash Player 17.0.0.158)

**Versión 1.4.6**

* Zendesk #2652: Documentación del Auditude para HLS de escritorio, Auditude aclarado media_id para HLS de escritorio

**Versión 1.4.5**

* Zendesk #2256: acceso a la lista de reproducción maestra, PSDK actualizado para enviar eventos de metadatos cronometrados para las etiquetas suscritas en la lista de reproducción maestra. (requiere la versión de Flash Player 17.0.0.134)
* Zendesk #2417: El reproductor intentaba descargar subtítulos antes de que comenzara la reproducción; WebVTT usaba la variable de número de segmento incorrecta para la coincidencia de número de segmento. El error solo aparecía en los medios que tenían índices de segmento a partir de cero. (requiere la versión de Flash Player 17.0.0.134)
* Zendesk #2537: El reproductor de Flash se bloquea al usar el complemento de pimienta con Chrome (requiere la versión de Flash Player 17.0.0.134)
* Zendesk #2547 - Subtítulos en árabe: El texto debe estar alineado a la derecha (requiere la versión de Flash Player 17.0.0.134)

**Versión 1.4.4**

* Zendesk #1561 - Re: `[Adobe Primetime]` Actualización: compatibilidad de conmutación por error basada en cliente HLS para PROGRAM-DATE-TIME en PSDK de escritorio (requiere la versión de Flash Player 16.0.0.305 o buena)
* Zendesk #2197 - `[Ads]` Seguimiento de errores de publicidad
* Zendesk #2286 - Solicitud de funcionalidad: Proporcione información sobre el estado de carga del anuncio (VPAID)
* Zendesk #2285 - Solicitud de característica: Omitir anuncio después de una duración de tiempo de espera especificada
* Error #3921755: actualización de la biblioteca OpenSSL a la versión 1.0.1L en Flash Player (requiere la versión de Flash Player 16.0.0.305 o buena)

**Versión 1.4.2**

* Zendesk #1303 - Desplazamiento vertical para subtítulos (requiere la versión de Flash Player 16.0.0.235 o buena, fecha prevista de lanzamiento: diciembre de 2014)
* Zendesk #1870 - Subtítulos Encendidos y Apagados (requiere la versión de Flash Player 16.0.0.235 o buena, fecha prevista de lanzamiento: diciembre de 2014)
* Zendesk #2110: La reproducción se atasca después de intentar entrar a pantalla completa durante un anuncio VPAID (requiere la versión de Flash Player 16.0.0.235 o buena, fecha de lanzamiento prevista: diciembre de 2014)
* Zendesk #2199 - `[VPAID]` El reproductor no responde al buscar una pausa publicitaria pasada
* Zendesk #2358 - Re: `[Analytics]` Datos de capítulo incorrectos

**Versión 1.4.1**

* Se ha actualizado la API de bloqueos para que sea coherente con la implementación de Android y iOS.

**Versión 1.4.0**

* Zendesk #1024: función para eliminar el anuncio del flujo a través del manifiesto
* Zendesk #1423 - El fallo de reproducción de HLS está bloqueando el Flash Player (sin que se informe de ningún error)
* Zendesk #1674 - ClosedCaption No aparece, pantalla correcta de 708 subtítulos cuando faltan 0x03 códigos ETX.

## Problemas conocidos {#known-issues}

* Subtítulos no funcionará con contenido de solo audio porque el sistema de subtítulos necesita vídeo para funcionar.
Sin vídeo, no hay ninguna dimensión de ventanilla móvil y, sin ella, no se puede mostrar ningún gráfico para los subtítulos.
* La integridad de la emisión es ligeramente más lenta en Google Chrome debido a las restricciones de la zona protegida de Chrome.
* En TVSDK 1.4, si desactiva la reproducción automática, puede producirse un error de DRM cuando el reproductor permanece inactivo durante al menos un minuto. Para solucionar este problema, cuando deshabilita la reproducción automática pero precarga recursos, modifique `ReferenceCore.as` al cambiar el contenido de `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versión 1.4.13** PTPLAY-8501: cuando VMAP devuelve dos anuncios MP4 directos no transcodificados, el mismo anuncio de reserva se reproduce dos veces.

* **Versión 1.4.2** En la versión de Flash Player 16, se identificó un problema con la lógica de &quot;cambio descendente&quot; de ABR, después de que el reproductor entra en un evento de almacenamiento en búfer vacío. El problema evita que la velocidad de bits se desactive en entornos de ancho de banda incorrecto una vez que el reproductor entra en un estado de almacenamiento en búfer. Para solucionar el problema, haga que la aplicación configure el `BufferControlParameters.initialBufferTime` para que sea igual que `BufferControlParameters.playbackBufferTime` temporalmente durante el estado de almacenamiento en búfer (es decir, en un `BufferEvent.BUFFERING_BEGIN` ) y, a continuación, vuelva a los valores establecidos en `BufferEvent.BUFFERING_END` evento. La corrección de este problema estará disponible en la próxima versión del parche de la versión 16 del Flash Player.

* **Versión 1.4.0**

   * PTPLAY-1634: la misma etiqueta suscrita tiene diferentes marcas de tiempo en diferentes ventanas activas. Cuando las ventanas activas se mueven, la misma etiqueta de cada una de ellas debe tener las mismas marcas de tiempo. Sin embargo, a veces, las mismas etiquetas tienen marcas de tiempo diferentes.
   * PTPLAY-28: la cronología de MediaPlayer no incluye pausas vacías.
   * Se requiere un archivo de directiva entre dominios (cross-domain.xml) para poder transmitir contenido desde un dominio diferente. [Configuración de un archivo cross-domain.xml para flujo HTTP](https://helpx.adobe.com/adobe-media-server/dev/configure-dynamic-streaming-live-streaming.html).
   * #3694203 de errores: En un flujo de DVR, la búsqueda desde dentro de un mid-roll que se reproduce en otro anuncio mid-roll puede provocar la congelación del explorador
   * Error #3753725: selectPolicyForSeekIntoAd no tiene en cuenta si se ha visto la pausa publicitaria
   * #3754529 de errores: Los anuncios previos a la emisión no se eliminan del flujo al buscar de nuevo en un flujo de DVR en directo
   * Error #3761896: si se permite la búsqueda durante la reproducción del anuncio, los marcadores de publicidad se reajustarán después de la búsqueda. La solución consiste en no utilizar la llamada de retorno ITEM_UPDATED durante la búsqueda
   * #3779889 de errores: La llamada completa no se realiza al llegar al final del juego de trucos en Video Analytics
   * #VA-779 de errores: El latido del evento de cambio de velocidad de bits no se envía para el análisis de vídeo mejorado con implementación de referencia de compatibilidad con Heartbeat. El juego de trucos no se implementa en la aplicación de ejemplo.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
