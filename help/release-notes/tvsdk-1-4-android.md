---
title: Notas de la versión de TVSDK 1.4 para Android
description: Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos, y los problemas de los dispositivos en TVSDK para Android 1.4.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---

# Notas de la versión de TVSDK 1.4 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos, y los problemas de los dispositivos en TVSDK para Android 1.4.

## Nuevas funciones {#new-features}

**Versión 1.4.43**

**Carga segura de publicidad a través de HTTPS**

Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad de primetime y a CRS a través de HTTPS.

**alwaysUseAudioOutputLatency(valor booleano) en la clase MediaPlayer**

Cuando este parámetro esté establecido, utilice la latencia de salida de audio en el cálculo de la marca de tiempo de audio.

Acepta un valor de parámetros booleanos. Si su valor es `True`, el cliente utiliza la latencia de salida de audio en el cálculo de la marca de tiempo del audio.

**Versión 1.4.42**

**Inserción parcial de desglose de anuncios:**
Experiencia similar a la de una TV de unirse en medio de un anuncio sin activar el seguimiento del anuncio parcialmente visto.
Ejemplo: Las uniones de usuarios se producen en medio (a los 40 segundos) de una pausa publicitaria de 90 segundos y consisten en tres anuncios de 30 segundos. Son 10 segundos del segundo anuncio de la pausa.
* El segundo anuncio se reproduce durante el tiempo restante (20 segundos) seguido del tercer anuncio.
* Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Los rastreadores solo del tercer anuncio se activan.

**Versión 1.4.41**

No hay nuevas funciones.

**Versión 1.4.40**

No hay nuevas funciones.

>[!NOTE]
>
>No requerirá los cambios de la API si su versión es anterior a la 1.4.39.

**Versión 1.4.39**

* TVSDK está certificado con VHL 2.0.1 y con VHL 2.0.1 con Nielsen.
* El TVSDK de Android se ha actualizado para realizar solicitudes de CRS desde el nuevo host de Akamai `primetime-a.akamaihd.net`.
* La nueva configuración de nombre de host proporciona la entrega de recursos CRS a través de HTTP y HTTPS (SSL) a mayor escala.
* TVSDK admite la versión de Android Oreo.
* Se agrega una nueva función a `AdClientFactory` para admitir el registro de varios detectores de oportunidades:

  ```
  public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
  ```

  Esto debería devolver una matriz de PlacementOpportunityDetector. Ahora puede registrar varios detectores de oportunidades. Por ejemplo, para la función de salida anticipada de publicidad, se requerían dos detectores de oportunidades: uno para la inserción de publicidad y otro para la salida anticipada de publicidad. Solo debe implementar este nuevo impacto de función si ha implementado su propio AdvertisingFactory (y no utiliza DefaultAdvertisingFactory). Para obtener el comportamiento existente, debe crear un único detector de oportunidades, como en la función createOpportunityDetector() , y colocar en una matriz y devolver:

  ```
  public class MyAdvertisingFactory extends AdvertisingFactory {  
  …  
  @Override  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
  return opportunityDetectors;  
  } }
  ```

>[!NOTE]
>
>No requerirá los cambios de la API si su versión es anterior a la 1.4.39.

**Versión 1.4.36**

Corrección de errores para la omisión de contenido en Android.

**Versión 1.4.35**

* **Información de anuncio de red**

  Las API de TVSDK ahora proporcionan información adicional sobre las respuestas VAST de terceros. Las extensiones de ID de anuncio, sistema de publicidad y anuncio VAST se proporcionan en la clase NetworkAdInfo, a la que se puede acceder mediante la propiedad networkAdInfo de un recurso de publicidad. Esta información se puede utilizar para integrar con otras plataformas de Ad Analytics como **Análisis de foso**.

**Versión 1.4.31**

**Compatibilidad con varias CDN para anuncios CRS**
* De forma predeterminada, todos los recursos transcodificados se alojarán en CDN propiedad del Adobe en Akamai. Con la última versión, el servicio de reempaquetado creativo de Adobe (CRS) permite cargar los elementos creativos transcodificados en varias CDN según especifique el cliente.
* Se añaden nuevas API al TVSDK para permitir la especificación de la URL creativa final de CRS cuando no se utiliza la URL predeterminada. Consulte la documentación para aprender a utilizar estas nuevas API.

