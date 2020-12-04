---
title: Notas de la versión de TVSDK 1.4 for Desktop HLS
seo-title: Notas de la versión de TVSDK 1.4 for Desktop HLS
description: Las notas de la versión de TVSDK for Desktop HLS describen las novedades o los cambios, los problemas resueltos y conocidos de TVSDK DHLS.
seo-description: Las notas de la versión de TVSDK for Desktop HLS describen las novedades o los cambios, los problemas resueltos y conocidos de TVSDK DHLS.
uuid: 84da27b7-299b-478d-88f5-ef943f0a8321
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: e4437a26-9454-4da1-ae87-0fce664aac3d
translation-type: tm+mt
source-git-commit: ba291a4615a8e0713cf610f76f41e328da96ec4d
workflow-type: tm+mt
source-wordcount: '5222'
ht-degree: 0%

---


# Notas de la versión de TVSDK 1.4 para HLS de escritorio {#tvsdk-for-desktop-hls-release-notes}

Las notas de la versión de TVSDK for Desktop HLS describen las novedades o los cambios, los problemas resueltos y conocidos de TVSDK DHLS.

## Nuevas funciones {#new-features}

**1.4.31**

* **Compatibilidad con múltiples CDN para anuncios CRS**

   * De forma predeterminada, todos los recursos transcodificados se alojarán en CDN propiedad de Adobe en Akamai. Con la última versión, el servicio de reempaquetado creativo de Adobe (CRS) permite cargar los elementos creativos transcodificados en varios CDN, según lo especificado por el cliente.
   * Se añaden nuevas API al SDK de TVSDK para permitir la especificación de la URL creativa de CRS final cuando no se utiliza la URL predeterminada. Consulte la documentación para aprender a utilizar estas nuevas API.

### Nuevas funciones de las versiones anteriores {#new-features-previous}

**1.4.30**

* **Métricas de facturación**

Para dar cabida a los clientes que desean pagar solamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.

**1.4.24**

* **Conexión de red persistente**

Importante: Debe tener instalado al menos Adobe Flash Player versión 22 o posterior.
Las conexiones de red persistentes crean y almacenan una lista interna de conexiones de red que se puede reutilizar para varias solicitudes, en lugar de abrir una nueva conexión para cada solicitud de red. Las conexiones de red persistentes deberían aumentar la eficiencia y reducir la latencia del código de red.

En esta versión, esta función no se admite en Apple Safari ni Mozilla Firefox en Mac.

**1.4.19**

* Compatibilidad con integridad de flujo para anuncios VPAID.
* Se habilitó la opción de tabulación silenciar en el reproductor de Flash FP 20.0.0.267 para Firefox 42 y versiones posteriores corrigiendo el problema de bloqueo.

**1.4.18**

* El SDK de TVSDK de Primetime Desktop ahora admite elementos creativos de SWF lineales de VPAID 2.0 para permitir una experiencia de publicidad interactiva y enriquecida en flujo.

**1.4.10**

