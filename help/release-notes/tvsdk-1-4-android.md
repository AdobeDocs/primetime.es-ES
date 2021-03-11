---
title: Notas de la versión de TVSDK 1.4 para Android
description: Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 1.4.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---


# Notas de la versión de TVSDK 1.4 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 1.4.

## Nuevas funciones {#new-features}

**Versión 1.4.43**

**Carga de publicidad segura a través de HTTPS**

Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad primetime y CRS a través de HTTPS.

**alwaysUseAudioOutputLatency(boolean val) en la clase MediaPlayer**

Cuando se establezca este parámetro, utilice la latencia de salida de audio en el cálculo de la marca de tiempo del audio.

Acepta un valor de parámetros booleanos. Si su valor es `True`, el cliente utiliza la latencia de salida de audio en el cálculo de la marca de tiempo del audio.

**Versión 1.4.42**

**Inserción parcial de Ad-Break:**
experiencia parecida a la TV de unirse en mitad de un anuncio sin activar el seguimiento del anuncio parcialmente visto.
Ejemplo: El usuario se une en el medio (a los 40 segundos) de una pausa publicitaria de 90 segundos que consta de tres anuncios de 30 segundos. Pasarán 10 segundos desde el segundo anuncio de la pausa.
* El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.
* Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Se activan los rastreadores solo del tercer anuncio.

**Versión 1.4.41**

No hay nuevas funciones.

**Versión 1.4.40**

No hay nuevas funciones.

>[!NOTE]
>
>No necesitará los cambios de API si está en una versión anterior a la 1.4.39.

**Versión 1.4.39**

* TVSDK está certificado con VHL 2.0.1 y con VHL 2.0.1 con Nielsen.
* Android TVSDK se ha actualizado para realizar solicitudes CRS desde el nuevo host de Akamai `primetime-a.akamaihd.net`.
* La nueva configuración de nombre de host proporciona la entrega de recursos CRS a través de HTTP y HTTPS (SSL) a buena escala.
* TVSDK es compatible con la versión Android Oreo.
* Se agrega una nueva función a la clase `AdClientFactory` para que admita el registro de varios Detectores de oportunidad:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   Esto debería devolver una matriz de PlacementOportunityDetector. Ahora puede registrar varios Detectores de oportunidades. Por ejemplo, para la función de salida de publicidad anticipada, se necesitaban dos detectores de oportunidad: uno para la inserción de publicidad y otro para la salida anticipada del anuncio. Debe implementar esta nueva función solo impacto si ha implementado su propio AdvertisingFactory (y no utilizando DefaultAdvertising Factory). Para obtener el comportamiento existente, debe crear un solo detector de oportunidad, como en la función createOportunityDetector() , y colocarlo en una matriz y devolver:

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
>No necesitará los cambios de API si está en una versión anterior a la 1.4.39.

**Versión 1.4.36**

Corrección de errores para la omisión de contenido en Android.

**Versión 1.4.35**

* **Información de publicidad de red**

   Las API de TVSDK ahora proporcionan información adicional sobre respuestas VAST de terceros. El ID de anuncio, el sistema de publicidad y las extensiones de publicidad VAST se proporcionan en la clase NetworkAdInfo a la que se puede acceder mediante la propiedad networkAdInfo de un recurso de publicidad. Esta información se puede utilizar para la integración con otras plataformas de Ad Analytics, como **Moat Analytics**.

**Versión 1.4.31**

**Compatibilidad con varias CDN para anuncios CRS**
* De forma predeterminada, todos los recursos transcodificados se alojan en CDN de propiedad de Adobe en Akamai. Con la última versión, el servicio de reempaquetado creativo de Adobe (CRS) ofrece la capacidad de cargar los elementos creativos transcodificados en varias CDN, según lo especificado por el cliente.
* Se añaden nuevas API al TVSDK para permitir la especificación de la URL creativa CRS final cuando no se utiliza la URL predeterminada. Consulte la documentación para aprender a utilizar estas nuevas API.