**Versión 1.4.18**
Primetime Android TVSDK ahora es compatible con los creativos de JavaScript VPAID 2.0 para permitir una experiencia de anuncio en flujo enriquecida e interactiva. Para obtener más información sobre VPAID 2.0, consulte [Compatibilidad con anuncios VPAID](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Versión 1.4.17**

AC-3 5.1 solo es compatible con Amazon FireTV.

**Versión 1.4.11**

* **Ad Fallback, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103** Para los anuncios VAST (creativos) con la regla de reserva habilitada, TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Anuncio alternativo para anuncios VAST y VMAP](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Biblioteca de Video Heartbeats (VHL) actualizada a la versión 1.5**
   * Capacidad para enviar metadatos con inicio de vídeo o inicio de vídeo/publicidad/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño

**Versión 1.4.7**

* **Soporte de individualización local** Compatibilidad con instalaciones on-premise del servidor de individualización de Adobe para personalizar la solicitud de individualización del cliente para ir a un punto final diferente.

**Versión 1.4.6**

* **Cifrado AES de muestra (requiere la versión 17.0.0.134 del Flash Player)**Ahora se admite el cifrado AES basado en muestra.

**Versión 1.4.2**

* **Actualización de la biblioteca de Video Heartbeats (VHL) a la versión 1.4.0.1.**

   * Se ha añadido la capacidad de combinar diferentes casos de uso de análisis, de otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete. La pausa publicitaria se deduce de las llamadas a los métodos trackAdStart y trackAdComplete.
   * La propiedad cabezal de reproducción ya no es necesaria al rastrear anuncios.

* **Integración del SDK de Nielsen** TVSDK ahora admite el envío de información de seguimiento de usuarios al SDK de Nielsen sin ninguna integración personalizada.

**Versión 1.4.0**

* **Señalización De Interrupción Con Sustitución De Contenido Alternativo** Como parte de la actualización de TVSDK 1.4, TVSDK ahora también admite la inclusión y la devolución de interrupciones regionales en contenido lineal. El TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para monitorizar las señales de interrupción incluso cuando se muestra programación alternativa en lugar de la programación original.

* **Eliminar/reemplazar anuncios C3** Ahora, no se necesita ningún trabajo de preparación adicional para insertar dinámicamente nuevos anuncios en recursos de vídeo bajo demanda (VOD) que salen de la ventana de C3. TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar dinámicamente nuevos anuncios. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se emite durante la emisión y se extrae inmediatamente para su uso como contenido bajo demanda sin el tiempo adecuado para &quot;limpiar&quot; el recurso.

* La interfaz PlaybackEventListener tiene un nuevo método denominado onReplaceMediaPlayerItem, que puede utilizar para detectar un nuevo evento, `ITEM_REPLACED`. Este evento se envía cada vez que se reemplaza una instancia de MediaPlayer en MediaPlayer. La aplicación cliente que implementa este PlaybackEventListener debe implementar o anular este nuevo método.
* AdClientFactory tiene una nueva función agregada a la clase para registrarse en varios detectores de oportunidades:

  ```
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
  
  For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
  
  To override this new function create a single Opportunity Detector, and put into an array and return:
  
  @Override
  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
  
  return opportunityDetectors;
  }
  
  }
  ```

## Cambios en TVSDK para 1.4 {#tvsdk-changes}

* La interfaz PlaybackEventListener tiene un nuevo método denominado onReplaceMediaPlayerItem, que puede utilizar para detectar un nuevo evento, ITEM_REPLACED. Este evento se envía cada vez que se reemplaza una instancia de MediaPlayer en MediaPlayer. La aplicación cliente que implementa este PlaybackEventListener debe implementar o anular este nuevo método.

* AdClientFactory tiene una nueva función agregada a la clase para registrarse en varios detectores de oportunidades:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Por ejemplo, para la función de salida anticipada de un anuncio, necesita dos detectores de oportunidades: uno para la inserción de anuncios y otro para la salida anticipada del anuncio.

Para anular esta nueva función, cree un único detector de oportunidades, colóquelo en una matriz y devuélvalo:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Certificación y compatibilidad de dispositivos en 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Las siguientes funciones son **no** admitido en el TVSDK:
>
>* Cámara lenta, en cualquier plataforma o versión.
>* Jugar truco en vivo.

**Versión 1.4.43**

TVSDK 1.4.43 está certificado con dispositivos Android con Android 6.0.1/ 7.0 y 8.1 (Oreo).

* **Versión 1.4.23:**

   * TVSDK 1.4.23 está certificado para dispositivos Android con Android N.

* **Versión 1.4.18:**

   * Primetime ha sido certificado para Amazon Fire TV.
   * VPAID 2.0 solo es compatible con dispositivos con Android 4.0 y versiones posteriores.

## Problemas resueltos en 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Se recomienda encarecidamente a todos los clientes de TVSDK que utilicen CRS que actualicen a TVSDK 1.4.39 o la versión más reciente en iOS y Android. Esta actualización sustituye a la implementación de la aplicación existente. Después de la actualización, compruebe las solicitudes de URL creativas de CRS en una herramienta proxy (por ejemplo, Charles) para verificar que la versión de la ruta refleje la versión 3.1. Por ejemplo:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versión 1.4.43**

* Ticket #27143: no se puede reproducir la pista de audio 5.1 en dispositivos FireTV

   * TVSDK ahora puede reproducir audio AC3 en dispositivos FireTV. La reproducción siempre es en estéreo.

* #33902 de tickets: Entrega segura de publicidad a través de HTTPS

   * Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad de primetime y a CRS a través de https.

* Ticket #34493 - Retardo de audio Bluetooth

   * Añadido `alwaysUseAudioOutputLatency` en la clase MediaPlayer que, cuando se establece, utilizará la latencia de salida de audio en el cálculo de la marca de tiempo de audio.

* #34949 de tickets: nueva versión de la biblioteca de Video Heartbeat (VHL) integrada.

**Versión 1.4.42 (1791)**

* Zendesk #33719: FireTV 4k Adaptive Bitrate se escala lentamente. Se ha agregado compatibilidad con ABR para dispositivos FireTV 4K.
* Zendesk #33338: resetDRM borra todos los datos de la aplicación.  Se ha gestionado un caso adicional en el que las excepciones en subprocesos que no son de TVSDK provocaban que las colas de operación de TVSDK se llenaran.

**Versión 1.4.41 (1776)**

* Zendesk #33002: datos de recursos complementarios de TVSDK en Fire TV. Se ha implementado una nueva clase AdBannerAsset que devolverá los datos complementarios como Lista &lt;adbannerasset> y AdAsset::id es ahora String en lugar de long.
* El reproductor de Zendesk #32821 - Android Primetime se congela cuando encuentra la Marca de tiempo de presentación (PTS) para WWE. Este problema se corrigió en esta versión.
* #33572 de Zendesk: Error de inicio del anuncio de VideoAnalyticsProvider. Este problema se ha corregido mediante la combinación correcta de la versión del SDK conjunto de VideoHeartbeat.jar de VHL+Nielsen.
* Zendesk #33355 - Fire TV: Retira el número de 15 segundos. No hay ninguna corrección del lado de TVSDK y del cliente que verifique esto en su extremo y en un tercero.

**Versión 1.4.40 (1764)**

* Zendesk #33068 - Amazon problema de sincronización de labios en el nuevo dispositivo. El problema de sincronización de labios se ha corregido en estas versiones.
* Zendesk #32215 - Problemas de seguridad de Android TVSDK 1.4.38 `[Hotlist]`. Se ha actualizado a la última versión OpenSSL-1.1.0 y curl-7.55.1.
* Zendesk #32920: pantalla en blanco dentro de una pausa publicitaria y sin finalización de la pausa publicitaria. Se ha corregido un problema en el cual un contenedor VPAID podía entrar en estado de bloqueo y se gestionaba un problema en el que los anuncios VPAID de Facebook devolvían a menudo varios bloques CDATA en un único nodo \&amp;lt;AdParameters\&amp;gt; VAST.

**Versión 1.4.39 (1744)**

* Zendesk #28976 - La solicitud de licencia toma más de un segundo. Mientras se ejecutan las llamadas de solicitud de licencia DRM que utilizan POST, Curl añade el encabezado adicional &quot;Esperar: 100-continue&quot;. Se ha eliminado el encabezado &quot;Esperar:&quot; en TVSDK
* Zendesk #27707: Los entornos CSAI no respetan los marcadores CUE IN para un retorno anticipado o un retorno al contenido. Se proporcionó soporte para varios generadores de oportunidades.

**Versión 1.4.38 (1722)**

* Zendesk #21590: Rendimiento y seguimiento de vídeos en las últimas versiones de origen

Integración y certificación de VHL 2.0 en TVSDK para reducir la barrera en la implementación de VideoHeartbeatsLibrary al reducir la complejidad de las API.

* Zendesk #29688: Compatibilidad con clientes de Android O Beta.

Compatibilidad de TVSDK con la nueva versión beta de Android.

**Versión 1.4.36 (1713)**

* Zendesk #27392 - Omisión de contenido en Android

Para dar cabida al descifrado, el TVSDK de Android ampliaba incorrectamente el intervalo de bytes del contenido que no era iframe en 16 bytes. La ampliación es necesaria para las secuencias de Iframe, pero no para las secuencias que no son de iframe.

**Versión 1.4.34 (1702)**

* Zendesk #27638 - Fuga en el objeto cURL INet

El objeto Posix cURL INet se filtraba mientras se aferraba al administrador de recursos compartidos y a la caché DNS que se usaba en las conexiones cURL.

Este problema se resolvió eliminando el objeto Posix cURL INet del desconstructor INet.

**Versión 1.4.33 (1694)**

* **Biblioteca OpenSSL**

La biblioteca OpenSSL se ha actualizado con OpenSSL versión 1.0.2j.

* Zendesk #21701: envíe la URL creativa original para la solicitud CRS 1401 en lugar de la URL normalizada.
Este problema se resuelve enviando las URL creativas originales.

* Zendesk #25023 - Reproducción de vídeo de larga duración: congelación de vídeo, parpadeos en la pantalla Este problema se resolvió estableciendo las dimensiones máximas de formato de vídeo para los dispositivos de decodificador CenturyLink.

* #27460 de Zendesk: La nueva cuenta de Akamai no puede gestionar una solicitud de cdn de POST.
El código se ha actualizado para que la `cdn.auditude.com` solicitud de anuncio para ser GET en lugar de POST.

* Zendesk #28245: El estado de reproducción no se notifica correctamente cuando la aplicación pasa de segundo plano a primer plano. Este problema se resolvió restaurando correctamente el estado de reproducción para que se reproduzca o se detenga cuando la aplicación vuelva a primer plano.

**Versión 1.4.32 (1682)**

* Zendesk #25779: La vulnerabilidad de seguridad que se encuentra con TVSDK Android 4.2 y versiones posteriores tiene una vulnerabilidad de seguridad cuando JavaScript está habilitado en un WebView. El uso de WebView por TVSDK se ha deshabilitado para los dispositivos que ejecutan el sistema operativo 4.2 o inferior. Esto deshabilita el uso de anuncios VPAID en TVSDK en estos dispositivos.

* Zendesk #26890 - Problema en estado de PANTALLA (ENCENDIDO/APAGADO) manejo Ref. Reproductor Cuando el motor de vídeo de Adobe (AVE) se reanuda desde un estado SUSPENDIDO, DefaultMediaPlayer no actualiza su estado. Como resultado, DefaultMediaPlayer permanece en estado SUSPENDIDO aunque el AVE esté en estado REPRODUCIENDO. Este problema se ha resuelto estableciendo el estado DefaultMediaPlayer en PLAYING al recibir un estado PLAY del AVE, incluso si el estado actual de DefaultMediaPlayer es SUSPENDED.

**Versión 1.4.31 (1675)**

* Zendesk #21974 - Excepciones por objetos nulos
   * AdIndex rara vez se incrementa cuando es nulo. Esto puede deberse a llamadas de API incorrectas recibidas para el anuncio previo a la emisión. Se han corregido los tipos de datos para evitar estas excepciones

* Zendesk #24714: Desactivar el registro superfluo
   * Se ha actualizado TVSDK para desactivar el registro superfluo

* Zendesk #24488 - Problemas de sincronización AV en Fire TV
   * Se ha solucionado mejorando el manejo de los hilos del decodificador AV. En concreto, cada vez que se modifican las colas de los marcos de entrada o salida, se ejecuta el subproceso descodificador específico del tipo de contenido del marco.

* Zendesk #26551: Corrija los errores de CRS
   * Cuando la solicitud es HEAD (http head), no es necesario leer el contenido porque está vacío. Aunque está bien intentar leerlo, el antiguo Android (4.0.x) se bloquea mientras llamamos a read() y el nuevo Android devuelve el valor correcto (-1) cuando llamamos a read(). En función de esto, cambió el código a no leer el contenido de &quot;head&quot;

* Zendesk #26696 Excepción de puntero nulo al acceder a TrickPlayManager
   * Se corrigió comprobando si el objeto TrickPlayManager no es nulo antes de utilizarlo.

**Versión 1.4.30 (1659)**

* Zendesk #22675 La duración de los recursos no se actualiza para los flujos en directo/lineales Este problema se resolvió proporcionando una nueva API, assetDuration, en PTVideoAnalyticsTrackingMetadata que proporciona la duración de los recursos para los flujos en vivo y lineales.

* Fuga de memoria de Zendesk #25853 en TVSDK al cambiar de canal Se ha resuelto el problema de la fuga de búfer de lectura de archivos cuando se restablece o libera el MediaPlayer al descargar un archivo.

**Versión 1.4.29 (1653)**

* Zendesk #21200: El reproductor no se recupera del estado suspendido cuando la aplicación estaba en segundo plano. Cuando el reproductor se suspendió después de que se indicara el cambio de flujo, la resolución permite al reproductor realizar el cambio de flujo cuando se restaura el reproductor desde el estado de suspensión, en lugar de restaurarlo a la posición anterior.

* Zendesk #23412 - El reproductor se queda atascado con una caja negra si hace clic en cualquier anuncio dentro de los últimos 3 segundos de la pausa publicitaria. Este problema es el mismo que el de Zendesk #21200.

* Zendesk #23616: La pausa para anuncios omitida busca demasiado en el futuro Según el tipo de inserción de publicidad (inserción/sustitución), TVSDK determina si la duración de la publicidad se utiliza en el cálculo para determinar el punto final de la pausa publicitaria.

* Fuga de memoria DRM de Zendesk #25078 - TVSDK en Android TV STB La fuga de memoria para el objeto adaptador DRM se ha localizado y corregido.

* #25067 de Zendesk: error en VideoEngineTimeline Esto sucede porque los objetos no se limpiaron correctamente y se llamó a eventos después de que se destruyeron. El problema se resolvió añadiendo comprobaciones para evitar excepciones nulas.

* Zendesk #25352 - Set custom HTTP header Este problema se resolvió añadiendo un nuevo encabezado personalizado a la lista de permitidos en TVSDK.

* Zendesk #25617 - Live stream PTS rollover causando discontinuidad del reproductor y bloqueo de memoria Este problema se resolvió añadiendo una gestión de rollover PTS en FragmentedHTTPStreamer cuando se produce una rollover en medio de un segmento.

**Versión 1.4.28 (1637)**

* Zendesk #23618: Los eventos de pausa publicitaria se activan antes de consultar la política de publicidad. Este problema se resolvió al no activar los eventos AD_BREAK_START y AD_START cuando se omite el anuncio debido a adForgibility. En su lugar, se envía el evento AD_BREAK_SKIPPED.

**Versión 1.4.27 (1631)**

* Zendesk #23174: Problema de rendimiento al cambiar el tamaño del vídeo Este problema se resolvió al probar una nueva API, MediaPlayerView.setSurfaceFixedSize, que permite a TVSDK acceder a SurfaceHolder.setFixedSize() desde MediaPlayerView.

* Zendesk #24450 - TVSDK realiza solicitudes de publicidad duplicadas Este problema se producía cuando el tiempo transcurrido se convertía en largo y no en doble, y este problema se ha corregido.

**Versión 1.4.26 (1627)**

* Zendesk #21436 - Actualización de la biblioteca OpenSSL a la versión 1.0.2h Actualización de la biblioteca OpenSSL a la versión 1.0.2h OpenSSL
* Zendesk #23825: Las cookies no se incluyen en las llamadas de retorno. Se corrigió al proporcionar compatibilidad con cookies de Android.

**Versión 1.4.25 (1620)**

* Zendesk #22900 - Live Adobe Primetime DRM stream no se está reproduciendo en el reproductor de referencia de Android El problema de asignación de memoria se ha corregido.
* Zendesk #23176: La aplicación se bloquea cuando intenta reproducir anuncios VPAID El bloqueo se produjo porque la aplicación no crea una vista de anuncio personalizada para procesar un anuncio VPAID. Este problema se resolvía ignorando los anuncios VPAID en la respuesta del servidor de publicidad cuando no había ninguna vista de anuncio personalizada.

* Zendesk #23153 - SampleAES DRM Stream - Parada de reproducción en el reproductor de referencia de TVSDK Este problema es el mismo que el de Zendesk #22900.

**Versión 1.4.24 (1612)**

* Zendesk #20784 - Analytics: Se activa la finalización del contenido para las transiciones de vídeo en directo Este problema se resolvió añadiendo una API (trackVideoComplete) para almacenar manualmente en déclencheur la finalización del contenido durante una sesión de seguimiento de vídeo lineal/en directo.

* Zendesk #21977 VideoEngineTimeline se bloquea durante la operación placeAdBreak/acceptAd
   * En este número, se actualizaron las siguientes bibliotecas:
      * Biblioteca de Adobe Mobile a la versión 4.10.0
      * Biblioteca VHL a la versión 1.5.6
      * Biblioteca VHL-Nielsen a la versión 1.6.7

Este problema se solucionó añadiendo una comprobación nula antes de añadir anuncios a la lista de anuncios aceptados.

* Zendesk #22313 La velocidad de bits para los STB con el chipset Amilogic no va más allá de 1,2 millones Este problema se resolvió precargando las funcionalidades del códec de medios y deshabilitando el conmutador sin problemas para los dispositivos con chipset Amilogic.

* Zendesk #19520 Recurso HLS de AES de muestra no se reproduce en reproductores de TVSDK Este problema se resolvió al administrar varios descriptores de PAGO para flujos HLS cifrados de AES de muestra.

**Versión 1.4.23 (1602)**

* Zendesk #18852: actualizar la lógica de selección creativa basada en las reglas de CRS Este problema se resolvió añadiendo un archivo de configuración JSON para especificar la prioridad de selección creativa.

* Zendesk #20861 - Android N Esta versión es compatible con Android N al eliminar la capacidad de usar directamente las bibliotecas nativas de la plataforma Android a las que ya no pueden acceder las aplicaciones que se ejecutan en Android N.

* Zendesk #21018 - Android N crash Misma resolución que ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter se bloquea en un error Invalid_Key El error Invalid_Key no incluye una descripción de AVE, por lo que el análisis del texto resultó en NPE. El problema se resolvió agregando una comprobación nula para la descripción durante onError antes de analizar la descripción.

* Zendesk #22286: La biblioteca nativa está asignando la clave/fragmento de lectura de memoria, lo que provoca el bloqueo . Este bloqueo que se produjo en Android al intentar cargar un manifiesto con varias claves simultáneamente se ha corregido.

**Versión 1.4.22 (1581)**

* Zendesk #17236: Tiempo de reproducción de vídeos HLS con DRM Poco fiable Se ha corregido el salto de tiempo con los flujos LBA, donde el tiempo de inicio del segmento de audio no coincide con el tiempo de inicio del segmento de vídeo.

* Zendesk #17680 - La reproducción de vídeo se está congelando en el cuadro de Selevision Andredo El decodificador de vídeo en este dispositivo a veces devuelve un salto de tiempo de salida significativo al eliminar el fotograma de vídeo del búfer de salida, y esta marca de tiempo de salida permanece alta. Este problema se resolvió devolviendo un *perfil de vídeo no admitido* error que no fuerza al reproductor a reintentar el mismo perfil o elegir un perfil diferente.

* Zendesk #19074 - Congelación de vídeo durante el juego de trucos FFWD y REW Este problema se resolvió añadiendo una nueva advertencia TRICKPLAY_ENDED_DUE_TO_ERROR para notificar a la aplicación que el juego de trucos ha salido y que el vídeo se detuvo debido a un error irrecuperable.

* Zendesk #19574 - TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM Este problema se resolvió de las siguientes maneras:

* Zendesk #19986: comportamiento de OP roto para ciertos dispositivos como Android TV
* Añadir un error FILE_NOT_FOUND a la condición.
* Cuando el error proviene de un *archivo no encontrado* error, separando la dirección URL y la respuesta de la descripción del error si la respuesta está disponible.
Se ha corregido el error lógico introducido por el soporte de NVidia shield OP. En dispositivos blindados que no sean NVidia, confíe en los indicadores seguros de pantalla incluso cuando se desconozca el tipo de pantalla.

* Zendesk #20549 - Manejo de listas de reproducción antiguas. Este problema se resolvió reduciendo el intervalo entre la actualización del manifiesto activo y la mitad de la duración del segmento esperada, si la captura anterior no recibe nuevos segmentos.

* Zendesk #20742: El uso de memoria parece seguir aumentando cuando se reproduce contenido en directo en FireTV. El bloqueo se debe a la tabla de referencia de objetos JNI que ha alcanzado el límite. Este problema se resolvió eliminando la referencia al objeto MediaFormat que se creó durante el reinicio del decodificador.

* Zendesk #21125: Regrese antes de la pausa publicitaria en directo/lineal (CSAI). Se ha añadido una función que permite al reproductor volver al contenido principal durante una pausa publicitaria si el reproductor registra el empalme en las señales de anuncio mediante el uso del empalme en el detector de oportunidades.

* #21334 de Zendesk: valor de tiempo de espera de solicitud de anuncio de TVSDK para solicitudes de publicidad de terceros. Se ha añadido una configuración adRequestTimeout a AdvertisingMetadata que permite un tiempo de espera global para la llamada de anuncio.

**Versión 1.4.21 (1566)**

* Zendesk #17781: La captura de pantalla de ADB ya no funciona Este problema se resolvió agregando la API DefaultMediaPlayer.create(Context, boolean secureSurface), que permite la captura de pantalla.
Para permitir capturas de pantalla, pase false para secureSurface.
Importante: Recomendamos encarecidamente que no habilite esta función de captura de pantalla en una configuración de producción.

* Zendesk #19074 - Congelación de vídeo durante el juego de trucos FFWD y REW Se han resuelto los siguientes problemas que ocurrieron cuando el trickPlay podía congelarse en la reproducción:

* Zendesk #19532 - Close Caption está apareciendo desordenado
   * FHS inicia el juego de trucos, pero el primer segmento de iframe no tenía un fotograma.
   * Al descargar un segmento de iframe, si FHS da error, sale de trickplay y pausa la reproducción.
   * La implementación de Android MediaCodec espera para siempre la disponibilidad de la cola de entrada mientras se le pedía que vaciara todos los búferes de entrada y salida.
Este problema se resolvió invirtiendo el orden de las señales WebVTT, de modo que varias señales superpuestas parezcan &quot;desplazarse hacia arriba&quot;.

* Zendesk #19574: TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM En la carga inicial del archivo de manifiesto en PTMediaPlayerItem.prepareToPlay, si la carga falla, TVSDK no informa del cuerpo de la respuesta de error a la aplicación.
Este problema se resolvió permitiendo que TVSDK informara de la respuesta de error como un error a la aplicación.

* Zendesk #19701 - Congelación de la reproducción con SAP/Discontinuidad Se ha resuelto la congelación del reproductor cuando el audio y el vídeo no están alineados en la discontinuidad.

* Se ha resuelto el error #PTPLAY-11162: Actualización de la biblioteca OpenSSL a la versión 1.0.2f.

**Versión 1.4.20 (1546)**

* Zendesk #17384 - Solicitud de funciones: A partir de la versión 1.4.20 de TVSDK para Android, se ofrece compatibilidad con metadatos ID3 para la reproducción de AAC para las etiquetas ID3 en medios AAC.

* Zendesk #18358: el reproductor se bloquea en el conmutador de velocidad de bits con discontinuidades fuera de sincronización Este problema se resolvió al tratar adecuadamente los casos extremos de vinculación ABR.

* Zendesk #19232: La aplicación que utiliza TVSDK 1.4.18 se comporta de forma extraña en la versión 4 del sistema operativo Amazon más antigua. Este problema se resolvió eliminando la creación de vistas web ocultas en el proceso de inicialización del reproductor TVSDK para evitar conflictos con los dispositivos que no admiten Android Webview.

* Zendesk #19585: Reproducción a cámara lenta cuando se produce una transición de velocidad de bits adaptable.
Durante el cambio ABR, si el nuevo perfil tiene una velocidad de muestreo de audio diferente a la del perfil actual, la reproducción se vuelve a cámara lenta o rápida. Esto se debe a que no se notifica al presentador de vídeo que el formato de audio ha cambiado.
Este problema se resolvió asegurándose de que el indicador de notificación se establece en el lugar correcto.

* Zendesk #19683 - Reproducción SAP DAI - Sin audio durante unos segundos.
En varios casos de la lógica de TVSDK, cuando se comparó la marca de tiempo de dos segmentos de representación, RENDITION_TIMEOUT_THRESHOLD se utilizó como un rango de valor aceptable, ya que la marca de tiempo no siempre puede coincidir con una diferencia de 0 ms. Si la brecha se encuentra dentro del rango de RENDITION_TIMEOUT_THRESHOLD, se supone que coincide.

RENDITION_TIMEOUT_THRESHOLD se estableció en 100 ms, pero resultó insuficiente para ciertas secuencias. Este problema se resolvió aumentando RENDITION_TIMEOUT_THRESHOLD a 200 ms.

* Zendesk #19699: TVSDK no puede cambiar entre las pistas de subtítulos VTT. Este problema se resolvió volcando el reproductor y recargando el manifiesto cuando cambia una pista y corrigiendo el problema de conversión de cadenas UTF8 que afectaba a los nombres de las pistas de subtítulos WebVTT de doble byte.

* Zendesk #19717 - Problema de visualización de las opciones de CC Este problema se resolvió administrando correctamente la cadena Unicode.

* No se han detectado etiquetas Zendesk #19910 - TIT2 ID3 Este problema se ha resuelto proporcionando una compatibilidad más completa para las codificaciones de cadena ID3 v2.4 y para la compatibilidad con ID3 v2.3.

* #20135 de Zendesk: El SDK de TVSDK activa varias opciones onComplete para el contenido de VOD.
Este problema se resolvió agregando el detector de eventos post_roll_complete en el lugar correcto, en lugar de en el caso completo del evento de cambio de estado.

**Versión 1.4.19 (1521)**

* #4180 de Zendesk: TVSDK no aplica HDCP.
   * Esta es una corrección parcial para este ticket y solo soluciona el problema de los dispositivos de escudo NVidia.
Debe utilizar la API de detección de HDCP correctamente implementada en Nvidia Shield para realizar un seguimiento dinámico del estado de HDCP.

* Zendesk #18358: El TVSDK se congela en el conmutador de velocidad de bits sin interrupciones sincronizadas.
   * Este problema se resolvió añadiendo una nueva advertencia para detectar la discontinuidad de PTS y forzando la comprobación de PTS para rehacer la búsqueda del segmento correcto para cada conmutador ABR.
Para corregir el bloqueo, la llamada al método mediaPlayer.setCustomConfiguration debe incluir forcePTSCheckForABR como argumento.

* Zendesk #19038 - No hay transmisión en vivo en Asus Zenpad 10.

  Este problema se resolvía cargando previamente la información del códec de medios, de modo que no se consultaba la función en tiempo de ejecución.

* Los siguientes problemas son los mismos que Zendesk #19038:
   * Zendesk #19483: El TVSDK se bloquea en la plataforma Intel.
   * Zendesk #19171 - Se bloquea en Asus Memo Pad 7 con Android 5.0.

**Versión 1.4.18 (1503)**

* Zendesk #3324: La creación de informes de anuncios de Primetime no realiza un seguimiento de las pausas publicitarias cuando no hay medios publicitarios en un VMAP.
Cuando una pausa publicitaria está vacía, los eventos de seguimiento de inicio y finalización de la pausa publicitaria no se rastreaban. Este problema se resolvió enviando pings de inicio de pausa publicitaria en pausas publicitarias vacías, como VMAP AdBreak, con un nodo de AdSource válido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) se ignora después de la llamada a MediaPlayer.reset() Este problema se resolvió al agregar setCCVisibility(Visibility.INVISIBLE); a la función reset() en la clase MediaPlayer.