* **Ad Fallback, Daisy encadenado en la lógica de selección de anuncios (Zendesk #3103)** Para anuncios VAST (elementos creativos) con la regla de reserva activada, el TVSDK trata una publicidad con un tipo MIME no válido como una publicidad vacía e intenta usar anuncios alternativos en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Retorno de anuncios para anuncios VAST y VMAP](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Video Heartbeat Library (VHL) actualizado a la versión 1.5**

   * Capacidad para enviar metadatos con inicio de vídeo y/o inicio de vídeo/anuncio/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño.

**1.4.7**

* **Asistencia para la individualización in situ**

Compatibilidad con instalaciones in situ del servidor de individualización de Adobe para personalizar la solicitud de individualización del cliente para ir a otro extremo.

**1.4.6**

* **Cifrado AES de muestra (requiere la versión 17.0.0.134 de Flash Player)**

Ahora se admite el cifrado AES basado en muestras.

**1.4.2**

* **Actualización de Video Heartbeat Library (VHL) a la versión 1.4.0.1**

   * Se añadió la capacidad de compilar diferentes casos de uso de análisis, desde otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete. La pausa publicitaria se deduce de las llamadas a los métodos trackAdStart y trackAdComplete.
   * La propiedad playhead ya no es necesaria al rastrear anuncios.

**1.4.0**

* **Señalización de interrupción con** sustitución de contenido alternativoComo parte de la actualización 1.4 del TVSDK, el TVSDK ahora también admite entrar y volver de los bloqueos regionales contra contenido lineal. TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de interrupción incluso cuando se muestra una programación alternativa en lugar de la programación original.

* **Eliminar o reemplazar** publicidades de C3 Ahora, no se necesita ningún trabajo previo adicional para insertar dinámicamente nuevas publicidades en recursos de vídeo a petición (VOD) que salen de la ventana de C3. TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar publicidades nuevas de forma dinámica. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se transmite durante la retransmisión y se baja inmediatamente para utilizarlo como contenido a petición sin tiempo suficiente para &quot;limpiar&quot; el recurso.

## Problemas resueltos {#resolved-issues}

>[!NOTE]
>
>Se recomienda encarecidamente a todos los clientes de TVSDK que utilicen CRS que actualicen al menos a TVSDK 1.4.32 en iOS, Android y HLS de escritorio. Esta actualización sustituirá a la implementación de la aplicación existente. Después de la actualización, compruebe las solicitudes de URL creativa de CRS en una herramienta proxy (por ejemplo, Charles) para comprobar que la versión de la ruta refleja la versión 3.1. Por ejemplo,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versión 1.4.41**

* Zendesk #33777 - FRS de token de host local para la compilación de distribución DHLS caducó.

   Actualización del token de localhost para la demostración de PMP en DHLS.

### Problemas resueltos en las versiones anteriores {#resolved-issues-previous}

**Versión 1.4.38** (891)

* Zendesk #30731 - TVSDK no reproduce varias publicidades VPAID en un AdBreak.

   Se corrigió la reproducción de varias publicidades VPAID en un AdBreak.

* Zendesk #29968 - Cartel de Doble.

   El reproductor de vídeo puede repetir el último segmento de un período en el que se produce un cambio de ABR. Debido a esto, a veces, el último segmento de predesplazamiento se repite. Esto se ha solucionado.

**Versión 1.4.35** (879)

* Zendesk #26058 - Admite eventos VPAID nativos

**Versión 1.4.33** (873)

* Zendesk #21701 - Envíe la URL creativa original para la solicitud de CRS 1401 en lugar de la URL normalizada.

   Se ha solucionado el problema por el que se solicitaban direcciones URL ya reempaquetadas para la transcodificación, según lo requerido por el servidor CRS.
* Zendesk #26197 - La compresión anamórfica no se reproduce en la resolución de visualización deseada.

   **Nota**: Este problema requiere Flash Player 24.0.0.194 o posterior.

   Se ha solucionado el problema por el que se utilizaban entradas que faltaban en las tablas de proporción de aspecto para calcular el ancho de salida.

* Zendesk #26840: error de detección de HDCP en IE11 + Windows7 tras un segundo intento.

   **Nota**: Este problema requiere Flash Player 24.0.0.218 o posterior.

   Este problema se resolvió modificando el procesamiento de la cola de mensajes principal de AdobeCP para iterar en toda la cola, en lugar de simplemente bloquear el primer mensaje.

* Zendesk #27460 - La nueva cuenta de Akamai no puede gestionar una solicitud de CDN POST.

   La nueva cuenta de CDN no puede gestionar una solicitud de CDN POST. Este problema se resolvió actualizando el código para que la solicitud de publicidad cdn.auditude.com fuera GET en lugar de POST.
* Zendesk #27619 - Flash bloqueado en Windows 10

   **Nota**: Este problema requiere Flash Player 24.0.0.218 o posterior.

   Este problema se resolvió evitando un error como resultado de direcciones URL largas.

* Zendesk #28218 - El evento de seguimiento no se activa mientras el retroceso se produce desde el punto de reanudación

   Este problema es el mismo problema que en Zendesk #26592. Se ha solucionado el problema por el que se permitían las operaciones de búsqueda cuando el reproductor de medios está en el estado PREPARADO para los flujos de VOD.

**Versión 1.4.32** (867)

* El evento de seguimiento Zendesk #26592 no se activa cuando la reproducción se inicio desde el punto de reanudación

El código no actualizaba el elemento de pausa publicitaria previa cuando el punto de reanudación no era cero. Este problema se resolvió añadiendo lógica para actualizar el código cuando los tiempos de inicio del intervalo no coinciden.

* Zendesk #27022 Las publicidades no se reproducen la segunda vez que se reproduce un recurso

Las excepciones con los métodos de matriz se han corregido.

**Versión 1.4.30** (855)

En esta versión se han solucionado los siguientes problemas de TVSDK:

* Zendesk #22898 - Los subtítulos que faltan no deberían provocar errores en la reproducción.

**Nota**: Este problema requiere Flash Player 23.0.0.185 o posterior.

Este problema se resolvió permitiendo que TVSDK continuara la reproducción, incluso si al manifiesto le falta WebVTT M3U8 y solo tiene que registrar una advertencia.

* Zendesk #23454 - Los anuncios de terceros (VPAID) no se gestionan correctamente

Este problema se resolvió administrando correctamente las publicidades VPAID en función de los ID de contenido en lugar de los intervalos de tiempo.

* Zendesk #24528 - Métricas de uso de TVSDK para facturación.

Importante: Este problema requiere Flash Player 23.0.0.185 o posterior.

* Problema con los subtítulos opcionales Zendesk # 25432 durante el cambio de tamaño del reproductor.

Importante: Este problema requiere Flash Player 23.0.0.185 o posterior.

El código del mapa de textura de visualización del rótulo se ha corregido para gestionar correctamente las coordenadas durante el cambio de tamaño del reproductor.

Video Heartbeat Library (VHL) se ha actualizado a la versión 1.5.9 para resolver los siguientes problemas:

* Zendesk #23730 - Las métricas de velocidad de bits están vacías

Este problema se resolvió mediante el seguimiento de los cambios de velocidad de bits en VideoAnalyticsTracker.

* Se ha añadido una nueva API, assetDuration, a PTVideoAnalyticsTrackingMetadata para actualizar la duración de los recursos para flujos interactivos/lineales.

**Versión 1.4.28** (848)

* Zendesk #25027 - Auditude no funciona en la versión de escritorio 1.4.27

Este problema se resolvió agregando el código para comprobar el valor AUDITUDE_METADATA_KEY y haciendo que AUDITUDE_METADATA_KEY y ADVERTISING_METADATA_KEY sean intercambiables.

* Zendesk #24428 - Problema frecuente de almacenamiento en búfer con TVSDK para reproducir un DRM HLS

Este problema se resolvió teniendo en cuenta que cuando no hay configuración de publicidad, TVSDK puede acelerar el procesamiento eliminando la retención previa de anuncios y la retención de reservas activas en la línea de tiempo diseñada para sincronizar la inserción de anuncios.

* Zendesk #24344 - Desactive los archivos WebVTT para mejorar los tiempos de inicio.

**Nota**: Este problema requiere Flash Player 23 o posterior.

Este problema se resolvió cargando los archivos WebVTT solo cuando es necesario mostrar los rótulos.

* Zendesk #24994 - Los subtítulos optativos se retiran del reproductor al volver de la pausa comercial

**Nota**: Este problema requiere Flash Player 23 o posterior.

El espurio código EOC causó que la visualización del rótulo desapareciera. Este problema se resolvió obligando a los códigos RU2, RU3 y RU4 de 608 rótulos a proporcionar la visibilidad correcta en la ventana activa actual.

**Versión 1.4.27** (844)

* Zendesk #21554 - Las señalizaciones de error de TVSDK no se activan para el tipo de aplicación = vídeo/mp4

Este problema se resolvió habilitando TVSDK para hacer ping a las direcciones URL de seguimiento de errores correctas en formatos de recurso no válidos.

* Zendesk #23402 - Reproducción publicitaria incompleta

**Nota**: Este problema requiere Flash Player 23 o posterior.

Después de obtener un error 404 en determinadas solicitudes, puede producirse un bloqueo. Este problema se ha resuelto asegurándose de que la conexión no se apague mientras se gestiona la respuesta. La resolución garantiza que los archivos de publicidad VPAID no se contabilicen incorrectamente, por lo que no se lanzarán mientras se descargan.

* Zendesk #23621 - Retry está fallando en 400 y 404

**Nota**: Este problema requiere Flash Player 23 o posterior.

Se ha corregido el problema que provocaba la corrupción de los metadatos DRM al cambiar de un perfil a otro.

* Zendesk #23705 - Anuncios de vídeo congelados durante los descansos con título publicitario

**Nota**: Este problema requiere Flash Player 23 o posterior.

Este problema es el mismo que en Zendesk #23621.

* Zendesk #23905 - Algunos saltos de publicidad se saltan en los saltos de publicidad

**Nota**: Este problema requiere Flash Player 23 o posterior.

El código de red nativo de Windows se ha corregido para garantizar que las conexiones no cierren los controladores que están siendo utilizados por otras conexiones.

* ticket #24029 - Los flujos HLS FER no reproducen todos los anuncios intermedios en el archivo .json mid-roll.

Este problema se resolvió permitiendo que los clientes establecieran parámetros personalizados por separado en la instancia de Oportunidad para que los clientes no tuvieran que anular OpportunityGenerator.

**Versión 1.4.26** (839)

* Zendesk #18854 - Actualización de la lógica de selección creativa basada en las reglas de CRS
   * Se ha proporcionado compatibilidad para actualizar la lógica de selección creativa en función de las reglas de CRS

* Zendesk #22725 - implementación de playbackManager.beginPlayback() en la aplicación de ejemplo para escritorio

   * Se corrigió eliminando esta llamada redundante al final de startPlaybackFromFlashVars, ya que se llama al método desde setupVideo()

* Zendesk #22807 - Excepción de referencia nula de SeekManager

   * Se corrigió proporcionando la protección de puntero NULL necesaria dentro de SeekManager en relación con _dispatcher

* Zendesk #22822: Almacenamiento en búfer frecuente al utilizar TVSDK para reproducir un HLS claro

   * Se corrigió eliminando la oportunidad inicial generada por adSignalingModeOpportunityGenerator si no hay publicidad

* Zendesk #23378 - La integridad del flujo bloquea rules.xml

   * Se ha corregido cargando el archivo rules.xml a través del flujo de trabajo de integridad de flujo

**Versión 1.4.24** (817)

* Zendesk #19851 - Cuando el reproductor se adapta a una velocidad de bits diferente, salta unos pocos fotogramas en el tiempo con la nueva velocidad de bits, lo que hace que la experiencia sea incómoda

**Nota**: Este problema requiere Flash Player 22.0.0.175 o posterior.

Se ha solucionado el problema por el que el adaptador de DRM se restablecía después de descargar una pequeña fracción de un segmento no se restauraba correctamente.

* Zendesk #20784 - Análisis: Se completa el contenido de activación para transiciones de vídeo en directo

Este problema se resolvió agregando una API (trackVideoComplete) para activar manualmente la finalización de contenido durante una sesión de seguimiento de vídeo LINEAR/LIVE.

Se han actualizado las bibliotecas siguientes:

* Zendesk #21643 - Los anuncios VPAID no se reproducen en su totalidad

   * Biblioteca de AdobeMobile a 4.10.0
   * Biblioteca VHL a 1.5.6
   * Biblioteca VHL-Nielsen a 1.6.7

Este problema se resolvió usando una ventanilla de altura cero para completar el escenario cuando se reprodujo un anuncio VPAID.

* Zendesk #22110 - Análisis: Añadir un campo h:sc:ssl en las llamadas de seguimiento de Heartbeat

Se han solucionado los problemas relacionados con SSL y la biblioteca VHL que se utiliza en TVSDK se ha actualizado a la versión más reciente.

* Zendesk #22608 - El vídeo muestra de forma intermitente una pantalla negra (requiere Flash Player 22.0.0.175 o posterior)

Durante la velocidad de bits adaptable, con el límite máximo de velocidad de bits, la recarga del vídeo muestra de forma intermitente una pantalla negra aunque el cliente vea actualizaciones en su posición y se comporta como si estuviera reproduciendo contenido.

**Versión 1.4.23** (809)

* Zendesk #2887 - Problema de omitir anuncio posterior cuando se aplicó la lógica de regla de publicidad al TVSDK

**Nota**: Este problema requiere Flash Player 21.0.0.240 o posterior.

Se ha solucionado el problema por el que las publicidades posteriores se omitían cuando se aplicaba la lógica de regla de publicidad al TVSDK.

* Zendesk #19863 - Anuncio con archivo de medios VPAID descartado

Si un anuncio en línea amplio tiene varios archivos de medios con un anuncio VPAID como primer anuncio, el anuncio en línea no se reproduce para los flujos en vivo. Este problema se resolvió seleccionando un archivo de medios diferente en su lugar.

* Zendesk #21021 - Repetición de audio de enlace tardío

**Nota**: Este problema requiere Flash Player 21.0.0.240 o posterior.

Se ha solucionado el problema de repetición de audio.

* Zendesk #21125 - Retorno de la pausa publicitaria en directo/lineal antes de la hora prevista

**Nota**: Este problema requiere Flash Player 21.0.0.240 o posterior.

Esta versión permite volver de una pausa publicitaria antes de que se reproduzca la pausa publicitaria hasta que finalice. La devolución anticipada se indica mediante una etiqueta de manifiesto personalizada.

* Zendesk # 21369 El enlace tardío del audio causa un tiempo incoherente

**Nota**: Este problema requiere Flash Player 21.0.0.240 o posterior.

El problema de repetición de audio que se ha solucionado también se ha corregido.

* Zendesk #21760, 20921 - Audio Video Desync on Seek.

**Nota**: Este problema requiere Flash Player 21.0.0.240 o posterior.

Se ha solucionado el problema de repetición de audio.

* Zendesk #22024 - Error al ejecutar el TVSDK

Se ha solucionado el problema por el que el reproductor de referencia no reproducía ningún flujo y hacía una excepción en el inicio.

**Versión 1.4.22** (791)

* Zendesk #17580 - Error de tiempo de ejecución de Primetime con código 3357

**Nota**: Este problema requiere Flash Player 21.0.0.197 o posterior.

Se han corregido los errores aleatorios 3357 que se producían al inicializar correctamente el deviceID al llamar a storeVoucher().

* Zendesk #21334 - Valor de tiempo de espera de solicitud de publicidad TVSDK para solicitudes de publicidad de terceros

En esta versión, se ha agregado el tiempo de espera de solicitud de publicidad global.

**Versión 1.4.21** (782)

* Zendesk #19580 TVSDK espera la finalización de la resolución de contenido antes de enviar notificaciones `PTTimedMetadataChangedNotification`

**Nota**: Este problema requiere Flash Player 21.0.0.182 o posterior.

Este problema se resolvió en Desktop Reference Player al proporcionar la capacidad de establecer etiquetas de publicidad y agregar un generador de oportunidades personalizado que muestre cómo suscribirse a las indicaciones personalizadas y cómo procesar estas señales en un archivo VOD.

* Zendesk #20806 Los futuros anuncios intermedios en la ventana de DVR no se activarán después de intercambiar cámaras

**Nota**: Este problema requiere Flash Player 21.0.0.182 o posterior.

Este problema se resolvió actualizando la aplicación para establecer _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) para deshabilitar la inserción de anuncios previos en un intercambio PIP y, como resultado, no se genera ninguna oportunidad previa al lanzamiento.