**La versión 1.4.18**
 de Primetime Android TVSDK ahora es compatible con los creativos de Javascript VPAID 2.0 para permitir una rica experiencia de publicidad interactiva en flujo. Para obtener más información sobre VPAID 2.0, consulte [Compatibilidad con anuncios VPAID](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Versión 1.4.17**

El AC-3 5.1 solo es compatible con Amazon FireTV.

**Versión 1.4.11**

* **Abandono de anuncio, encadenamiento de margaritas en la lógica de selección de anuncios (Zendesk #3103**  Para anuncios VAST (creativos) con la regla de reserva habilitada, TVSDK trata un anuncio con un tipo MIME no válido como un anuncio vacío e intenta usar anuncios de reserva en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Ad fallback for VAST and VMAP ads](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Video Heartbeats Library (VHL) actualizado a la versión 1.5**
   * Capacidad para enviar metadatos con el inicio de vídeo o el inicio de vídeo/anuncio/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño

**Versión 1.4.7**

* **Asistencia** de individualización localCompatibilidad con instalaciones locales del servidor de individualización de Adobe para personalizar la solicitud de personalización del cliente para ir a un punto final diferente.

**Versión 1.4.6**

* **Encriptado AES de muestra (requiere la versión de Flash Player 17.0.0.134)**Ahora se admite el cifrado AES basado en muestras.

**Versión 1.4.2**

* **Actualización de Video Heartbeats Library (VHL) a la versión 1.4.0.1**

   * Se ha agregado la capacidad de agrupar diferentes casos de uso de análisis, de otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete . La pausa publicitaria se infiere de las llamadas de método trackAdStart y trackAdComplete .
   * La propiedad playhead ya no es necesaria al rastrear anuncios.

* **Integración de SDK** de NielsenEl SDK de TVSDK ahora admite el envío de información de seguimiento de usuarios al SDK de Nielsen sin ninguna integración personalizada.

**Versión 1.4.0**

* **Señalización de interrupción con** reemplazo de contenido alternativoComo parte de la actualización 1.4 de TVSDK, ahora TVSDK también admite entrar y salir de interrupciones regionales con contenido lineal. Ahora, el TVSDK puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de bloqueo incluso cuando se muestra una programación alternativa en lugar de la programación original.

* **Elimine/reemplace C3** AdsAhora, no se necesita ningún trabajo de preparación adicional para insertar dinámicamente nuevos anuncios en recursos de vídeo bajo demanda (VOD) que salen de la ventana C3. El SDK de TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar de forma dinámica nuevos anuncios. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se emite durante la emisión y se baja inmediatamente para utilizarlo como contenido bajo demanda sin el tiempo adecuado para &quot;limpiar&quot; el recurso.

* La interfaz PlaybackEventListener tiene un nuevo método llamado onReplaceMediaPlayerItem, que puede utilizar para detectar un nuevo evento, `ITEM_REPLACED`. Este evento se envía cada vez que se reemplaza una instancia de MediaPlayeritem en MediaPlayer. La aplicación cliente que implementa este PlaybackEventListener debe implementar o anular este nuevo método.
* AdClientFactory tiene una nueva función agregada a la clase para registrarse en varios detectores de oportunidad:

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

## Cambios del SDK de TVSDK para 1.4 {#tvsdk-changes}

* La interfaz PlaybackEventListener tiene un nuevo método llamado onReplaceMediaPlayerItem, que puede usar para escuchar un nuevo evento, ITEM_REPLACED. Este evento se envía cada vez que se reemplaza una instancia de MediaPlayeritem en MediaPlayer. La aplicación cliente que implementa este PlaybackEventListener debe implementar o anular este nuevo método.

* AdClientFactory tiene una nueva función agregada a la clase para registrarse en varios detectores de oportunidad:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Por ejemplo, para la función de salida de publicidad anticipada, necesita dos Detectores de oportunidad: uno para la inserción de publicidad y otro para la salida anticipada de un anuncio.

Para anular esta nueva función, cree un único detector de oportunidades, coloque en una matriz y devuelva:

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
>Las siguientes funciones son **no** compatibles con el TVSDK:
>
>* Movimiento lento, en cualquier plataforma o versión.
>* Juego de trucos en vivo.


**Versión 1.4.43**

TVSDK 1.4.43 se ha certificado con dispositivos Android con Android 6.0.1/ 7.0 y 8.1 (Oreo).

* **Versión 1.4.23:**

   * TVSDK 1.4.23 se ha certificado para dispositivos Android con Android N.

* **Versión 1.4.18:**

   * Primetime está certificado para Amazon Fire TV.
   * VPAID 2.0 solo es compatible con dispositivos con Android 4.0 y versiones posteriores.

## Problemas resueltos en 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Se recomienda encarecidamente a todos los clientes de TVSDK que utilicen CRS que actualicen a TVSDK 1.4.39 o a la versión más reciente en iOS y Android. Esta actualización sustituye a la implementación de aplicación existente. Después de la actualización, compruebe las solicitudes de URL creativas de CRS en una herramienta de proxy (por ejemplo, Charles) para verificar que la versión en la ruta refleja la versión 3.1. Por ejemplo:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versión 1.4.43**

* Ticket #27143 - No se puede reproducir la pista de audio 5.1 en dispositivos FireTV

   * TVSDK ahora puede reproducir audio AC3 en dispositivos FireTV. La reproducción siempre está en estéreo.

* ticket #33902 - Envío seguro de publicidad a través de HTTPS

   * Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad primetime y CRS sobre https.

* ticket #34493 - Retraso de audio Bluetooth

   * Se ha agregado `alwaysUseAudioOutputLatency` en la clase MediaPlayer, que cuando se establece, resultará en el uso de latencia de salida de audio en el cálculo de la marca de tiempo del audio.

* ticket n.º 34949 - Nueva versión de Video Heartbeat Library (VHL) integrada.

**Versión 1.4.42 (1791)**

* Zendesk #33719: La velocidad de bits adaptable de FireTV 4k se escala lentamente. Se ha agregado compatibilidad con ABR para dispositivos FireTV 4K.
* Zendesk #33338:  resetDRM borra todos los datos de la aplicación.  Se han gestionado casos adicionales en los que excepciones en subprocesos que no son de TVSDK estaban provocando que se rellenaran las colas de operación de TVSDK.

**Versión 1.4.41 (1776)**

* Zendesk #33002 - Datos de recursos complementarios de TVSDK en Fire TV. Se ha implementado una nueva clase AdBannerAsset que devolverá los datos Companion como List &lt;AdBannerAsset> y AdAsset::id ahora es una cadena en lugar de ser larga.
* Zendesk #32821 - Android Primetime player se bloquea cuando encuentra Presentation Timestamp (PTS) para WWE. Este problema se corrigió en esta versión.
* Zendesk #33572 - Bloqueo de anuncio de VideoAnalyticsProvider. El uso de la combinación correcta de la versión conjunta del SDK VHL+Nielsen de VideoHeartbeat.jar ha corregido este problema.
* Zendesk #33355 - Fire TV: Anule 15 segundos el número. No hay ninguna corrección por parte de TVSDK y los clientes están verificando esto en su End y en terceros.

**Versión 1.4.40 (1764)**

* Zendesk #33068 - Problema de sincronización de labios de Amazon en el nuevo dispositivo. El problema de sincronización de vínculos se ha corregido en esta versión.
* Zendesk #32215 - Problemas de seguridad de Android TVSDK 1.4.38 `[Hotlist]`. Actualizado a los últimos OpenSSL-1.1.0 y curl-7.55.1.
* Zendesk #32920 - Pantalla en blanco dentro de una pausa publicitaria y sin finalización de pausa publicitaria. Se ha corregido un problema en el cual un contenedor de VPAID podía entrar en un estado inestable y se gestionaba un problema en el que los anuncios de VPAID de Facebook a menudo devolvían varios bloques de CDATA en un único \&amp;lt;AdParameters\&amp;gt; Nodo VAST.

**Versión 1.4.39 (1744)**

* Zendesk #28976 - La solicitud de licencia tarda más de un segundo. Mientras se ejecutan las llamadas de solicitud de licencia de DRM que utilizan el POST, Curl agrega &quot;Expect: Encabezado &quot;100-continue&quot;. Se ha eliminado el encabezado &quot;Expect:&quot; en TVSDK .
* Zendesk #27707 - Los entornos CSAI no respetan los marcadores CUE IN para una pronta devolución o retorno al contenido. Se ha proporcionado asistencia para múltiples generadores de oportunidades.

**Versión 1.4.38 (1722)**

* Zendesk #21590 - Rendimiento y seguimiento de vídeo en las últimas versiones de origen

Integración y certificación de VHL 2.0 en TVSDK para reducir la barrera en la implementación de VideoHeartbeatsLibrary disminuyendo la complejidad de las API.

* Zendesk #29688 - Soporte para clientes de Android O Beta.

Compatibilidad con TVSDK para la nueva versión beta de Android.

**Versión 1.4.36 (1713)**

* Zendesk #27392 - Omisión de contenido en Android

Para admitir el descifrado, el TVSDK para Android ampliaba incorrectamente el intervalo de bytes del contenido que no es de iframe en 16 bytes. La ampliación es necesaria para flujos de iframe, pero no para flujos que no sean de iframe.

**Versión 1.4.34 (1702)**

* Zendesk #27638 - Fuga en el objeto INet cURL

El objeto Posix cURL INet presentaba fugas al mantener presionado el administrador de recursos compartidos y la caché DNS que se usaban en las conexiones cURL.

Este problema se resolvió eliminando el objeto Posix cURL INet del deconstructor INet.

**Versión 1.4.33 (1694)**

* **Biblioteca OpenSSL**

La biblioteca OpenSSL se ha actualizado con la versión 1.0.2j de OpenSSL.

* Zendesk #21701 - Envíe la URL creativa original para la solicitud CRS 1401 en lugar de la URL normalizada.
Este problema se resuelve enviando las URL creativas originales.

* Zendesk #25023 - Reproducción de vídeo de larga duración: congelación de vídeo, parpadeos de pantalla
Este problema se resolvió estableciendo las dimensiones máximas de formato de vídeo para los dispositivos set-top box CenturyLink.

* Zendesk #27460 - La nueva cuenta de Akamai no puede gestionar una solicitud de cdn de POST.
El código se actualizó para que la solicitud de publicidad `cdn.auditude.com` fuera GET en lugar de POST.

* Zendesk #28245 - No se notifica correctamente el estado de reproducción cuando la aplicación pasa de estar en primer plano a estar en segundo plano
Este problema se ha resuelto restaurando correctamente el estado de reproducción para que se reproduzca o se detenga cuando la aplicación vuelva al primer plano.

**Versión 1.4.32 (1682)**

* Zendesk #25779 - Vulnerabilidad de seguridad encontrada con TVSDK
Android 4.2 y versiones posteriores tienen una vulnerabilidad de seguridad cuando JavaScript está habilitado en WebView. El uso de WebView por TVSDK se ha deshabilitado para dispositivos que ejecutan OS 4.2 o versiones posteriores. Esto deshabilita el uso de anuncios VPAID en TVSDK en estos dispositivos.

* Zendesk #26890 - Problema en estado de PANTALLA (ON/OFF) manejando Ref. Jugador
Cuando el motor de vídeo de Adobe (AVE) se reanuda a partir de un estado SUSPENDIDO, DefaultMediaPlayer no actualiza su estado. Como resultado, DefaultMediaPlayer permanece en estado SUSPENDIDO aunque el AVE esté en estado REPRODUCIENDO. Este problema se ha resuelto estableciendo el estado DefaultMediaPlayer en PLAYING al recibir un estado PLAY del AVE, incluso si el estado actual de DefaultMediaPlayer está SUSPENDIDO.

**Versión 1.4.31 (1675)**

* Zendesk #21974 - Excepciones debidas a objetos nulos
   * AdIndex raramente se incrementa cuando es nulo. Esto puede deberse a llamadas de API incorrectas recibidas para adBreak previo a la emisión. Se han corregido los tipos de datos para evitar estas excepciones

* Zendesk #24714 - Desactivación de registros prescindibles
   * Se ha actualizado TVSDK para desactivar el registro superfluo

* Zendesk #24488 - Problemas de sincronización AV en Fire TV
   * Se ha corregido mejorando la gestión de los subprocesos del decodificador AV. Específicamente, cada vez que se modifican las colas de la trama de entrada o salida, se ejecuta el subproceso del decodificador específico del tipo de contenido del fotograma.

* Zendesk #26551 - Corrija los fallos del CRS
   * Cuando la solicitud es HEAD (encabezado http), no es necesario leer el contenido porque está vacío. Aunque está bien intentar leerlo, el antiguo Android (4.0.x) se cuelga mientras llamamos read() y el nuevo Android devuelven el valor correcto (-1) cuando llamamos read(). En función de esto, cambió el código a no leer contenido para &quot;head&quot;.

* Zendesk #26696 Excepción de puntero nulo al acceder a TrickPlayManager
   * Se ha corregido comprobando si el objeto TrickPlayManager no es nulo antes de utilizarlo.

**Versión 1.4.30 (1659)**

* La duración de los recursos de Zendesk #22675 no se actualiza para los flujos en directo/lineales
Este problema se ha resuelto proporcionando una nueva API, assetDuration, en PTVideoAnalyticsTrackingMetadata que proporciona la duración del recurso para las emisiones en directo y lineales.

* Zendesk #25853 Fuga de memoria en TVSDK al cambiar de canal
Se ha resuelto el problema de la fuga de un búfer de lectura de archivos cuando MediaPlayer se restablece o se libera mientras se descarga un archivo.

**Versión 1.4.29 (1653)**

* Zendesk #21200 - El reproductor no se recupera del estado suspendido cuando la aplicación estaba en segundo plano
Cuando el reproductor se suspendió después de que se señalara el conmutador de flujo, la resolución permite al reproductor realizar el conmutador de flujo al restaurar el reproductor desde el estado de suspensión, en lugar de restaurar a la posición anterior.

* Zendesk #23412 - El reproductor está atascado con una caja negra si hace clic en cualquier Anuncio dentro de los últimos 3 segundos de la pausa publicitaria
Este problema es el mismo que Zendesk #21200.

* Zendesk #23616 - La pausa publicitaria omitida busca demasiado lejos en el futuro
En función del tipo de inserción de anuncio (insertar/reemplazar), TVSDK determina si la duración de la publicidad se utiliza en el cálculo para determinar el punto final de la pausa publicitaria.

* Zendesk #25078 - Fuga de memoria DRM de TVSDK en Android TV STB
Se ha localizado y corregido la fuga de memoria para el objeto adaptador DRM.

* Zendesk #25067 - Bloqueo en VideoEngineTimeline
Esto sucede porque los objetos no se limpiaron correctamente y se llamaron a los eventos después de destruirlos. El problema se resolvió añadiendo comprobaciones para evitar excepciones nulas.

* Zendesk #25352: Establecer encabezado HTTP personalizado
Este problema se ha resuelto añadiendo un nuevo encabezado personalizado a la lista de permitidos en TVSDK.

* Zendesk #25617 - El rollover de PTS en directo provoca la discontinuidad del reproductor y el bloqueo de memoria
Este problema se ha resuelto añadiendo un controlador PTS en FragmentedHTTPStreamer cuando se produce un rollover en medio de un segmento.

**Versión 1.4.28 (1637)**

* Zendesk #23618 - Los eventos de pausa publicitaria se activan antes de consultar la política publicitaria
Este problema se resolvió al no activar los eventos AD_BREAK_START y AD_START cuando se omite el anuncio debido a adForgity. Se envía el evento AD_BREAK_SKIPPED en su lugar.

**Versión 1.4.27 (1631)**

* Zendesk #23174 - Problema de rendimiento al cambiar el tamaño del vídeo
Este problema se resolvió probando una nueva API, MediaPlayerView.setSurfaceFixedSize, que permite que TVSDK acceda a SurfaceHolder.setFixedSize() desde MediaPlayerView.

* Zendesk #24450 - TVSDK realiza solicitudes de publicidad duplicadas
Este problema se producía cuando el tiempo transcurrido se convertía en largo y no en doble, y este problema se ha corregido.

**Versión 1.4.26 (1627)**

* Zendesk #21436 - Actualización de la biblioteca OpenSSL a la versión 1.0.2h
* Zendesk #23825 - Las cookies no se incluyen en las devoluciones de llamada Corregidas al proporcionar compatibilidad con cookies android.

**Versión 1.4.25 (1620)**

* Zendesk #22900 - El flujo DRM de Adobe Primetime en directo no se está reproduciendo en el reproductor de referencia de Android
Se ha corregido el problema de asignación de memoria.
* Zendesk #23176 - La aplicación se bloquea cuando intenta reproducir anuncios VPAID
El bloqueo se produjo porque la aplicación no crea una vista de anuncio personalizada para procesar un anuncio VPAID. Este problema se resolvió ignorando las publicidades VPAID en la respuesta del servidor de publicidad cuando no hay ninguna vista de publicidad personalizada.

* Zendesk #23153 - SampleAES DRM Stream - Retraso en el reproductor de referencia TVSDK
Este problema es el mismo que Zendesk #22900.

**Versión 1.4.24 (1612)**

* Zendesk #20784 - Análisis: Se completa la activación de contenido para transiciones de vídeo en directo
Este problema se ha resuelto añadiendo una API (trackVideoComplete) para almacenar en déclencheur manualmente la finalización del contenido durante una sesión de seguimiento de vídeo en directo/lineal.

* Zendesk #21977 VideoEngineTimeline Bloquear durante la operación placeAdBreak/acceptAd
   * En este número se actualizaron las bibliotecas siguientes:
      * Biblioteca AdobeMobile a la versión 4.10.0
      * Biblioteca VHL a la versión 1.5.6
      * Biblioteca VHL-Nielsen a la versión 1.6.7

Este problema se ha resuelto añadiendo una comprobación nula antes de añadir anuncios a la lista de anuncios aceptados.

* Zendesk #22313 La velocidad de bits para las STBs con chipset Amilogic no va más allá de 1,2M
Este problema se resolvió precargando las capacidades del códec de medios y desactivando el conmutador perfecto para los dispositivos de chipset Amilogic.

* Zendesk #19520 Ejemplo de recurso HLS AES no se reproduce en reproductores TVSDK
Este problema se resolvió gestionando varios descriptores de PMT para flujos HLS cifrados de AES de muestra.

**Versión 1.4.23 (1602)**

* Zendesk #18852 - Actualización de la lógica de selección creativa basada en las reglas CRS
Este problema se resolvió añadiendo un archivo de configuración JSON para especificar la prioridad de selección creativa.

* Zendesk #20861 - Android N
Esta versión es compatible con Android N, ya que elimina la capacidad de usar directamente las bibliotecas nativas de la plataforma Android a las que ya no pueden acceder las aplicaciones que se ejecutan en Android N.

* Zendesk #21018 - Android N se bloquea
La misma resolución que ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter se bloquea en un error Invalid_Key
El error Invalid_Key no incluye una descripción del AVE, por lo que el análisis del texto resultó en NPE. El problema se resolvió añadiendo una comprobación nula para la descripción durante onError antes de analizar la descripción.

* Zendesk #22286 - La biblioteca nativa está asignando clave/fragmento de lectura de memoria causando un bloqueo
Se ha corregido este bloqueo que se producía en Android al intentar cargar un manifiesto con varias claves simultáneamente.

**Versión 1.4.22 (1581)**

* Zendesk #17236 - Tiempo de reproducción no confiable para vídeos HLS con DRM
Se ha corregido el salto de tiempo con los flujos LBA, en el que el tiempo de inicio del segmento de audio no coincide con la hora de inicio del segmento de vídeo.

* Zendesk #17680 - La reproducción de vídeo se está congelando en el cuadro Selevision Andredo
El decodificador de vídeo de este dispositivo devuelve a veces un salto de tiempo de salida significativo al eliminar un fotograma de vídeo del búfer de salida, y esta marca de tiempo de salida sigue siendo alta. Este problema se ha resuelto devolviendo un error *perfil de vídeo no admitido* que no obliga al reproductor a reintentar el mismo perfil o elegir un perfil diferente.

* Zendesk #19074 - Congelación de vídeo durante FFWD y REW truco
Este problema se ha resuelto añadiendo una nueva advertencia TRICKPLAY_ENDED_DUE_TO_ERROR para notificar a la aplicación que se ha salido de trickplay y que el vídeo se ha pausado debido a un error irrecuperable.

* Zendesk #19574 - TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM
Este problema se resolvió de las siguientes maneras:

* Zendesk #19986 - Comportamiento de OP roto para determinados dispositivos como Android TV
* Añadir un error FILE_NOT_FOUND a la condición.
* Cuando el error proviene de un error *file not found*, separando la dirección URL y la respuesta de la descripción del error si la respuesta está disponible.
Se ha corregido el error lógico introducido por el soporte de NVidia shield OP. En los dispositivos de protección que no sean NVidia, confíe en los indicadores de seguridad de visualización incluso cuando se desconozca el tipo de visualización.

* Zendesk #20549 - Gestión de listas de reproducción antiguas. Este problema se resolvió reduciendo el intervalo entre la actualización del manifiesto activo y la mitad de la duración esperada del segmento, si la recuperación anterior no recibe nuevos segmentos.

* Zendesk #20742 - El uso de memoria parece seguir aumentando cuando se reproduce contenido en directo en FireTV. El bloqueo es causado por la tabla de referencia de objeto JNI que ha alcanzado el límite. Este problema se resolvió eliminando la referencia al objeto MediaFormat que se creó durante el reinicio del decodificador.

* Zendesk #21125 - Regreso de pausa publicitaria en directo/lineal temprano (CSAI). Se ha añadido una función que permite al reproductor regresar al contenido principal durante una pausa publicitaria si el reproductor registra la empalme en las señales publicitarias utilizando la empalme en el detector de oportunidades.

* Zendesk #21334 - Valor de tiempo de espera de solicitud de anuncio de TVSDK para solicitudes de anuncios de terceros. Se ha agregado una configuración adRequestTimeout a AdvertisingMetadata que habilita un tiempo de espera global para la llamada de anuncio.

**Versión 1.4.21 (1566)**

* Zendesk #17781 - La captura de pantalla de ADB ya no funciona
Este problema se resolvió agregando la API DefaultMediaPlayer.create(Context context, boolean secureSurface) , que permite la captura de pantalla.
Para permitir capturas de pantalla, pase false para secureSurface.
Importante: Se recomienda no habilitar esta función de captura de pantalla en una configuración de producción.

* Zendesk #19074 - Congelación de vídeo durante FFWD y REW truco
Se han resuelto los siguientes problemas que se producían cuando el archivo &quot;game&quot; podría bloquearse en la reproducción:

* Zendesk #19532 - El subtítulo aparece fuera de orden
   * FHS comienza con la reproducción de trampas, pero el primer segmento de iframe no tenía un fotograma.
   * Al descargar un segmento de iframe, si FHS detecta una condición de error, sale de la reproducción de trucos y pone en pausa la reproducción.
   * La implementación de Android MediaCodec espera para siempre la disponibilidad de la cola de entrada mientras se le pedía que vaciara todos los búferes de entrada/salida.
Este problema se ha resuelto invirtiendo el orden de las señales WebVTT para que varias señales superpuestas parezcan &quot;desplazarse hacia arriba&quot;.

* Zendesk #19574 - El TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM
En la carga inicial del archivo de manifiesto en PTMediaPlayerItem.prepareToPlay, si la carga falla, el TVSDK no informa del cuerpo de la respuesta de error a la aplicación.
Este problema se resolvió permitiendo que el TVSDK informara de la respuesta de error como un error a la aplicación.

* Zendesk #19701 - congelación de la reproducción con SAP/Discontinuidad
El reproductor se bloquea cuando el audio y el vídeo se desalinean cuando se ha resuelto la discontinuidad.

* Error #PTPLAY-11162 - Se ha resuelto la actualización de la biblioteca OpenSSL a la versión 1.0.2f.

**Versión 1.4.20 (1546)**

* Zendesk #17384 - Solicitud de funciones: Compatibilidad con metadatos ID3 para la reproducción de AAC
Se ha proporcionado compatibilidad con etiquetas ID3 en medios AAC en el TVSDK para Android a partir de la versión 1.4.20.

* Zendesk #18358 - El reproductor se bloquea en el interruptor de velocidad de bits con interrupciones fuera de sincronización
Este problema se resolvió manejando adecuadamente los casos de borde de vinculación de ABR.

* Zendesk #19232 - La aplicación que utiliza TVSDK 1.4.18 se está comportando extrañamente en la versión 4 anterior del sistema operativo Amazon
Este problema se ha resuelto eliminando la creación de vistas web ocultas en el proceso de inicialización del reproductor TVSDK para evitar conflictos con dispositivos que no admiten Android Webview.

* Zendesk #19585 - Reproducción de movimiento lento cuando se produce una transición de velocidad de bits adaptable.
Durante el interruptor ABR, si el nuevo perfil tiene una velocidad de muestreo de audio diferente a la del perfil actual, la reproducción se convierte en movimiento rápido o lento. Esto se debe a que no se notifica al presentador de vídeo que el formato de audio ha cambiado.
Este problema se ha resuelto asegurándose de que el indicador de notificación está establecido en el lugar correcto.

* Zendesk #19683 - Reproducción de SAP DAI - Sin audio durante unos segundos.
En varios casos en la lógica del SDK de TVSDK, cuando se comparó la marca de tiempo de dos segmentos de representación, se utilizó RENDITION_TIMEOUT_THRESHOLD como un intervalo de valor aceptable, ya que la marca de tiempo no siempre se puede comparar con una diferencia de 0 ms. Si el espacio está dentro del rango de RENDITION_TIMEOUT_THRESHOLD, se supone que es una coincidencia.

RENDITION_TIMEOUT_THRESHOLD se estableció en 100 ms, pero resultó insuficiente para ciertas emisiones. Este problema se resolvió aumentando el RENDITION_TIMEOUT_THRESHOLD a 200 ms.

* Zendesk #19699 - El TVSDK no cambia entre las pistas de subtítulos VTT
Este problema se solucionó haciendo que el volcado del reproductor y recargue el manifiesto cuando cambia una pista y corrigiendo el problema de conversión de cadenas UTF8 que afectaba a los nombres de seguimiento de subtítulos WebVTT de doble byte.

* Zendesk #19717 - CC opciones problema de visualización
Este problema se ha resuelto administrando correctamente la cadena Unicode.

* Zendesk #19910 - No se detectan las etiquetas TIT2 ID3
Este problema se ha resuelto proporcionando compatibilidad más completa para las codificaciones de cadena ID3 v2.4 y para la compatibilidad con ID3 v2.3.

* Zendesk #20135 - El TVSDK está activando varios onComplete para contenido de VOD.
Este problema se resolvió añadiendo el detector de eventos post_roll_complete en el lugar correcto, en lugar de en el caso completo del evento de cambio de estado.

**Versión 1.4.19 (1521)**

* Zendesk #4180 - El TVSDK no está aplicando el HDCP.
   * Esto es una corrección parcial para este ticket y aborda solamente el problema para los dispositivos de protección NVidia.
Debe utilizar la API de detección de HDCP implementada correctamente en Nvidia Shield para realizar un seguimiento dinámico del estado de HDCP.

* Zendesk #18358 - El TVSDK se bloquea en el interruptor de velocidad de bits sin interrupciones no sincronizadas.
   * Este problema se resolvió añadiendo una nueva advertencia para detectar la discontinuidad de PTS y obligando a la comprobación de PTS a rehacer la búsqueda del segmento correcto para cada conmutador ABR.
Para corregir el bloqueo, la llamada al método mediaPlayer.setCustomConfiguration debe incluir forcePTSCheckForABR como argumento.

* Zendesk #19038 - No transmisión en vivo en Asus Zenpad 10.

   Este problema se ha resuelto cargando previamente la información del códec de medios, de modo que no realice consultas con la función en tiempo de ejecución.

* Los siguientes problemas son los mismos que Zendesk #19038:
   * Zendesk #19483 - El TVSDK se está bloqueando en la plataforma Intel.
   * Zendesk #19171 - Bloqueos en el Asus Memo Pad 7 con Android 5.0.

**Versión 1.4.18 (1503)**

* Zendesk #3324 - El informe de anuncios de Primetime no rastrea pausas publicitarias cuando no hay medios publicitarios en un VMAP.
Cuando una pausa publicitaria está vacía, los eventos de seguimiento de inicio y finalización de la pausa publicitaria no se estaban agrupando. Este problema se resolvió enviando pings de inicio de pausa publicitaria en pausas publicitarias vacías, como VMAP AdBreak, con un nodo AdSource válido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) se ignora después de la llamada a MediaPlayer.reset()
Este problema se resolvió añadiendo setCCVisibility(Visibility.INVISIBLE); a la función reset() en la clase MediaPlayer.

* Zendesk #18328 - Problema de trama perdida en dispositivos de segunda generación de Amazon Fire TV para el contenido con 60FPS
Este problema se resolvió aplicando el FPS codificado para la toma de decisiones durante el tiempo de espera y con una lógica de predicción FPS mejor codificada.

**Versión 1.4.17 (1472)**

* Zendesk #2231 - Error devuelto al recuperar el manifiesto no disponible en MediaPlayerNotification
Este problema se ha resuelto incluyendo el cuerpo de respuesta del manifiesto cuando hay un error de análisis.

* Zendesk #17703 - VideoEngineView no impide las capturas de pantalla durante la reproducción del vídeo
El método setSecure ha estado disponible desde la API 17, pero como la API 17 cubre las versiones 4.2, 4.2.1 y 4.2.2, no se sabe cuál generará una excepción o si es específico del dispositivo. Este problema se resolvió al incluir VideoEngineView.setSecure en la cláusula try catch.

* Zendesk #17919 - La búsqueda de contenido causa un error de latido
Se producía un error de posición de datos de entrada no válido como resultado de la llamada de latido generada cuando la búsqueda se inició después de la emisión. Este problema se ha resuelto.

**1.4.16a**  (1454a)

* Zendesk #18215 - Algunos flujos AES no pueden cargarse.
Este problema se ha resuelto comprobando el tamaño de los metadatos DRM del perfil antes de cargar la clave AES.

**Versión 1.4.16 (1454)**

* Zendesk #3875 - Tab S se bloquea durante la reproducción
Revertir la dependencia de OKHTTP en Auditude para CRS porque TVSDK ahora está utilizando directamente httpurlconnection en lugar de curl. El problema se resolvió borrando las excepciones antes de realizar cualquier otra llamada de JNI.

* Zendesk #4487 - Seguimiento del canal de contenido lineal
El problema se resolvió permitiendo la reinicialización del rastreador de Video Heartbeat durante una sesión de reproducción de flujo lineal.

* Zendesk #17919 - Android: la búsqueda de contenido causa un error de latido
Se ha resuelto el problema que se producía cuando el latido estaba en estado de error cuando se realizaba una llamada a otro punto del capítulo.

* Zendesk #18053 - Adobe Primetime se bloquea en malvavisco
El SDK de TVSDK se bloqueaba en el sistema operativo Android M cuando la biblioteca TVSDK utilizaba código neón que realizaba la conversión de color YUV -> RGB. El problema se resolvió actualizando las funciones que causan este problema usando la versión no neon del código.

* Zendesk #18072 - Android M - Bloqueo de aplicación
Al comprobar si el perfil y el nivel son compatibles, se produce un bloqueo al llamar a las API MediaCodecList y MediaCodecInfo . El problema se ha resuelto proporcionando una solución temporal cargando toda la información del códec con antelación para evitar llamar a estas API solo cuando se necesita información del códec.

* Zendesk #18074 - Los subtítulos árabes no funcionan en Nexus con Android 6.0
El problema se resolvió proporcionando compatibilidad con el mapa de fuentes CTS para Android.

**Actualización de la versión 1.4.15 (1438)**

* Zendesk #17437 - Largo retraso en el inicio del contenido de VOD con algunos flujos de AES.
Para resolver este problema, si hay varias claves enumeradas en el manifiesto, descargue todas las claves de AES en paralelo.

**Versión 1.4.15 (1435)**

* Zendesk #4278 - Glitches on Android establece los cuadros superiores cuando cambia la velocidad de bits adaptable (ABR).
La solución fue agregar compatibilidad con el conmutador ABR sin problemas con el último códec de medios Android.

* Zendesk #17063 - Llamar a mediaPlayer.reset() causa un error de restablecimiento del motor de vídeo.
La corrección era incluir el MediaErrorCode original de VideoEngineExceptions al enviar eventos de error.

* Zendesk #17130 - Una pausa breve pero destacable cuando se cambia la tasa de bits vista en FireTV.
(Igual que el número 4278 anterior) La corrección era para añadir compatibilidad con el conmutador ABR sin problemas con el último códec de medios Android.

* Zendesk #17666 - Marcadores de publicidad adicionales, Inesperados o Sin anuncios al reanudar el contenido.
La solución fue un problema al hacer prepareToPlay en contenido de vídeo bajo demanda (VOD), la búsqueda inicial funciona en el tiempo local en lugar del tiempo virtual.

* Zendesk #17437 - Largo retraso en el inicio del contenido de VOD con algunos flujos de AES.
La corrección era descargar todas las claves AES en paralelo cuando aparecen varias claves en el manifiesto.

* Zendesk #17851 - Android TV - Marco negro durante ABR
La corrección era especificar KEY_MAX_WIDTH y KEY_MAX_HEIGHT para habilitar la reproducción adaptable.

**Versión 1.4.14 (1415)**

* Zendesk #3875 - Tab S se bloquea durante la reproducción.
Se necesitaba una corrección adicional para evitar el bloqueo.

* Zendesk #17245 - La reserva en Android TV no funciona.
Se ha corregido un problema adicional que hacía que la reproducción se bloqueara cuando se habilitaba la reserva y la respuesta de VMAP tuviera una pausa publicitaria vacía.

**Versión 1.4.14 (1412)**

* Zendesk #17245 - La reserva en Android TV no funciona.
Se ha eliminado una restricción para deshabilitar el reempaquetado creativo en los anuncios de reserva.

**Versión 1.4.13 (1388)**

* Zendesk #3502 - Soporte de failover basado en clientes HLS durante una pausa publicitaria
Permitir la conmutación por error al manifiesto principal cuando se produce un error de actualización de perfiles activos durante un período de pausa publicitaria.

* Zendesk #3875 - Tab S se bloquea durante la reproducción
Para resolver el conflicto entre HttpUrlConnection y cURLm, utilice una biblioteca de terceros.

* Zendesk #4450: problema al configurar metadatos personalizados para una única ubicación en una resolución de contenido
Agregue un establecedor a la configuración de oportunidad.

**Versión 1.4.12 (1388)**

* Zendesk #2751 - CSAI y CRS | Mejora: Gestione elementos dinámicos en determinadas direcciones URL de archivos multimedia.
Se ha actualizado el servicio de reempaquetado creativo para que gestione correctamente los anuncios con direcciones URL creativas dinámicas.

* Zendesk #3965 - Si se vuelve a la reproducción normal después de la reproducción, se produce un salto hacia delante un poco antes de iniciar la reproducción.
   * La corrección incluye que TVSDK devuelva el tiempo antes del cambio de velocidad hasta que se actualicen todas las variables, en lugar de intentar calcular GetStreamTime.
   * Se ha corregido un bloqueo al cambiar la velocidad de reproducción del truco cerca del final del flujo.
   * Se ha corregido el cálculo de tiempo actual durante la reproducción de trucos.

* Zendesk #3978 - Trickplay a 8x y 16x se bloquea con frecuencia.
   * Elija siempre el perfil de reproducción de trucos con la velocidad de bits más baja para evitar el almacenamiento en búfer constante.
   * Aumente el intervalo de fotogramas de omisión para una tasa de reproducción de trucos alta.
   * Se ha corregido un problema que provocaba que el búfer siguiera creciendo después de alcanzar la longitud objetivo durante la reproducción del truco.

* Zendesk #3992 - Velocidad adicional de reproducción.
TrickPlay se ha actualizado para aceptar tasas superiores a 16x; +/- 32, +/-64 y +/-128 ahora también están permitidos.

* Zendesk #4007 - Interpretación del objeto GEOB como parte de los metadatos de la cronología (Android y Web).
Se ha añadido la API setByteArray y getByteArray.

* PTPLAY-7301: Instant On start en Random Access Point.
Instant On se ha actualizado para permitir un punto de inicio distinto de cero.

**Versión 1.4.11 (1363)**

* Zendesk #2076 - Encuentro frecuente al reproducir vídeo en Motorola Xoom con Android 4.0.3
Se han agregado dispositivos a la lista de permitidos para evitar que intenten reproducir contenido de alto perfil.

* Zendesk #2197 - `[Ads]` Seguimiento de errores de publicidad
enviar OperationFailedEvent con notificación de advertencia.

* No se rellena la macro de Zendesk #3304 - VAST 3.0 `[ERRORCODE]`
   * el código de error 400 se expondrá si el anuncio en línea tiene un elemento creativo incorrecto.
   * `[ERRORCODE]` la macro estará codificada en la dirección URL

**Versión 1.4.10 (1354)**

* Zendesk #2941 - Los activos activos activos no tienen &quot;0&quot; en el rango buscable
Anteriormente había un búfer de 3 segmentos cuando se intentaba llegar al principio de una emisión en directo, ahora es posible buscar al principio de una emisión en directo (es decir, el inicio del primer segmento).

* Zendesk #3169 - Actualización del reproductor de referencia con integración con Adobe AnalyticsEl reproductor de referencia se ha actualizado con la biblioteca Adobe Analytics como ejemplo de implantación.
* Zendesk #3299 - Comportamiento inexplicable del juego de trucos
   * Se ha corregido un error por el que volver al estado de reproducción después de detener la reproducción del truco podía tardar varios segundos (a veces más de 25 segundos).
   * Se ha corregido un error por el que invocar la reproducción mediante trucos por segunda vez en el mismo medio podía hacer que el flujo se bloqueara en el momento actual.
* Zendesk #3433 - Android y Flash - Problemas con subtítulos

GetLine para WebVTT no respetaba una longitud ajustada &lt;CR>&lt;LF> para un paquete; el último rótulo podría contener caracteres de rótulos anteriores.

* PTPLAY-6243: Mejore el reproductor de referencia para capturar información de depuración

Los reproductores de referencia de ejemplo de Android se han mejorado con una opción para activar los registros de depuración y enviar por correo electrónico los resultados. Esta opción se encuentra en el menú Log del reproductor de referencia.

**Versión 1.4.9 (1332)**

* Zendesk #2649 - Se completa el búfer antes de que el búfer inicial esté lleno

Después de una llamada a otro punto del contenido, es posible que el motor de vídeo establezca el estado en REPRODUCIR antes de que el presentador de vídeo esté listo para la reproducción. Se produce cuando el estado del búfer es alto antes de la llamada a otro punto del contenido. Se corrige notificando al motor de vídeo de estado de búfer bajo. Con el estado de búfer bajo del motor de vídeo, la llamada a Reproducir hace que el estado cambie a ALMACENAMIENTO EN BÚFER en lugar de REPRODUCIR. La reproducción se reanuda cuando el estado cambia a PLAYING.

* Zendesk #2846 - Solicitud de mejora: Proporcionar la capacidad de establecer distintas cadenas de usuario-agente para las llamadas realizadas por la biblioteca de Auditude

Se ha añadido una nueva API para establecer el agente de usuario para las llamadas relacionadas con la publicidad, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Si no hay ningún agente de usuario establecido, se utilizará el valor predeterminado. Esto solo afecta al agente de usuario para las llamadas relacionadas con la publicidad, el agente de usuario para las llamadas de medios no cambia, que es &quot;Adobe Primetime&quot;+&lt;user agent predeterminado>.

**Versión 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Error con local ... Si la carga del manifiesto en FragmentedHTTPStreamer::ThreadParseManifest() falla, compruebe si el dominio URL es localhost y, si es así, cambie el dominio a 127.0.0.1 y recupere ThreadParseManifest.
* Zendesk #3072 - Cambio automático a velocidades de bits más bajas. Se ha cambiado el cálculo de la longitud del búfer para omitir la carga útil PTS cero.
* Zendesk #3168 - Los subtítulos de WebVTT solo se muestran durante los primeros 10 segundos.
* Zendesk #3193 - Solicitud de una API de cambio de perfil en TVSDK, se ha añadido PlaybackEventListener.onProfileChanged() .

**Versión 1.4.7 (1311)**

* Zendesk #2197 - Seguimiento de errores de publicidad. Se ha añadido una notificación para el recurso que no pudo cargar el manifiesto
* Zendesk #2575 - PSDK ignora el anuncio MARK personalizado en el flujo antes del vídeo
* Zendesk #2719 - Gana la muerte con anuncios de audiencia, seguimiento de señalizaciones fijo cuando se redirige a la URL relativa en el complemento de auditude
* Zendesk #2760 - Etiqueta DISCONTINUITY ignorada durante el modo TrickPlay
* Zendesk #2805 - Bloqueo del reproductor al comienzo de la reproducción, la misma corrección que Zendesk #2719
* Zendesk #2817 - Reproductor de Android - El reproductor a veces se cuelga y se detiene la reproducción, corregido al ampliar los búferes de descodificación de 2 a 3 segundos
* Zendesk #2839 - ¿Adobe Primetime PSDK es compatible con chipsets ARMv8?, se ha añadido una corrección para el bloqueo que se encuentra en Galaxy S6.
* Zendesk #2885 - Reproducción de bloqueo de audiencia, la misma corrección que Zendesk #2719
* Zendesk #2895 - Fallo de HLS en directo de forma consistente después de 10 minutos de reproducción
* Zendesk #2925 - Comentarios con respecto a la compilación de Android dev (1.4.5), en ciertos dispositivos cuando ponemos el paquete en cola en la cola de entrada, si el PTS es negativo, el decodificador entra en un estado extraño de que siempre obtenemos un PTS de salida negativo para paquetes futuros. La corrección establece la entrada PTS en cero si es negativo para evitar este problema.
* PTPLAY-4645 - Desactive el soporte de cifrado RC4 en openssl. Hay explosiones conocidas para RC4. Esto significa que si se intenta conectar con un servidor que solo admita RC4, se producirá un error.

**Versión 1.4.6 (1282)**

* Zendesk #2192 - La velocidad de bits no siempre disminuye en condiciones de red deficientes, ya que se soluciona eliminando la implementación rápida del conmutador.
* Zendesk #2631 - Subtítulos árabes en Android: El texto de varias líneas aparece cortado, corregido ajustando el tamaño de fuente para las fuentes árabes.
* Zendesk #2844 - El almacenamiento en búfer en la Nota 4 y el tiempo de descarga del fragmento no son precisos.

Este problema se solucionó añadiendo latencia entre las descargas de segmentos de vídeo en el cálculo del ancho de banda y haciendo que la lógica de cálculo del tiempo de descarga utilizara el tiempo completo del ciclo de solicitud.

* Zendesk #2908 - los subtítulos árabes no funcionan en Nexust 5, 6 y 7, arreglado agregando dos fuentes de reserva más para scripts árabes.
* PTPLAY-4627: actualizar Nielson appsdk a la versión 1.2.3.7
* PTPLAY-5084: compatibilidad con la conmutación por error de la actualización del manifiesto maestro activo

**Versión 1.4.5 (1248)**

* Zendesk #1757 - Se corrigió solo el audio reproducido o el reproductor se bloquea para algún perfil de velocidad de bits de vídeo, Nexus 4 y Nexus 7
* Zendesk #2072 - TimedMetadata para AdEvent no contiene la dirección URL completa solo &quot;http&quot;
* Zendesk #2192 - La velocidad de bits no siempre disminuye en malas condiciones de red
* Zendesk #2256 - Acceso a la lista de reproducción maestra, PSDK actualizado para distribuir eventos timedMetadata para etiquetas suscritas en la lista de reproducción maestra.
* Zendesk #2269 - Dos idiomas de subtítulo diferentes aparecen en la pantalla al mismo tiempo con WebVTT
* Zendesk #2417 - El reproductor que intenta descargar subtítulos antes del inicio de la reproducción, WebVTT estaba usando una variable de número de segmento incorrecta para la coincidencia de números de segmento. El error solo aparecería para los medios que tienen índices de segmento que comienzan en cero.
* Zendesk #2470 - PSDK no vuelve del estado SUSPENDED cuando se produce un cambio en la velocidad de bits después de la suspensión. En una situación especial en la que RestoreGPUResource (restaure el reproductor del estado de suspensión) llama a la búsqueda inteligente y el conmutador de flujo detectado antes de eso, la búsqueda inteligente no puede completarse y resulta en un almacenamiento en búfer constante.
* Zendesk #2451 - Subtítulos &quot;inserción inferior&quot;, parámetro &quot;bottomInset&quot; añadido al código de subtítulo
* Zendesk #2480 - Desactivación de la optimización de redireccionamiento HTTP 302, se ha añadido compatibilidad para establecer la propiedad useRedirectUrl
* Zendesk #2486 - señalizaciones de terceros
* Zendesk #2547 - subtítulos en árabe: El texto debe alinearse con la justificación correcta

**Versión 1.4.4 (1195)**

* Zendesk #1158 - La reproducción falla en Huawei Valiant (Y301A1)
* Zendesk #1709 - Tamaño incorrecto de los medios y vídeo estirado
* Zendesk #1757 - Solo audio reproducido después del cambio de perfil entre flujos con idénticos datos spa/pps
* Zendesk #2095 - Estado HTTP 307 (redirección) hace que el reproductor de Adobe detenga la reproducción
* Zendesk #2126 - Falta el evento TimedMetaData para el último ADEVENT, las etiquetas suscritas que existen después del último segmento no se notificaron al PSDK desde AVE
* Zendesk #2227 - Bloqueo en VideoEngine nativeReset y nativePause
* Error #3921755 - Actualización de la biblioteca OpenSSL a la versión 1.0.1L

**Versión 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Encendido y apagado de subtítulos
* PTPLAY-1818 - El truco de rebobinado se detiene en el anuncio en lugar de rebobinar más allá
* PTPLAY-2736: Se muestra en la pantalla un subtítulo WebVTT que se mostraba anteriormente cuando se termina de reproducir un flujo con el subtítulo WebVTT
* PTPLAY-3773: Un anuncio mid-roll no se reproduce cuando se inicia la reproducción del flujo después de la posición del anuncio

**Versión 1.4.2**

* Zendesk #1561 - Soporte de failover basado en clientes HLS en primetime. Utilizará la fecha y hora del programa para solucionar el failover
* Zendesk #1590 - LoadInfo.MediaDuration siempre es 0 (no fijo solo para audio)
* Zendesk #1626 - Posible fuga de memoria en el reproductor. No se ha producido una fuga de memoria real, el problema era con NotificationHistory guardando las últimas 1000 notificaciones, esto se ha reducido a 100.
* Zendesk #2192 - La velocidad de bits no siempre disminuye en malas condiciones de red

**Versión 1.4.1 (1121)**

* Zendesk #1951 - Bloqueo en VideoEngine.nativeReset() en dispositivos 4.0.x
* Zendesk #2064 - Native Crash SIGSEGV en dispositivos Android específicos basados en intel
* Zendesk #2075 - Bloqueo en VideoEngine.nativeReleaseGPUResource en dispositivos 4.0.x
Nota: Esta compilación es ***necesaria*** para la compatibilidad con Android 5.0 (Lollipop)
* Zendesk #1513 - Compatibilidad con Android Lollipop
* Zendesk #1709 - Tamaño incorrecto de los medios y vídeo estirado
* Zendesk #1871 - Los subtítulos WebVTT desaparecen ocasionalmente y vuelven a aparecer al ver una emisión en directo con subtítulos WebVTT
* Zendesk #1996 - No se ven marcadores de línea de tiempo en PSDK 1.4.0
* Zendesk #2046 - Bloqueo con PSDK 1.4.1.1113, bloqueo corregido para emisiones en directo cuando no se devuelve anuncios de la audiencia
* Error #3769657 - Actualizar la versión de curl a 7.38.0
* PTPLAY-1575 - Cuando la reproducción de ABR comienza con audio solamente y luego cambia a la emisión de audio/vídeo, el vídeo nunca se renderiza mientras el audio continúa
* PTPLAY-2499 - Actualización a OpenSSL a la versión 1.0.1j para abordar las vulnerabilidades recientes
* PTPLAY-2632: El vídeo no se recupera después de finalizar el anuncio mid-roll en Android Lollipop
* PTPLAY-2678: Se cuelga un vídeo durante las pruebas de longevidad en directo en Android Lollipop

**Versión 1.4.0**

* Zendesk #1024 - Función para eliminar un anuncio del flujo a través de un manifiesto
* Zendesk #1293 - Problema de selección de seguimiento de subtítulos.
* Zendesk #1590 - LoadInfo.MediaDuration siempre es 0, mediaDuration ahora muestra el valor correcto.
* Zendesk #1629: el reproductor/la aplicación se bloquea al final de la reproducción del anuncio en Galaxy S4
* Zendesk #1674 - ClosedCaption No aparece, se muestran correctamente los 708 subtítulos cuando faltan los códigos 0x03 ETX.
* PTPLAY-2157 : los captadores devolvieron los estilos predeterminados de subtítulos aunque se hubieran establecido y verificado visualmente distintos estilos en la emisión. Las propiedades de estilo de Subtítulos ahora mostrarán el valor en el que se han establecido.

## Problemas conocidos en 1.4 {#known-issues-in}

**Versión 1.4.31**

* PTPLAY-16803 - Subtítulos no funcionarán con contenido de solo audio, ya que el sistema de subtítulos necesita vídeo para funcionar. Sin vídeo, no hay dimensión de ventanilla móvil y, sin una dimensión de ventanilla móvil, no se puede mostrar ningún gráfico para los rótulos.
* PTPLAY-1634 - La misma etiqueta suscrita tiene diferentes marcas de hora en diferentes ventanas en vivo. Cuando la ventana activa se mueve, la misma etiqueta debe tener las mismas marcas de tiempo. Sin embargo, a veces, incluso las mismas etiquetas tienen marcas de tiempo diferentes.
* PTPLAY-3197 - Bloqueo con la señal 11 error SIGSEGV en el dispositivo Acer Iconia después ~ 1 hora de reproducción continua
* PTPLAY-3310 - Con un audio de velocidad de bits más baja, el audio se convierte en disquetes/estupidez en Acer Iconia
* PTPLAY-3355 - WIN MUERTE choque en Motorola Xoom con 4.0.x después ~ 1 hora de reproducción continua.
* PTPLAY-3557 - El rebobinado en una pausa publicitaria está provocando que la emisión se complete
* PTPLAY-7079 - La ventana de reproducción en el cliente android no funciona con Parada segura/Parada dura
* Error #3760144 - La resolución puede cambiar o parecer que impulsa cuando el flujo está en pausa en algunos dispositivos, como Kindle Fire 7 y Samsung Galaxy Nexus. Sólo observable bajo estrecha inspección
* Error #3761170 - seekToLocal en directo con anuncios no puede volver a buscar en contenido de anuncios, es mejor utilizar las API de tiempo actual para emisiones en directo
* Error #3763370 - Las transmisiones en directo con anuncios ocasionalmente mostrarán dos marcadores de anuncio juntos cuando solo debería haber uno. Estos marcadores de publicidad representan el mismo anuncio y solo se reproducirá uno
* Error #3763373 - El marcador de anuncio puede desaparecer brevemente al buscar más allá de un anuncio en flujos de VOD. El marcador de anuncio se restaura y no hay otros efectos adversos en la cronología
* Algunos dispositivos tienen problemas de reproducción conocidos. Consulte [Problemas conocidos del dispositivo en 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementación de referencia: la reproducción de trucos no se implementa en la aplicación de ejemplo
* En algunos dispositivos de Android TV se puede ver un marco negro debido a un restablecimiento del decodificador en los siguientes puntos de transición:
   * entrada y salida del modo de reproducción de trucos
   * cambio entre las pistas de audio de enlace tardío
   * de un anuncio al contenido principal.

**Versión 1.4.23**

* Subtítulos no funcionarán con contenido de solo audio porque el sistema de subtítulos necesita que el vídeo funcione. Sin vídeo, no hay ninguna dimensión de ventanilla móvil y sin una dimensión de ventanilla móvil, no se puede mostrar ningún gráfico para los rótulos.
* A partir de la versión 1.4.23, el TVSDK no admitirá el sistema operativo Gingerpan OS 2.3. Esto se debe a que el TVSDK utilizó las siguientes bibliotecas privadas de Android para recopilar información de hardware sobre dispositivos con el sistema operativo Gingerpan:

   * `libstagefright.so`
   * `libcutils.so`

En la versión Android N, Google ha eliminado el acceso a estas bibliotecas privadas. Actualmente, el sistema operativo Gingerpan representa menos del 1 % de la cuota de mercado del sistema operativo Android a nivel mundial, por lo que, después de la versión 1.4.23, el sistema operativo Gingerpan ya no será compatible con el SDK de TVSDK.
Cuando utiliza la versión 1.4.23 (que incluye compatibilidad con Android N) o posterior:
* Actualice sus aplicaciones para utilizar minSdkVersion versión 11.
* Si el usuario final ejecuta OS 2.3, la versión del SDK será menor que la minSdkVersion de la aplicación. El sistema interrumpe la instalación o actualización de la aplicación.
* Si el usuario final ejecuta una versión superior a OS 2.3, la aplicación se instalará correctamente.

Si actualiza minSdkVersion:

* Si el usuario final ejecuta OS 2.3, la aplicación se instala, pero la reproducción no funcionará.
Esto se aplica tanto a la actualización como a la nueva instalación.
* Si el usuario final ejecuta un sistema superior a OS 2.3, la aplicación se instala correctamente y el contenido se reproduce correctamente.

**Versión 1.4.22**

* La salida anticipada de los anuncios no funciona con algunos de los anuncios mid-roll cuando los de splice-out y splice-in están demasiado cerca los unos de los otros.

**Versión 1.4.2**

* El rebobinado en una pausa publicitaria está provocando que la emisión se complete.

Media Player envía de forma incorrecta MediaPlayerState.Complete durante la operación de rebobinado Trick Play cuando llega a un límite del anuncio. El reproductor debe ignorar este evento cuando se encuentra en el modo de reproducción de trucos; de lo contrario, el SDK gestiona el estado correctamente.

**Versión 1.4.0 (1086)**

* PTPLAY-1634 - La misma etiqueta suscrita tiene diferentes marcas de hora en diferentes ventanas en vivo. Cuando se mueven ventanas en vivo, la misma etiqueta en cada una de ellas debe tener las mismas marcas de tiempo. Sin embargo, a veces, incluso las mismas etiquetas tienen marcas de tiempo diferentes.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE se ve a veces después de varios conmutadores a/desde el flujo alternativo en interrupciones
* Error #3726865 - Si un flujo LBA de velocidad de bits múltiple comienza desde un flujo de solo audio, el vídeo no se mostrará si se cambia a un flujo de audio/vídeo. Al comenzar por un flujo de audio/vídeo, este problema no se mostrará y puede cambiar correctamente entre los flujos de audio y audio/vídeo
* Error #3760144 - La resolución puede cambiar o parecer que impulsa cuando se pone en pausa un flujo en algunos dispositivos, como Kindle Fire 7 y Samsung Galaxy Nexus. Sólo observable bajo estrecha inspección
* Error #3761170 - seekToLocal in Live with Ads no puede volver a buscar en contenido de publicidad; es mejor utilizar las API currentTime para transmisiones en directo
* Error #3763370 - Las transmisiones en directo con anuncios ocasionalmente mostrarán dos marcadores de anuncio juntos cuando solo debería haber uno. Estos marcadores de publicidad representan el mismo anuncio y solo se reproducirá uno
* Error #3763373 - El marcador de anuncio puede desaparecer brevemente al buscar más allá de un anuncio en flujos de VOD. El marcador de anuncio se restaura y no hay otros efectos adversos en la cronología
* Algunos dispositivos tienen problemas de reproducción conocidos. Para obtener más información, consulte [Problemas conocidos del dispositivo en 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementación de referencia: la reproducción de trucos no se implementa en la aplicación de ejemplo.

## Problemas conocidos del dispositivo en 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Solución alternativa |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | Se espera un retraso de ABR, ya que está reiniciando el decodificador. |  |  |
| HTC Desire (diferente de HTC Desire HD) | QSD8250 | No se puede reproducir vídeo. Devuelve el error VIDEO_PROFILE_NOT_SUPPORTED. | Desire no proporciona un decodificador HW adecuado. Proporciona el decodificador SW de Stagefright. | Reinicie el dispositivo. |
| HTC EVO 4G | QSD8650 | Sin decodificador HW. | Qualcomm no tiene un decodificador HW. | Actualización a Android 4.x. |
| Kindle FireSystem versión 6.0 | TI OMAP4 | No reproduce flujos HLS. El vídeo en AIR no funciona. |  | Actualice a la versión 6.3 del sistema. |
| Kindle Fire HD | TI OMAP4 | Puede llegar a un estado en el que no pueda reproducir vídeo. Devuelve los errores VIDEO_PROFILE_NOT_SUPPORTED y UNRECOVERABLE_ERROR. | El decodificador de HW entra en un estado irrecuperable cuando la aplicación no apaga completamente el decodificador de HW, por ejemplo, después de encontrarse con un bloqueo. También sucede en las aplicaciones nativas del dispositivo. | Reinicie el dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE se bloquea después de varios conmutadores ABR. |  |  |
| Motorola Atrix | Tegra2 | Problemas generales de rendimiento con AVE en lugar de AIR. La reproducción de audio/vídeo se bloquea después de reproducirse entre 9 y 15 minutos. Bloqueos. | Posiblemente relacionado con openGLES que activamos en AIR. Se está investigando. |  |
| Nexus 7 (2.ª generación) | S4Pro APQ8064 (Qualcomm) | El dispositivo se bloquea cuando una película está en pausa durante más de 30 minutos. | Problema del dispositivo del que se ha informado a Google. | La aplicación debe agotarse el tiempo de espera para no permitir un estado de pausa prolongado. |
| Nexus S (GB) | Pájaro huzador | No se puede reproducir ningún vídeo con el decodificador HW. | No hay decodificador HW basado en Stagefright en Nexus S, por lo que para Android 2.3 utilizamos un decodificador SW. | Actualice a ICS. |
| Nexus S (ICS) | Pájaro huzador | El vídeo parpadea ocasionalmente. | Los datos incorrectos pueden hacer que el descodificador entre en un estado incorrecto. | Reinicie el dispositivo. |
| Nook TabletAndroid OS: 2,3 | OMAP TI 4 | El vídeo no se reproduce y la aplicación se bloquea. | Stagefright entra en un estado inestable después de ejecutar la aplicación durante un par de veces. Llamadas a mediaplayer::QueryCodecs se cuelgan. | Reinicie el dispositivo para restablecer el estado. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | No se puede instalar la aplicación SampleMediaPlayer. | Utiliza ARM v6 en lugar del chipset ARM v7 más común. FP/AIR no admite este dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | No se puede reproducir vídeo. | Este chipset es un decodificador desconocido para Android pre-ICS en AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | El rendimiento del vídeo no está a la par para este dispositivo. | El decodificador HW devuelve fotogramas decodificados con el PTS incorrecto. Parece que el decodificador utiliza el tiempo de descodificación en lugar de la hora de presentación. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | TI OMAP4 | Se bloquea al iniciar el vídeo. |  | Actualice a Android 2.3.7 o 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | De forma intermitente, el vídeo se bloquea y solo se reproduce audio, y luego deja de responder. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | El vídeo se bloquea. | Investigando. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | La transición MBR puede tardar hasta tres segundos. | Como solución para los bloqueos MBR, reiniciamos el decodificador para cada conmutador de flujo, que puede tardar hasta tres segundos. |  |
| Samsung Galaxy Y |  | No se puede instalar la aplicación SampleMediaPlayer. | Utiliza ARM v6 en lugar del chipset ARM v7 más común. FP/AIR no admite este dispositivo. |  |
| Xoom | Tegra | Se pierden algunos fotogramas para cambiar. El decodificador no se reinicia. | Límite OMXAL. |  |

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