* Zendesk #18328: Problema de fotogramas descartados en dispositivos Amazon Fire TV de segunda generación para el contenido con 60 FPS Este problema se resolvió aplicando el FPS codificado para la toma de decisiones sobre el tiempo de sueño y con una lógica de predicción de FPS mejor codificada.

**Versión 1.4.17 (1472)**

* Zendesk #2231 - Error devuelto al recuperar el manifiesto no disponible en MediaPlayerNotification Este problema se resolvió al incluir el cuerpo de respuesta del manifiesto cuando hay un error de análisis.

* Zendesk #17703 - VideoEngineView no evita capturas de pantalla durante la reproducción de vídeo El método setSecure ha estado disponible desde la API 17, pero como la API 17 cubre las versiones 4.2, 4.2.1 y 4.2.2, no se sabe cuál generará una excepción o si es específico del dispositivo. Este problema se resolvió ajustando VideoEngineView.setSecure en la cláusula try catch.

* Zendesk #17919: La búsqueda de contenido provoca un error de latido Se estaba produciendo un error de posición de datos de entrada no válido como resultado de la llamada de latido generada cuando la búsqueda se iniciaba después del anuncio previo a la emisión. Este problema se ha resuelto.

**1.4.16 bis** (1454 bis)

* Zendesk #18215: Algunos flujos AES no se pueden cargar.
Este problema se resolvió comprobando el tamaño de los metadatos DRM de perfil antes de cargar la clave AES.