Se introdujo una funcionalidad de clasificación para corregir la colocación de anuncios fuera de secuencia que resultó en una duración de contenido principal negativa.

* Zendesk #20522: No se pueden omitir las publicidades de VPAID 2.0

**Nota**: Este problema requiere Flash Player 21.0.0.182 o posterior.

* Este problema se resolvió omitiendo las publicidades VPAID durante el perdón de anuncios.
* Cuando la directiva de salto de página está configurada para omitir, los eventos de pausa publicitaria y publicitaria aún se envían. El estado del reproductor es incoherente.

Este problema se resolvió para comportarse correctamente y no distribuir eventos cuando se omitía la pausa publicitaria.

* Zendesk #20955 Establezca pares de clave-valor en la propiedad customParameters mediante el generador de oportunidades

**Nota**: Este problema requiere Flash Player 21.0.0.182 o posterior.

La solicitud de audiencia analiza AuditudeSettings en busca de parámetros personalizados al crear una unidad de publicidad para solicitudes de publicidad.

Este comportamiento se cambió para incluir parámetros personalizados del objeto Oportunidad en la solicitud. Además, no se pueden empaquetar varias oportunidades con parámetros personalizados diferentes en una sola solicitud de Auditude.

* Zendesk #21227 - m3u8 no juega de manera consistente