**Versión 1.4.16 (1454)**

* Zendesk #3875 - Tab S se bloquea durante la reproducción Revirtiendo la dependencia de OKHTTP en el Auditude para CRS porque TVSDK ahora utiliza directamente httpurlconnection en lugar de curl. El problema se resolvió borrando las excepciones antes de realizar cualquier otra llamada JNI.

* Zendesk #4487 - Seguimiento del canal lineal de contenido El problema se resolvió permitiendo reiniciar el rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* Zendesk #17919 - Android - la búsqueda de contenido provoca un error de latido Se ha resuelto el problema cuando el latido está en estado de error cuando hay una búsqueda en un capítulo.

* Zendesk #18053 - Adobe Primetime se bloquea en Marshmallow El TVSDK se bloqueaba en el sistema operativo Android M cuando la biblioteca TVSDK usaba código de neón que hace la conversión de color YUV -> RGB. El problema se resolvió actualizando las funciones que causan este problema mediante el uso de una versión de código que no es de neón.

* Zendesk #18072 - Android M - Error en la aplicación Al comprobar si el perfil y el nivel son compatibles, se produce un bloqueo al llamar a las API MediaCodecList y MediaCodecInfo. El problema se solucionó cargando toda la información del códec con antelación para evitar llamar a estas API solo cuando se necesitaba información del códec.

* Zendesk #18074 - Subtítulos en árabe que no funcionan en Nexus con Android 6.0 El problema se resolvió al proporcionar compatibilidad con mapas de fuentes CTS para Android.

**Actualización de la versión 1.4.15 (1438)**

* Zendesk #17437: Largo retraso en el inicio del contenido de VOD con algunos flujos AES.
Para resolver este problema, si hay varias claves enumeradas en el manifiesto, descargue todas las claves AES en paralelo.

**Versión 1.4.15 (1435)**

* Zendesk #4278: destellos en los decodificadores de Android cuando cambia la velocidad de bits adaptable (ABR).
La corrección consistió en agregar compatibilidad con el conmutador ABR sin problemas con el último códec de medios de Android.

* #17063 de Zendesk: La llamada a mediaPlayer.reset() provoca un error de restablecimiento del motor de vídeo.
La corrección consistió en incluir el MediaErrorCode original de VideoEngineExceptions al enviar ErrorEvents.

* Zendesk #17130 - Una breve pero notable pausa al cambiar la velocidad de bits visto en FireTV.
(Igual que #4278 anterior) La corrección consistió en añadir compatibilidad con el conmutador ABR sin problemas con el último códec de medios de Android.

* #17666 de Zendesk: marcadores de publicidad adicionales, inesperados o sin anuncios al reanudar el contenido.
La corrección era un problema al hacer prepareToPlay en contenido de vídeo bajo demanda (VOD), la búsqueda inicial se realiza en la hora local en lugar de la hora virtual.

* Zendesk #17437: Largo retraso en el inicio del contenido de VOD con algunos flujos AES.
La corrección consistió en descargar todas las claves AES en paralelo cuando se enumeran varias claves en el manifiesto.

* Zendesk #17851 - Android TV - Black Frame during ABR La solución era especificar KEY_MAX_WIDTH y KEY_MAX_HEIGHT para habilitar la reproducción adaptativa.

**Versión 1.4.14 (1415)**

* Zendesk #3875 - Tab S se bloquea durante la reproducción.
Se necesitaba una corrección adicional para evitar el bloqueo.

* Zendesk #17245: La alternativa en Android TV no funciona.
Se ha corregido un problema adicional en el cual la reproducción se bloqueaba cuando la opción de reserva estaba habilitada y la respuesta de VMAP tenía una pausa publicitaria vacía.

**Versión 1.4.14 (1412)**

* Zendesk #17245 - La alternativa en Android TV no funciona.
Se ha eliminado una restricción para deshabilitar el reempaquetado creativo en los anuncios de reserva.

**Versión 1.4.13 (1388)**

* Zendesk #3502: la compatibilidad con la conmutación por error basada en el cliente HLS durante una pausa publicitaria permite la conmutación por error al manifiesto principal cuando se produce un error de perfil en directo durante el período de pausa publicitaria.

* Zendesk #3875 - Tab S se bloquea durante la reproducción Para resolver el conflicto entre HttpUrlConnection y cURLm, utilice una biblioteca de terceros.

* #4450 de Zendesk: configuración de problemas, metadatos personalizados para una sola ubicación en un solucionador de contenido. Añada un configurador a la configuración de Oportunidades.

**Versión 1.4.12 (1388)**

* Zendesk #2751 - CSAI y CRS | Mejorar: Gestionar elementos dinámicos en determinadas URL de archivos multimedia.
Se ha actualizado el servicio de reempaquetado creativo para que gestione correctamente los anuncios con direcciones URL creativas dinámicas.

* Zendesk #3965: Volver a la reproducción normal desde el trickplay resulta en un salto hacia adelante un poco antes de iniciar la reproducción.
   * La corrección incluye que TVSDK devuelva el tiempo antes del cambio de tasa hasta que se actualizan todas las variables, en lugar de intentar calcular GetStreamTime.
   * Se corrigió un bloqueo al cambiar la velocidad de reproducción con trucos cerca del final del flujo.
   * Se corrigió el cálculo de tiempo actual durante la reproducción con trucos.

* Zendesk #3978 - Trickplay en 8x y 16x se congela con frecuencia.
   * Elija siempre el perfil de juego con la velocidad de bits más baja para evitar el almacenamiento en búfer constante.
   * Aumente el intervalo de omisión de fotogramas para una alta tasa de trucos.
   * Se ha corregido un problema que hacía que el búfer siguiera creciendo después de alcanzar su longitud objetivo durante el juego de trucos.

* Zendesk #3992 - Velocidades adicionales de Trickplay.
TrickPlay se ha actualizado para aceptar tarifas superiores a 16x; +/- 32, +/-64 y +/-128 ahora también están permitidos.

* #4007 de Zendesk: Interpretación del objeto GEOB como parte de los metadatos de la cronología (Android y web).
Se añadieron las API setByteArray y getByteArray.

* PTPLAY-7301: instantánea al inicio en punto de acceso aleatorio.
Instant On se ha actualizado para permitir un punto de partida distinto de cero.

**Versión 1.4.11 (1363)**

* Zendesk #2076: tartamudeo frecuente al reproducir vídeo en Motorola Xoom con Android 4.0.3 Se han agregado dispositivos a la lista de permitidos para evitar que intenten reproducir contenido de alto perfil.

* Zendesk #2197 - `[Ads]` Seguimiento de errores y envío de OperationFailedEvent con notificación de advertencia.

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` la macro no se rellena
   * el código de error 400 se expone si el anuncio en línea tiene un error creativo.
   * `[ERRORCODE]` La macro tendrá codificación URL

**Versión 1.4.10 (1354)**

* Zendesk #2941: Los activos en directo no tienen &quot;0&quot; en el rango de búsqueda. Anteriormente, había un búfer de 3 segmentos al buscar el principio de una emisión en directo, ahora es posible buscar el principio de una emisión en directo (es decir, el inicio del primer segmento).

* Zendesk #3169: Actualización del reproductor de referencia con la integración de Adobe Analytics El reproductor de referencia se ha actualizado con la biblioteca de Adobe Analytics como implementación de ejemplo.
* Zendesk #3299 - Comportamiento inexplicable del juego de trucos
   * Se ha corregido un error por el cual volver al estado de reproducción después de detener la reproducción con truco podía tardar varios segundos (a veces más de 25 segundos).
   * Se ha corregido un error por el cual invocar el truco para reproducir por segunda vez en el mismo medio puede provocar que el flujo se congele en el momento actual.
* Zendesk #3433 - Android y Flash - Problemas con los subtítulos

GetLine para WebVTT no respetaba un &lt;cr>&lt;lf> longitud ajustada para un paquete; el último pie de ilustración podría contener caracteres de subtítulos anteriores.

* PTPLAY-6243: mejore el reproductor de referencia para capturar información de depuración

Los reproductores de referencia de muestra de Android se han mejorado con una opción para activar los registros de depuración y enviar por correo electrónico los resultados. Esta opción se encuentra en el menú Registro del reproductor de referencia.

**Versión 1.4.9 (1332)**

* #2649 de Zendesk: la finalización del búfer se produce antes de que el búfer inicial esté lleno

Después de una búsqueda, caso posible en el que el motor de vídeo establece el estado en REPRODUCIENDO antes de que el presentador de vídeo esté listo para reproducir. Se produce cuando el estado del búfer es alto antes de la búsqueda. Solucionar notificando al motor de vídeo que el estado del búfer es bajo. Con el motor de vídeo en un estado de búfer bajo, la llamada a Reproducir provoca un cambio de estado en ALMACENAMIENTO EN BÚFER en lugar de REPRODUCIR. La reproducción se reanuda cuando el estado cambia a REPRODUCIENDO.

* Zendesk #2846 - Solicitud de mejora: Proporciona la capacidad de establecer diferentes cadenas de usuario-agente para las llamadas realizadas por la biblioteca del Auditude

Se ha añadido una nueva API para establecer el agente de usuario para las llamadas relacionadas con publicidad, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Si no se establece ningún agente de usuario, se utilizará el predeterminado. Esto solo afecta al agente de usuario para llamadas relacionadas con anuncios; el agente de usuario para llamadas de medios no cambia y es &quot;Adobe Primetime&quot;+&lt;default useragent=&quot;&quot;>.

**Versión 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Error con local ... Si falla la carga del manifiesto en FragmentedHTTPStreamer::ThreadParseManifest(), compruebe si el dominio URL es localhost y, si es así, cambie el dominio a 127.0.0.1 y recupere ThreadParseManifest.
* Zendesk #3072 - Cambio automático a velocidades de bits más bajas. Se ha cambiado el cálculo de longitud de búfer para omitir la carga PTS cero.
* Zendesk #3168 - Los subtítulos WebVTT solo se muestran durante los primeros 10 segundos.
* Zendesk #3193: Se ha añadido la solicitud de una API de cambio de perfil en TVSDK, PlaybackEventListener.onProfileChanged().

**Versión 1.4.7 (1311)**

* Zendesk #2197 - Seguimiento de errores publicitarios. Se ha añadido una notificación para el recurso que no se ha podido cargar el manifiesto
* Zendesk #2575: PSDK ignora el anuncio en flujo personalizado de MARK antes del vídeo
* Zendesk #2719: Gane la muerte con anuncios de audiencia, seguimiento de señalización fijo cuando se redirige a una dirección URL relativa en el complemento de audiencia
* #2760 de Zendesk: etiqueta DISCONTINUITY ignorada durante el modo TrickPlay
* Zendesk #2805: error del reproductor al principio de la reproducción, la misma solución que Zendesk #2719
* Zendesk #2817 - Reproductor de Android: El reproductor a veces se bloquea y deja de reproducir, corregido ampliando los búferes de decodificación de 2.0 a 3.0 segundos
* Zendesk #2839 - ¿Adobe Primetime PSDK es compatible con chipsets ARMv8?, se agregó una corrección para el bloqueo que se encuentra en el Galaxy S6.
* Zendesk #2885: Reproducción de Auditude que se bloquea, la misma solución que Zendesk #2719
* Zendesk #2895: error de HLS en directo de forma consistente tras 10 minutos de reproducción
* Zendesk #2925 - Comentarios con respecto a Android dev build (1.4.5), en ciertos dispositivos cuando ponemos el paquete en cola de entrada, si el PTS es negativo, el decodificador entra en un estado extraño que siempre obtenemos un PTS de salida negativo para paquetes futuros. La corrección establece el PTS de entrada en cero si es negativo para evitar este problema.
* PTPLAY-4645: desactiva la compatibilidad con cifrado RC4 en openssl. Hay exploits conocidos para RC4. Esto significa que si se intenta conectar con un servidor que sólo admite RC4, se producirá un error.

**Versión 1.4.6 (1282)**

* Zendesk #2192 - La tasa de bits no siempre disminuye en condiciones de red deficientes, lo que se corrige eliminando la implementación rápida del switch.
* Zendesk #2631 - Subtítulos en árabe en Android: El texto en varias líneas aparece cortado, corregido ajustando el tamaño de la fuente para las fuentes árabes.
* Zendesk #2844 - El almacenamiento en búfer de la nota 4 y el tiempo de descarga del fragmento no son precisos.

Este problema se solucionó añadiendo latencia entre las descargas de segmentos de vídeo en el cálculo del ancho de banda y haciendo que la lógica de cálculo del tiempo de descarga utilice el tiempo de ciclo de solicitud completo.

* Zendesk #2908 - Subtítulos en árabe que no funcionan en los Nexust 5, 6 y 7, corregidos mediante la adición de 2 fuentes de reserva más para los scripts en árabe.
* PTPLAY-4627: actualizar el appsdk de Nielson a la versión 1.2.3.7
* PTPLAY-5084: compatibilidad con la conmutación por error de la actualización del manifiesto maestro activo

**Versión 1.4.5 (1248)**

* Zendesk #1757: solo se reproduce audio o el reproductor se bloquea para algunos perfiles de velocidad de bits de vídeo, Nexus 4 y Nexus 7 se bloquean
* #2072 de Zendesk: Los metadatos cronometrados para AdEvent no contienen una URL completa solo &quot;http&quot;
* Zendesk #2192 - La tasa de bits no siempre baja en condiciones de red deficientes
* Zendesk #2256: acceso a la lista de reproducción maestra, PSDK actualizado para enviar eventos de metadatos cronometrados para las etiquetas suscritas en la lista de reproducción maestra.
* Zendesk #2269: aparecen dos idiomas de subtítulos diferentes en la pantalla al mismo tiempo con WebVTT
* Zendesk #2417: El reproductor intentaba descargar subtítulos antes de que comenzara la reproducción; WebVTT usaba la variable de número de segmento incorrecta para la coincidencia de número de segmento. El error solo aparecía en los medios que tenían índices de segmento a partir de cero.
* Zendesk #2470: PSDK no vuelve del estado SUSPENDIDO cuando se produce un cambio en la velocidad de bits tras la suspensión. En una situación especial en la que RestoreGPUResource llama a la búsqueda inteligente (restaura el reproductor desde el estado de suspensión) y se detecta antes el cambio de flujo, la búsqueda inteligente no se puede completar y provoca un almacenamiento en búfer constante.
* Zendesk #2451 - Subtítulos &#39;bottom inset&#39;, se ha agregado el parámetro &#39;bottomInset&#39; al código de subtítulo
* #2480 de Zendesk: Desactivación de la optimización del redireccionamiento HTTP 302. Se ha agregado compatibilidad para configurar la propiedad useRedirectUrl
* Zendesk #2486 - señalizaciones de terceros
* Zendesk #2547 - Subtítulos en árabe: El texto debe estar alineado y justificado a la derecha

**Versión 1.4.4 (1195)**

* Zendesk #1158 - La reproducción falla en Huawei Valiant (Y301A1)
* Zendesk #1709 - Tamaño de medios incorrecto y vídeo estirado
* Zendesk #1757: solo se reproduce audio después de cambiar de perfil entre flujos con datos idénticos de spa/apps
* Zendesk #2095: El estado HTTP 307 (redirección) hace que el reproductor de Adobe detenga la reproducción
* Zendesk #2126 - Falta el evento TimedMetaData para el último ADEVENT, las etiquetas suscritas que existen después del último segmento no se notificaron a PSDK desde AVE
* Zendesk #2227 - Bloqueos en VideoEngine nativeReset y nativePause
* Error #3921755: Actualización de la biblioteca OpenSSL a la versión 1.0.1L.

**Versión 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Encendido y apagado de subtítulos
* PTPLAY-1818: el truco de rebobinado se detiene en el anuncio en lugar de rebobinarlo
* PTPLAY-2736: se muestra en la pantalla un subtítulo WebVTT que se mostraba anteriormente cuando termina de reproducirse un flujo con subtítulo WebVTT
* PTPLAY-3773: no se reproduce un anuncio mid-roll cuando se inicia la reproducción del flujo después de la posición del anuncio

**Versión 1.4.2**

* Zendesk #1561 - Soporte de failover basado en el cliente HLS en primetime. Utilizará la fecha y hora del programa para solucionar el problema de failover
* #1590 de Zendesk: LoadInfo.MediaDuration siempre es 0 (no se corrige solo para audio)
* Zendesk #1626 - Posible fuga de memoria en el reproductor. No es una fuga de memoria real, el problema era con el Historial de notificaciones que guardó las últimas 1000 notificaciones, esto se ha reducido a 100.
* Zendesk #2192 - La tasa de bits no siempre baja en condiciones de red deficientes

**Versión 1.4.1 (1121)**

* Zendesk #1951: Bloqueo en VideoEngine.nativeReset() en dispositivos 4.0.x
* Zendesk #2064: SIGSEGV nativo bloqueado en dispositivos Android específicos basados en Intel
* Zendesk #2075: Lockup en VideoEngine.nativeReleaseGPUResource en dispositivos 4.0.x Nota: Esta compilación es &#42;&#42;&#42;obligatorio&#42;&#42;&#42; para compatibilidad con Android 5.0 (Lollipop)
* Zendesk #1513 - Soporte para Android Lollipop
* Zendesk #1709 - Tamaño de medios incorrecto y vídeo estirado
* Los subtítulos de #1871 - WebVTT desaparecen ocasionalmente y vuelven a aparecer cuando se visualiza una emisión en directo con subtítulos WebVTT
* Zendesk #1996: no se ven marcadores de cronología en PSDK 1.4.0
* Zendesk #2046: Se ha corregido el bloqueo de los flujos en directo con PSDK 1.4.1.1113 cuando la audiencia no devolvía anuncios
* Error #3769657: actualizar la versión de curl a 7.38.0
* PTPLAY-1575: cuando la reproducción ABR comienza con una secuencia de audio solamente y luego cambia a una secuencia de audio/vídeo, el vídeo nunca se procesa mientras continúa el audio
* PTPLAY-2499: actualización a OpenSSL a la versión 1.0.1j para abordar vulnerabilidades recientes
* PTPLAY-2632: el vídeo no se recupera tras la emisión del anuncio en Android Lollipop
* PTPLAY-2678: Se detiene el vídeo durante las pruebas de longevidad en directo en Android Lollipop

**Versión 1.4.0**

* Zendesk #1024: función para eliminar el anuncio del flujo a través del manifiesto
* Zendesk #1293 - Problema de selección de seguimiento de subtítulos.
* Zendesk #1590 - LoadInfo.MediaDuration siempre es 0, mediaDuration ahora muestra el valor correcto.
* Zendesk #1629: el reproductor/aplicación se bloquea al final de la reproducción del anuncio en el Galaxy S4
* Zendesk #1674 - ClosedCaption No aparece, pantalla correcta de 708 subtítulos cuando faltan 0x03 códigos ETX.
* PTPLAY-2157: los captadores devolvieron los estilos predeterminados de subtítulos aunque se hayan establecido y verificado visualmente estilos diferentes en el flujo. Las propiedades de estilo Subtítulos ahora mostrarán el valor en el que se han establecido.

## Problemas conocidos en 1.4 {#known-issues-in}

**Versión 1.4.31**

* PTPLAY-16803: los subtítulos no funcionarán con contenido de solo audio, ya que el sistema de subtítulos necesita vídeo para funcionar. Sin vídeo, no hay ninguna dimensión de ventanilla móvil y, sin esta, no podemos mostrar gráficos para los subtítulos.
* PTPLAY-1634: la misma etiqueta suscrita tiene diferentes marcas de tiempo en diferentes ventanas activas. Cuando la ventana activa se mueve, la misma etiqueta de ellos debe tener las mismas marcas de tiempo. Sin embargo, a veces incluso las mismas etiquetas tienen marcas de tiempo diferentes.
* PTPLAY-3197 - Se estrelló con la señal 11 SIGSEGV error en el dispositivo Acer Iconia después de ~ 1 hora de reproducción continua
* PTPLAY-3310: con un poco de audio de velocidad de bits más baja, el audio se vuelve entrecortado/distorsionado en Acer Iconia
* PTPLAY-3355 - WIN DEATH se estrelló en Motorola Xoom con 4.0.x después de ~ 1 hora de reproducción continua.
* PTPLAY-3557: el rebobinado en una pausa publicitaria está causando la finalización del flujo
* PTPLAY-7079: La ventana de reproducción en el cliente de Android no funciona con Secure Stop/Hard Stop
* Error #3760144: la resolución puede cambiar o parecer que pulsa cuando el flujo está en pausa en algunos dispositivos como Kindle Fire 7 y Samsung Galaxy Nexus. Solo observable bajo estrecha inspección
* Error #3761170: seekToLocal en Live with Ads no puede buscar contenido de anuncios, lo mejor es utilizar las API currentTime para emisiones en directo
* Error #3763370: Las transmisiones en directo con anuncios ocasionalmente muestran dos marcadores de publicidad muy juntos cuando solo debería haber uno. Estos marcadores de publicidad representan el mismo anuncio y solo se reproducirá uno
* Error #3763373: el marcador de anuncio puede desaparecer brevemente al buscar más allá de un anuncio en flujos de VOD. El marcador de anuncio se restaura y no hay ningún otro efecto adverso en la cronología
* Algunos dispositivos tienen problemas de reproducción conocidos. Consulte [Problemas conocidos del dispositivo en 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementación de referencia: El juego de trucos no se implementa en la aplicación de ejemplo
* En algunos dispositivos Android TV se puede ver un marco negro debido a un restablecimiento del decodificador en los siguientes puntos de transición:
   * entrada y salida del modo trickplay
   * cambiar entre pistas de audio de enlace tardío
   * de un anuncio al contenido principal.

**Versión 1.4.23**

* Subtítulos no funcionará con contenido de solo audio porque el sistema de subtítulos necesita vídeo para funcionar. Sin vídeo, no hay ninguna dimensión de ventanilla móvil y, sin ella, no se puede mostrar ningún gráfico para los subtítulos.
* A partir de la versión 1.4.23, TVSDK no admitirá Gingerbread OS 2.3. Esto se debe a que TVSDK utilizó las siguientes bibliotecas privadas de Android para recopilar información de hardware sobre dispositivos con el sistema operativo Gingerbread:

   * `libstagefright.so`
   * `libcutils.so`

En la versión de Android N, Google ha eliminado el acceso a estas bibliotecas privadas. Actualmente, el sistema operativo Gingerbread representa menos del 1% de la cuota de mercado de Android OS a nivel mundial, por lo que, después de la versión 1.4.23, el sistema operativo Gingerbread ya no será compatible con el TVSDK.
Si utiliza la versión 1.4.23 (que incluye compatibilidad con Android N) o posterior:
* Actualice las aplicaciones para utilizar minSdkVersion versión 11.
* Si el usuario final ejecuta OS 2.3, la versión del SDK es inferior a la minSdkVersion de la aplicación. El sistema anula la instalación o actualización de la aplicación.
* Si el usuario final ejecuta una versión superior a OS 2.3, la aplicación se instalará correctamente.

Si actualiza minSdkVersion:

* Si el usuario final ejecuta OS 2.3, la aplicación está instalada pero la reproducción no funciona.
Esto se aplica tanto a la actualización como a la instalación nueva.
* Si el usuario final ejecuta un sistema superior a OS 2.3, la aplicación se instala correctamente y el contenido se reproduce correctamente.

**Versión 1.4.22**

* La salida anticipada de los anuncios no funciona con algunos de los anuncios mid-roll cuando las etiquetas splice-out y splice-in están demasiado cerca unas de otras.

**Versión 1.4.2**

* El rebobinado en una pausa publicitaria está provocando que la emisión se complete.

El Reproductor multimedia envía incorrectamente MediaPlayer Player PlayerState.Complete durante la operación de rebobinado de Trick Play cuando llega al límite del anuncio. El reproductor debe ignorar este evento en el modo de reproducción con trucos; de lo contrario, el SDK gestiona el estado correctamente.

**Versión 1.4.0 (1086)**

* PTPLAY-1634: la misma etiqueta suscrita tiene diferentes marcas de tiempo en diferentes ventanas activas. Cuando las ventanas activas se mueven, la misma etiqueta de cada una de ellas debe tener las mismas marcas de tiempo. Sin embargo, a veces incluso las mismas etiquetas tienen marcas de tiempo diferentes.
* PTPLAY-2541: COMPONENT_CREATION_FAILURE se ve a veces después de varios cambios a/desde la secuencia alternativa en interrupciones
* #3726865 de errores: Si un flujo LBA de varias velocidades de bits comienza desde un flujo de solo audio, el vídeo no se mostrará si se cambia a un flujo de audio/vídeo. Si se inicia desde un flujo de audio/vídeo, no se mostrará este problema y se puede alternar correctamente entre flujos de audio y audio/vídeo
* Error #3760144: la resolución puede cambiar o parecer que pulsa cuando se pausa un flujo en algunos dispositivos como Kindle Fire 7 y Samsung Galaxy Nexus. Solo observable bajo estrecha inspección
* Error #3761170: seekToLocal en Live with Ads no puede buscar contenido de anuncios; es mejor utilizar las API currentTime para flujos en directo
* Error #3763370: Las transmisiones en directo con anuncios ocasionalmente muestran dos marcadores de publicidad muy juntos cuando solo debería haber uno. Estos marcadores de publicidad representan el mismo anuncio y solo se reproducirá uno
* Error #3763373: el marcador de anuncio puede desaparecer brevemente al buscar más allá de un anuncio en flujos de VOD. El marcador de anuncio se restaura y no hay ningún otro efecto adverso en la cronología
* Algunos dispositivos tienen problemas de reproducción conocidos. Para obtener más información, consulte [Problemas conocidos del dispositivo en 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementación de referencia: El juego de trucos no se implementa en la aplicación de ejemplo.

## Problemas conocidos del dispositivo en 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Solución |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | Se espera un retraso de ABR ya que está reiniciando el decodificador. |  |  |
| HTC Desire (diferente de HTC Desire HD) | QSD8250 | No se puede reproducir el vídeo. Devuelve el error VIDEO_PROFILE_NOT_SUPPORTED. | Desire no proporciona un decodificador de HW adecuado. Le da el decodificador SW de Stagefright. | Reinicie el dispositivo. |
| HTC EVO 4G | QSD8650 | No hay decodificador de hardware. | Qualcomm no tiene un decodificador de hardware. | Actualización a Android 4.x. |
| Kindle FireSystem versión 6.0 | TI OMAP4 | No reproduce secuencias HLS. El vídeo en AIR no funciona. |  | Actualice a la versión 6.3 del sistema. |
| Kindle Fire HD | TI OMAP4 | Puede entrar en un estado en el que no pueda reproducir vídeo. Devuelve los errores VIDEO_PROFILE_NOT_SUPPORTED y UNRECOVERABLE_ERROR. | El decodificador de HW entra en un estado irrecuperable cuando la aplicación no apaga el decodificador de HW por completo, por ejemplo, después de encontrar un bloqueo. También sucede en aplicaciones nativas en el dispositivo. | Reinicie el dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE se bloquea después de varios cambios ABR. |  |  |
| Motorola Atrix | Tegra2 | Problemas generales de rendimiento con AVE, a diferencia de AIR. La sincronización de audio/vídeo se interrumpe, la reproducción de vídeo se bloquea después de reproducir entre 9 y 15 minutos. Bloqueos. | Posiblemente relacionado con openGLES que habilitamos en AIR. Estoy siendo investigado. |  |
| Nexus 7 (2ª generación) | S4Pro APQ8064 (Qualcomm) | El dispositivo se bloquea cuando una película se pone en pausa durante más de 30 minutos. | Problema del dispositivo que se ha notificado a Google. | La aplicación debe agotar el tiempo de espera para no permitir un estado de pausa largo. |
| Nexus S (GB) | Colibrí | No se puede reproducir ningún vídeo con el decodificador HW. | No hay ningún decodificador de hardware basado en Stagefright en Nexus S, por lo que para Android 2.3 utilizamos un decodificador SW. | Actualice a ICS. |
| Nexus S (ICS) | Colibrí | El vídeo parpadea ocasionalmente. | Los datos incorrectos pueden provocar que el descodificador entre en un estado incorrecto. | Reinicie el dispositivo. |
| Nook tabletAndroid OS: 2.3 | TI OMAP 4 | El vídeo no se reproduce y la aplicación se bloquea. | Stagefright entra en un estado inestable después de ejecutar la aplicación varias veces. Las llamadas al reproductor de medios::QueryCodecs se bloquean. | Reinicie el dispositivo para restablecer el estado. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | No se puede instalar la aplicación SampleMediaPlayer. | Utiliza ARM v6 en lugar del chipset ARM v7 más común. FP/AIR no es compatible con este dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | No se puede reproducir el vídeo. | Este chipset es un decodificador desconocido para Android pre-ICS en AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | El rendimiento de vídeo no está a la altura de este dispositivo. | El descodificador de hardware devuelve fotogramas descodificados con el PTS incorrecto. Parece ser que el descodificador utiliza el tiempo de descodificación en lugar del tiempo de presentación. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | TI OMAP4 | Se bloquea al iniciar el vídeo. |  | Actualice a Android 2.3.7 o 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | De forma intermitente, el vídeo se bloquea y solo se reproduce el audio, por lo que deja de responder. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | El vídeo se bloquea. | Investigando. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | La transición MBR puede tardar hasta tres segundos. | Como solución para los bloqueos de MBR, reiniciamos el decodificador para cada interruptor de flujo, que puede tardar hasta tres segundos. |  |
| Samsung Galaxy Y |  | No se puede instalar la aplicación SampleMediaPlayer. | Utiliza ARM v6 en lugar del chipset ARM v7 más común. FP/AIR no es compatible con este dispositivo. |  |
| Xoom | Tegra | Se pierden algunos fotogramas para cambiar. El descodificador no se reinicia. | limitación OMXAL. |  |

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