**Nota**: Este problema requiere Flash Player 21.0.0.211 o posterior.

Este problema se resolvió permitiendo que el TVSDK omitiera el manifiesto (subperfiles HLS) que contiene el códec AC3 que el TVSDK no admite (surround).

**Versión 1.4.20** (762)

* Zendesk #19181 - Los trucos juegan rápido hacia adelante hasta que el punto de vida se bloquee el flujo.

**Nota**: Este problema requiere Flash Player 20.0.0.306 o posterior.

* Zendesk #19286 - Se produjo un accidente de Flash Player al buscar hacia atrás y adelante en un flujo FER.

**Nota**: Este problema requiere Flash Player 20.0.0.306 o posterior.

Los bloqueos ocasionales que se producían al buscar en Google Chrome se resolvían cerrando las consultas, si las consultas tardaban demasiado en obtener una respuesta o si el socket se estaba apagando.

* Zendesk #19305: Reproducción de disquete encontrada al reproducir un flujo con discontinuidades A/V.

**Nota**: Este problema requiere Flash Player 20.0.0.306 o posterior.

Este problema se resolvió mediante un sistema de informes de advertencia.

* Zendesk # 19359 - Flash Player bloqueado debido a la posición de #EXT-X-FAXS-CM: en el manifiesto de nivel de conjunto.

Este problema se resolvió cuando la etiqueta #EXT-X-FAXS-CM aparece en la lista de reproducción superior antes de la velocidad de bits individual o los segmentos en la lista de reproducción.

* Zendesk #19489 - Fast Forward to Live Point stalls plugin (flujo en vivo)

Este problema es el mismo que Zendesk #19181.

* Zendesk #19699 - TVSDK no puede cambiar entre las pistas de subtítulos WebVTT

Este problema se resolvió haciendo que el volcado del reproductor volviera a cargar el manifiesto cuando cambiaba un seguimiento y corrigiendo el problema de conversión de cadena UTF8 que afectaba a los nombres de seguimiento de subtítulos WebVTT de byte doble.

**Versión 1.4.19** (1.4.19.738)

* Zendesk #18234 - Flash Player se bloquea al reproducir los flujos con cadenas Unicode en CC

Este problema requiere Flash Player FP 20.0.0.267 o posterior y se resolvió administrando la cadena Unicode correctamente.

* Zendesk #18304 - Compatibilidad de integridad de flujo para anuncios VPAID

Esta función requiere Flash Player FP 20.0.0.267 o posterior y se introdujo en la versión 1.4.19.

* Zendesk #18766 - El reproductor de referencia no puede mostrar caracteres Unicode no latinos en los nombres de pistas CC

Esta función requiere Flash Player FP 20.0.0.267 o posterior y se ha corregido administrando correctamente la cadena Unicode.

* Zendesk #18804 - El reproductor se bloquea en Firefox 42

Este problema requiere el Flash Player FP 20.0.0.235 o posterior y es el mismo problema que Zendesk #18723.

* Zendesk #18864 - Bloqueo de plugin completo de Flash Player

Este problema requiere el Flash Player FP 20.0.0.235 o superior y es el mismo que Zendesk #18723.

* Zendesk #18998 - Si las marcas de tiempo de audio y vídeo no coinciden, se produjo una descarga interminable de segmentos en caso de discontinuidad.

Este problema se resolvió ignorando el espacio entre las marcas de hora y solo reproduciendo el contenido descargado.

* Zendesk #19093 - Los anuncios de versión intermedia solo se pueden ver una vez con contenido de reproducción en directo y en evento completo (FER), pero estos anuncios no se pueden volver a ver cuando se reenvían rápidamente o se buscan más allá de los anuncios

En el selector de adPolicy predeterminado de Primetime, si se observa un anuncio intermedio, el adBreak no se mueve a la posición de búsqueda cuando se completa una búsqueda. Para volver a reproducir el anuncio, después de la búsqueda, la aplicación debe anular la función selectAdBreaksToPlay().

* Zendesk #19101 - Si se rebobina en publicidades Midroll sin resolver, se elimina la colocación de la publicidad.

Este problema se resolvió permitiendo que el reproductor actualizara la hora de las métricas de reproducción, la hora mínima de oportunidad y la línea de tiempo.

* Zendesk #19102 - Problemas con el modo FER y truco

Este problema requiere Flash Player FP 20.0.0.267 o posterior y se resolvió configurando correctamente el valor de marketingMetadata.adSignalingMode.

* Zendesk #19175 - A veces los anuncios previos no se muestran la primera vez que se reproduce el flujo.

Este problema se resolvió agregando una nueva API, adRequestTimeout, a AuditudeSettings para un tiempo de espera de solicitud de publicidad. Ahora los usuarios pueden anular el tiempo de espera predeterminado de solicitud de publicidad de 10 segundos.

**Versión 1.4.18** (1.4.18.722)

* Zendesk #3324 - El sistema de informes de anuncios Primetime no rastrea las pausas publicitarias cuando no hay medios publicitarios en un VMAP.

Cuando una pausa publicitaria está vacía, el inicio de la pausa publicitaria y los eventos de seguimiento completos no se estaban ping. Este problema se resolvió enviando pings de inicios de desglose de anuncios en los saltos de anuncios vacíos, como por ejemplo AdBreak de VMAP, con un nodo AdSource válido.

**Versión 1.4.17** (1.4.17.702)

* Zendesk #17168 - Los subtítulos no aparecen durante 10 segundos después de alternar la visibilidad

Este problema se resolvió proporcionando compatibilidad con la etiqueta EXT-X-MEDIA-TIME para los archivos de subtítulos vtt.

* Zendesk #17983 - Si no se descargan las claves de un manifiesto, se producirá un error en toda la reproducción del manifiesto

**Nota**: Debe tener al menos Flash Player FP 19.0.0.245 o superior.

Cuando a veces se reproduce contenido en directo, es posible que haya claves no válidas en el manifiesto (por ejemplo, para períodos de interrupción), pero otros intervalos de tiempo pueden tener claves válidas y se seguirán reproduciendo. Anteriormente, cuando no se podía descargar una clave enumerada en un manifiesto, se producía un error en todo el manifiesto. Ahora, el manifiesto solo falla cuando no se pueden descargar todas las claves de la lista. Si algunas claves son válidas, pero algunas de ellas no se han podido descargar, se reproducirá el contenido. Seguiremos fallando si tratamos de reproducir un segmento que requiere una clave que no tenemos.

* Zendesk #18554 - Integridad del flujo recortando las cookies en algunos casos

**Nota**: Debe tener al menos Flash Player FP 19.0.0.245 o superior.

Se corrigió un error en el código de manipulación de cookies que podría truncar los valores de las cookies.

**Versión 1.4.16** (1.4.16.684)

* Zendesk #3732 - Añada la compatibilidad con los proxies en Chrome para la integridad del flujo (requiere Flash Player FP 19.0.0.207 o bueno)

Esto es una mejora.

* Zendesk #4244 - Problemas de transmisión en PTS rollover

Este problema se resolvió detectando rollover y administrando la discontinuidad por tipo de carga útil y no de forma genérica.

* Zendesk #4487 - Seguimiento del Canal lineal del contenido

Este problema se resolvió volviendo a inicializar el rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* Zendesk #17427 - Adobe Stream Integrity no funciona a través de un proxy en Chrome (Win7) ()

**Nota**: La resolución requiere el Flash Player FP 19.0.0.2007 o bueno.

Este problema es el mismo que Zendesk #3732.

* Zendesk #17907 - Registro en el flujo en directo pHLS con Flash Player 19

**Nota**: La resolución requiere el Flash Player FP 19.0.0.2007 o bueno.

Este problema se resolvió administrando los flujos activos en los que los dominios de los archivos TS cambiaban al volver a cargar el manifiesto activo y los archivos se descargaban dos veces.

* Zendesk #17931 - El contenido HLS con pizarra al principio falla en la reproducción

**Nota**: La resolución requiere el Flash Player FP 19.0.0.2007 o bueno.

El problema se resolvió mediante la gestión de flujos sin audio en los primeros 2 segundos del primer archivo TS.

* Zendesk #17934 - Error de transmisión en directo con Flash 19.0.0.185

**Nota**: La resolución requiere el Flash Player FP 19.0.0.2007 o bueno.

El problema se resolvió mediante la gestión de flujos en directo con intercalación de tiempo entre los fotogramas de audio y vídeo en los límites del segmento.

* Zendesk #17973 - Último Flash Player 19.0.0.185 se bloquea durante el lanzamiento

**Nota**: La resolución requiere el Flash Player FP 19.0.0.2007 o bueno.

El problema se resolvió mediante la gestión de audio sin muestrear con inserción de anuncios en rollo medio. (El conmutador de analizador se produce y, en cualquier momento de la reproducción, el contenido transición al anuncio intermedio, o en mitad de la reproducción del anuncio, etc.)

* Zendesk #18049 - Flash 19 bloqueado con Firefox 42 beta

Este problema es el mismo que Zendesk #17973.

**Versión 1.4.15** (1.4.15.678)

* Zendesk #4377: Incendio el evento AD_BREAK_SKIPPED cuando se omita un salto publicitario debido a la directiva de publicidad.

La corrección consistía en agregar AD_BREAK_SKIPPED si se omitía una publicidad.

* Zendesk #4496 - Integridad del flujo: Error 102100 con redirecciones a flujos con token.

La corrección consistía en añadir compatibilidad para establecer la propiedad AVNetworkConfiguration useCookieHeaderForAllRequests mediante el TVSDK.

* Zendesk #17179 - El reproductor de Flash se bloquea en varios cambios de SAP para contenido cifrado.

Se corrigió un bloqueo durante la reproducción de contenido cifrado.

**Nota**: La corrección requiere Flash Player 19.0.0.200 o superior.

* Zendesk #17499 - cómo no eliminamos midrolls después de observar, sino que eliminamos preroll del contenido del fer

Se ha añadido un tipo en AdBreakTimelineItem (AdBreakTimelineItem.placementType) para que AdPolicySelector pueda devolver una política diferente para el contenido previo, medio y posterior al lanzamiento.

* Zendesk #17665 - Control del ancho de banda

La corrección consistía en eliminar la lógica para cambiar el tamaño del búfer de destinatario al tamaño inicial del búfer cuando empezaba el almacenamiento en búfer.

**Versión 1.14.14** (1.4.14.771)

* Zendesk #17363 - Corrección de la documentación de README para reproductor de referencia

   * Aclarar las instrucciones para descargar e instalar playerglobal.swc.
   * Añada instrucciones para actualizar la configuración del proyecto con una versión específica del reproductor Flash.
   * Actualice la configuración del proyecto AdvertisingOverlay para utilizar la versión mínima del reproductor.
   * Actualice la configuración del proyecto ReferenceCore para utilizar la versión 11.9 del reproductor específico

* Zendesk #17471 - Congelación de reproductor

Corrección parcial para un problema en el que una publicidad no se reproduce desde el principio después de la búsqueda.

* Zendesk #17496 - Podbuster no se resuelve al volver a buscar en la ventana de DVR

Proporcione parámetros personalizados para cada pausa publicitaria.

**Versión 1.4.13** (1.4.13.660)

* Zendesk #4037 - Error de Perfil no utilizable (requiere Flash Player 18.0.0.232 o bueno)

corregir el problema de análisis de URL cuando el parámetro de consulta contiene &quot;http&quot;

* Zendesk #4260 - Flash Player 18 se bloquea en IE11 (requiere Flash Player 18.0.0.232 o bueno)

Se corrigió un bloqueo al reproducir vídeo en modo de pantalla completa con IE11

* Zendesk #4262 - El reproductor de Adobe Primetime se bloquea en Windows 10 (requiere Flash Player 18.0.0.232 o bueno)

Se corrigió un bloqueo al reproducir vídeo en modo de pantalla completa con FireFox en Windows.

* Zendesk #4279 - Inserción de anuncios HLS TVSDK -302 problema de redireccionamiento en iOS y escritorio

Se corrigió un problema en el cual una dirección URL no obtenía el tipo de reconocimiento correcto porque no tenía extensión

* Zendesk #4306 - Flash Player se bloquea al pasar a pantalla completa solo en Win (requiere Flash Player 18.0.0.232 o bueno)

Se corrigió un bloqueo al reproducir vídeo en modo de pantalla completa en Windows.

* Zendesk #4480 - Faltan eventos de etiquetas ID3 (requiere Flash Player 18.0.0.232 o bueno)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI y CRS | Mejorar: Gestionar elementos dinámicos en determinadas direcciones URL de archivos multimedia.

Se ha actualizado el servicio de reempaquetado creativo para gestionar correctamente las publicidades con direcciones URL creativas dinámicas.

* PTPLAY - 2114 - Compatibilidad con reproducción MP4.

Ahora se admite la reproducción básica de contenido MP4, incluida la reproducción, la pausa y la búsqueda.

Lo siguiente requiere el Flash Player 18.0.0.225 o bueno:

* Zendesk #3992 - Velocidades adicionales de TrickPlay.

TrickPlay ahora acepta tasas superiores a 16x: +/- 32, +/-64 y +/-128.

* Zendesk #3113 - Bloqueo del complemento de Flash Player

Se corrigió un bloqueo al intentar reproducir una publicidad de redireccionamiento en Mac Firefox.

* Zendesk #4037 - Error de Perfil no utilizable
* Zendesk #4262 - El reproductor de Adobe Primetime se bloquea en las ventanas 10

Se corrigió un bloqueo en Windows Firefox durante la reproducción en pantalla completa.

**Versión 1.4.11** (1.4.11.648)

* Zendesk #1869 - Problema al cambiar el tamaño de fuente (requiere Flash Player 18.0.0.200)

Permitir el uso de tamaños de rótulos en el código de subtítulos WebVTT.

* Zendesk #3113 - Bloqueo del complemento de Flash Player (requiere Flash Player 18.0.0.200)
* Zendesk #3268 - Escritorio: Inicios del reproductor de vídeo que parpadean después de +- 40/50 segundos y inicios que se vuelven negros después de +- 90 segundos (requiere Flash Player 18.0.0.200)

Se corrigió un error de vídeo de etapa.

* Zendesk #3670 - Error INVALID_PARAMETER en VOD al buscar en el reproductor de referencia (requiere Flash Player 18.0.0.200)

InvalidateProfiles en ThreadSeek cuando se detecta un nuevo período.

* Zendesk #3896 - Bloqueo de Flash Player con la integridad del flujo activada en Chrome (requiere Flash Player 18.0.0.200)

Se ha solucionado el bloqueo en el modo de red nativo en pimienta

* Zendesk #3905 - El reproductor TVSDK no se carga cuando se aloja en CDN

Se han solucionado problemas que buscaban un token comodín cuando pageDomain es diferente del dominio swf.

**Versión 1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player bloquea el Flash en Firefox

Se corrigió un bloqueo ocasional del Flash Player con Firefox en Mac cuando un flujo, que se reproducía en un monitor externo, cambiaba a un flujo de velocidad de bits superior.(requiere Flash Player 18.0.0.160)

* Zendesk #3268 - Escritorio: Los inicios del reproductor de vídeo parpadean después de `+-` 40/50 segundos y los inicios se vuelven negros después de `+-` 90 segundos

Se ha corregido un problema en Mac Chrome por el que el flujo daba inicios para parpadear y, finalmente, volverse negro. (requiere Flash Player 18.0.0.161)

* No se rellena la macro Zendesk #3304 - VAST 3.0 `[ERRORCODE]`

   * el código de error 400 se mostrará si la publicidad en línea tiene un elemento creativo incorrecto.
   * `[ERRORCODE]` la macro estará codificada para la dirección URL

* Zendesk #3601 - Solicitud de mejora: Administración de compañeras de envoltorio

   * TVSDK mostrará envolventes complementarios que contengan recursos (html, iframe o static ) que se cerrarán en línea. (si la línea no contiene una para ese tamaño)
   * Se omitirán los acompañantes con recursos, a menos que se utilicen para la visualización. (no se usa para el seguimiento)
   * Solo se utilizarán los complementos de envoltorio con NO recurso para realizar el seguimiento. (complemento envolvente que sólo contiene seguimiento)

**Versión 1.4.9**

* Zendesk #2615 - problema al eliminar la vista HLS de la pantalla de escritorio

Se añadió el método clearVideo() en MediaPlayer. Borra el fotograma de vídeo mostrado borrando el objeto AVStream del objeto StageVideo. Sólo debe llamarse si el vídeo está en pausa y debe llamarse a replaceCurrentResource o replaceCurrentItem antes de que se pueda llamar a play() de nuevo.

* Zendesk #3169 - Actualización del reproductor de referencia con la integración de Adobe Analytics

El reproductor de referencia se ha actualizado con la integración de Adobe Analytics

* Zendesk #3296 - Desktop HLS TVSDK - VAST anuncios de terceros que no se reproducen

los tipos de MIME para el formato HLS distinguían entre mayúsculas y minúsculas, esto era incorrecto y se ha cambiado, por lo que ya no distinguen entre mayúsculas y minúsculas

**Versión 1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000 (requiere Flash Player 17.0.0.184)
* Zendesk #3007 - Anuncios previos que no aparecen después de actualizar al Flash Player 17 (requiere Flash Player 17.0.0.184)
* Zendesk #3085 - Desktop HLS Player genera un error de 106000 tras 60 segundos (requiere Flash Player 17.0.0.184)

**Versión 1.4.7**

* Zendesk #2760 - Etiqueta DISCONTINUITY ignorada durante el modo TrickPlay (requiere la versión 17.0.0.158 de Flash Player)
* Zendesk #2760 - Etiqueta DISCONTINUITY ignorada durante el modo TrickPlay (requiere la versión 17.0.0.158 de Flash Player)

**Versión 1.4.6**

* Zendesk #2652 - Documentación de Auditude para HLS de escritorio, Auditude media_id aclarado para documentación de HLS de escritorio

**Versión 1.4.5**

* Zendesk #2256 - Acceso a la lista de reproducción maestra, PSDK actualizado para distribuir eventos timedMetadata para las etiquetas suscritas en la lista de reproducción maestra. (requiere la versión 17.0.0.134 de Flash Player)
* Zendesk #2417 - El reproductor que intentaba descargar subtítulos antes del inicio de reproducción, WebVTT estaba usando la variable de número de segmento incorrecta para la coincidencia de número de segmento. El error solo se mostraba para los medios que tenían índices de segmentos que empezaban en cero. (requiere la versión 17.0.0.134 de Flash Player)
* Zendesk #2537 - El reproductor de Flash se bloquea al utilizar el plugin de pimienta con Chrome (requiere la versión de Flash Player 17.0.0.134)
* Zendesk #2547 - subtítulos en árabe: El texto debe estar alineado con la justificación correcta (requiere la versión 17.0.0.134 de Flash Player)

**Versión 1.4.4**

* Zendesk #1561 - Re: `[Adobe Primetime]` Actualización: Compatibilidad con failover basado en cliente HLS para PROGRAMA-DATE-TIME en el PSDK de escritorio (requiere la versión de Flash Player 16.0.0.305 o buena)
* Zendesk #2197 - `[Ads]` Seguimiento de errores de publicidad
* Zendesk #2286 - Solicitud de función: Proporcionar información sobre el estado de carga de la publicidad (VPAID)
* Zendesk #2285 - Solicitud de función: Omitir publicidad después de una duración de tiempo de espera especificada
* Error #3921755 - Actualización de la biblioteca OpenSSL a la versión 1.0.1L en Flash Player (requiere la versión de Flash Player 16.0.0.305 o buena)

**Versión 1.4.2**

* Zendesk #1303 - Desplazamiento vertical para subtítulos opcionales (requiere la versión 16.0.0.235 de Flash Player o la fecha buena de lanzamiento prevista: Diciembre de 2014)
* Zendesk #1870 - Encendido y desactivación de subtítulos opcionales (requiere la versión 16.0.0.235 de Flash Player o la buena fecha prevista de lanzamiento: Diciembre de 2014)
* Zendesk #2110 - La reproducción se queda atascada después de intentar entrar a pantalla completa durante un anuncio VPAID (requiere la versión de Flash Player 16.0.0.235 o la fecha buena de lanzamiento prevista: Diciembre de 2014)
* Zendesk #2199 - `[VPAID]` Jugador no responde al buscar una pausa publicitaria pasada
* Zendesk #2358 - Re: `[Analytics]` Datos incorrectos del capítulo

**Versión 1.4.1**

* Se ha actualizado la API de apagones para que sea coherente con la implementación de Android e iOS.

**Versión 1.4.0**

* Zendesk #1024 - Función para eliminar anuncios del flujo mediante manifiesto
* Zendesk #1423 - Error de reproducción HLS está bloqueando el Flash Player (sin error informado)
* Zendesk #1674 - ClosedCaption No aparece, se muestra correctamente el 708 subtítulos cuando faltan los códigos 0x03 ETX.

## Problemas conocidos {#known-issues}

* El subtítulo cerrado no funcionará con contenido de solo audio porque el sistema de subtítulos necesita que el vídeo funcione.
Sin vídeo, no hay ninguna dimensión de ventanilla móvil y, sin ella, no se puede mostrar ningún gráfico para los rótulos.
* La integridad del flujo es ligeramente más lenta en Google Chrome debido a las restricciones del entorno limitado de Chrome.
* En TVSDK 1.4, si deshabilita la reproducción automática, puede producirse un error de DRM cuando el reproductor permanece inactivo durante al menos un minuto. Para solucionar este problema, al deshabilitar la reproducción automática pero cargar previamente recursos, modifique `ReferenceCore.as` cambiando el contenido de `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versión 1.4.13** PTPLAY-8501 - Cuando VMAP devuelve dos anuncios directos no transcodificados MP4, se reproduce dos veces la misma caída y segunda.

* **Versión 1.4.2** En la versión 16 de Flash Player, se identificó un problema con la lógica ABR &quot;apagado&quot;, después de que el reproductor se coloca en un evento de almacenamiento en búfer vacío. El problema evita que la velocidad de bits se apague en entornos de ancho de banda incorrectos una vez que el reproductor se encuentre en estado de almacenamiento en búfer. Para solucionar el problema, haga que la aplicación establezca el `BufferControlParameters.initialBufferTime` como `BufferControlParameters.playbackBufferTime` temporalmente durante el estado de almacenamiento en búfer (es decir, en un evento `BufferEvent.BUFFERING_BEGIN`) y luego restablezca los valores establecidos en el evento `BufferEvent.BUFFERING_END`. La corrección de este problema estará disponible en la próxima versión de parche de Flash Player versión 16.

* **Versión 1.4.0**

   * PTPLAY-1634 - La misma etiqueta de suscripción tiene diferentes marcas de hora en diferentes ventanas activas. Cuando se mueven ventanas en vivo, la misma etiqueta de cada una de ellas debe tener las mismas marcas de hora. Sin embargo, a veces las mismas etiquetas tienen marcas de hora diferentes.
   * PTPLAY-28 - La línea de tiempo de MediaPlayer no incluye saltos vacíos.
   * Se requiere un archivo de política entre dominios (cross-domain.xml) para obtener permiso para transmitir contenido desde un dominio diferente. [Configuración de un archivo cross-domain.xml para flujo](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html) HTTP.
   * Error #3694203 - En un flujo de DVR, la búsqueda desde dentro de un anuncio de reproducción a otro anuncio intermedio puede provocar el bloqueo del explorador
   * Error #3753725 - selectPolicyForSeekIntoAd no tiene en cuenta si se ha visto la pausa publicitaria
   * Error n.º 3754529: Los anuncios preliminares no se eliminan del flujo cuando se buscan de nuevo en un flujo de DVR en directo
   * Error #3761896 - Si se permite la búsqueda durante la reproducción del anuncio, los marcadores de anuncio se reajustarán después de la búsqueda. La solución consiste en no utilizar la llamada de retorno ITEM_UPDATED durante la búsqueda
   * Error n.º 3779889: la llamada completa no se realiza cuando se llega al final de la reproducción mediante trucos en Video Analytics
   * Error #VA-779 - No se envía el latido de evento de cambio de velocidad de bits para la implementación de referencia de compatibilidad con Heartbeat de Video Analytics mejorada. La reproducción de trucos no se implementa en la aplicación de ejemplo.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Información y soporte de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
