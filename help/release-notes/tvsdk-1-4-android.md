---
title: Notas de la versión de TVSDK 1.4 para Android
seo-title: Notas de la versión de TVSDK 1.4 para Android
description: Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 1.4.
seo-description: Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 1.4.
uuid: 8bd8ee42-7a1b-4c14-aad9-22804743e505
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: f1ebc1a8-185a-493a-9c00-a6102dffb128
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '7830'
ht-degree: 0%

---


# Notas de la versión de TVSDK 1.4 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 1.4 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 1.4.

## Nuevas funciones {#new-features}

**Versión 1.4.43**

**Carga segura de publicidad a través de HTTPS**

Adobe Primetime ofrece una opción para solicitar la primera llamada al servidor de publicidad en tiempo principal y CRS a través de HTTPS.

**alwaysUseAudioOutputLatency(valor booleano) en la clase MediaPlayer**

Cuando se establezca este parámetro, utilice la latencia de salida de audio en el cálculo de la marca de tiempo de audio.

Acepta un valor de parámetros booleanos. Si su valor es `True`, el cliente utiliza la latencia de salida de audio en el cálculo de la marca de tiempo de audio.

**Versión 1.4.42**

**Inserción parcial de Ad-Break:**
Experiencia similar a la televisión de unirse en medio de un anuncio sin activar el seguimiento del anuncio parcialmente visto.
Ejemplo: El usuario se une en el medio (a los 40 segundos) de una pausa publicitaria de 90 segundos que consta de tres anuncios de 30 segundos. Pasarán 10 segundos desde el segundo anuncio de la pausa.
* El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.
* Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Se activan los rastreadores solamente para el tercer anuncio.

**Versión 1.4.41**

No hay nuevas funciones.

**Versión 1.4.40**

No hay nuevas funciones.

>[!NOTE]
>
>No necesitará los cambios de API si está en una versión anterior a la 1.4.39.

**Versión 1.4.39**

* TVSDK está certificado con VHL 2.0.1 y con VHL 2.0.1 con Nielsen.
* Android TVSDK se actualiza para realizar solicitudes CRS desde el nuevo host de Akamai `primetime-a.akamaihd.net`.
* La nueva configuración de nombre de host proporciona envío de recursos CRS a través de HTTP y HTTPS (SSL) a buena escala.
* TVSDK admite la versión de Oreo de Android.
* Se agrega una nueva función a la `AdClientFactory` clase para admitir el registro de varios detectores de oportunidades:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   Esto debe devolver una matriz de PlacementOpportunityDetector. Ahora puede registrar varios detectores de oportunidades. Por ejemplo, para la función de salida publicitaria anticipada, se necesitaban dos detectores de oportunidad: uno para la inserción de publicidad y otro para la salida anticipada del anuncio. Solo debe implementar esta nueva función si ha implementado su propio AdvertisingFactory (y no ha utilizado DefaultAdvertisingFactory). Para obtener el comportamiento existente, debe crear un solo detector de oportunidades, como en la función createOpportunityDetector() y colocarlo en una matriz y devolver:

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

Corrección de errores para omisión de contenido en Android.

**Versión 1.4.35**

* **Información de publicidad de red**

   Las API de TVSDK ahora proporcionan información adicional sobre las respuestas VAST de terceros. El ID de publicidad, el sistema de publicidad y las extensiones de publicidad VAST se proporcionan en la clase NetworkAdInfo a la que se puede acceder mediante la propiedad networkAdInfo de un recurso de publicidad. Esta información se puede utilizar para la integración con otras plataformas de análisis de publicidad, como **Moat Analytics**.

**Versión 1.4.31**

**Compatibilidad con múltiples CDN para anuncios CRS**
* De forma predeterminada, todos los recursos transcodificados se alojarán en CDN propiedad de Adobe en Akamai. Con la última versión, el servicio de reempaquetado creativo de Adobe (CRS) permite cargar los elementos creativos transcodificados en varios CDN, según lo especificado por el cliente.
* Se añaden nuevas API al SDK de TVSDK para permitir la especificación de la dirección URL creativa final de CRS cuando no se utiliza la dirección URL predeterminada. Consulte la documentación para aprender a utilizar estas nuevas API.

**La versión 1.4.18** Primetime Android TVSDK ahora admite elementos creativos de Javascript VPAID 2.0 para permitir una experiencia de publicidad interactiva y enriquecida en flujo. Para obtener más información sobre VPAID 2.0, consulte Compatibilidad con [anuncios](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md)VPAID.

**Versión 1.4.17**

El AC-3 5.1 solo es compatible con Amazon FireTV.

**Versión 1.4.11**

* **Ad Fallback, Daisy encadenado en la lógica de selección de anuncios (Zendesk #3103** Para anuncios VAST (elementos creativos) con la regla de reserva activada, TVSDK trata una publicidad con un tipo MIME no válido como una publicidad vacía e intenta usar anuncios alternativos en su lugar. Puede configurar algunos aspectos del comportamiento de reserva.

Para obtener más información, consulte [Reproducción de anuncios para anuncios](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md)VAST y VMAP.

* **Video Heartbeat Library (VHL) actualizado a la versión 1.5**
   * Capacidad para enviar metadatos con inicio de vídeo y/o inicio de vídeo/anuncio/capítulo como datos de contexto
   * Menos tráfico de red: los latidos son menos en promedio y de menor tamaño

**Versión 1.4.7**

* **Asistencia** de individualización in situAsistencia para instalaciones in situ del servidor de individualización de Adobe para personalizar la solicitud de individualización del cliente para ir a un punto final diferente.

**Versión 1.4.6**

* **Cifrado AES de muestra (requiere la versión 17.0.0.134 de Flash Player)**Ahora se admite el cifrado AES de muestra.

**Versión 1.4.2**

* **Actualización de Video Heartbeat Library (VHL) a la versión 1.4.0.1**

   * Se añadió la capacidad de compilar diferentes casos de uso de análisis, desde otros SDK o reproductores, con Adobe Analytics Video Essentials.
   * El seguimiento de anuncios se ha optimizado eliminando los métodos trackAdBreakStart y trackAdBreakComplete. La pausa publicitaria se deduce de las llamadas a los métodos trackAdStart y trackAdComplete.
   * La propiedad playhead ya no es necesaria al rastrear anuncios.

* **Integración** de SDK de NielsenEl SDK de TVSDK ahora admite el envío de información de seguimiento de usuarios al SDK de Nielsen sin ninguna integración personalizada.

**Versión 1.4.0**

* **Señalización de interrupción con sustitución** de contenido alternativo Como parte de la actualización 1.4 del TVSDK, el TVSDK ahora también admite entrar y salir de interrupciones regionales en contenido lineal. TVSDK ahora puede procesar dos archivos de manifiesto en paralelo, principal y alternativo, para supervisar las señales de interrupción incluso cuando se muestra una programación alternativa en lugar de la programación original.

* **Eliminar o reemplazar publicidades** C3 Ahora, no se necesita ningún trabajo previo adicional para insertar dinámicamente nuevas publicidades en recursos de vídeo a petición (VOD) que salgan de la ventana C3. TVSDK ahora proporciona una API para eliminar intervalos de contenido personalizados e insertar publicidades nuevas de forma dinámica. Esta nueva y potente funcionalidad también es útil en casos en los que el contenido en directo/lineal se transmite durante la retransmisión y se baja inmediatamente para utilizarlo como contenido a petición sin tiempo suficiente para &quot;limpiar&quot; el recurso.

* La interfaz PlaybackEventListener tiene un nuevo método llamado onReplaceMediaPlayerItem, que puede utilizar para detectar un nuevo evento `ITEM_REPLACED`. Este evento se distribuye cada vez que se reemplaza una instancia de MediaPlayeritem en MediaPlayer. La aplicación cliente que implementa este PlaybackEventListener debe implementar o anular este nuevo método.
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

## Cambios de TVSDK para 1.4 {#tvsdk-changes}

* La interfaz PlaybackEventListener tiene un nuevo método llamado onReplaceMediaPlayerItem, que puede utilizar para detectar un nuevo evento, ITEM_REPLACED. Este evento se distribuye cada vez que se reemplaza una instancia de MediaPlayeritem en MediaPlayer. La aplicación cliente que implementa este PlaybackEventListener debe implementar o anular este nuevo método.

* AdClientFactory tiene una nueva función agregada a la clase para registrarse en varios detectores de oportunidad:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Por ejemplo, para la función de salida de publicidad anticipada, necesita dos detectores de oportunidad: uno para la inserción de publicidad y otro para la salida anticipada del anuncio.

Para anular esta nueva función, cree un único detector de oportunidades y colóquelo en una matriz y devuelva:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Compatibilidad y certificación de dispositivos en 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>TVSDK **no admite** las siguientes funciones:
>
>* Movimiento lento, en cualquier plataforma o versión.
>* Juego de trucos en vivo.


**Versión 1.4.43**

TVSDK 1.4.43 está certificado con dispositivos Android con Android 6.0.1/ 7.0 y 8.1 (Oreo).

* **Versión 1.4.23:**

   * TVSDK 1.4.23 se ha certificado para dispositivos Android con Android N.

* **Versión 1.4.18:**

   * Primetime ha sido certificado para Amazon Fire TV.
   * VPAID 2.0 solo se admite en dispositivos con Android 4.0 o posterior.

## Problemas resueltos en 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Se recomienda encarecidamente a todos los clientes de TVSDK que utilicen CRS que actualicen a TVSDK 1.4.39 o posterior en iOS y Android. Esta actualización sustituye a la implementación de la aplicación existente. Después de la actualización, compruebe las solicitudes de URL creativa de CRS en una herramienta proxy (por ejemplo, Charles) para comprobar que la versión de la ruta refleja la versión 3.1. Por ejemplo:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versión 1.4.43**

* ticket #27143 - No se puede reproducir la pista de audio 5.1 en dispositivos FireTV

   * TVSDK ahora puede reproducir audio AC3 en dispositivos FireTV. La reproducción siempre está en estéreo.

* Boleto #33902 - Envío publicitario seguro sobre HTTPS

   * Adobe Primetime ofrece una opción para solicitar la primera llamada al servidor de publicidad primetime y CRS a través de https.

* Billete n.º 34493 - Retraso de audio Bluetooth

   * Añadida `alwaysUseAudioOutputLatency` en la clase MediaPlayer que, cuando se establece, resultará en el uso de latencia de salida de audio en el cálculo de la marca de tiempo de audio.

* ticket #34949 - Nueva versión integrada de Video Heartbeat Library (VHL).

**Versión 1.4.42 (1791)**

* Zendesk #33719: La velocidad de bits adaptable FireTV de 4k se escala lentamente. Compatibilidad añadida con ABR para dispositivos FireTV 4K.
* Zendesk #33338:  resetDRM borra todos los datos de la aplicación.  Se han utilizado casos adicionales en los que las excepciones en subprocesos que no eran de TVSDK provocaban que se rellenaran las colas de operaciones de TVSDK.

**Versión 1.4.41 (1776)**

* Zendesk #33002 - Datos de recursos complementarios de TVSDK en Fire TV. Se implementó una nueva clase AdBannerAsset que devolverá los datos Companion como Lista &lt;AdBannerAsset> y AdAsset::id ahora es una cadena en lugar de larga.
* Zendesk #32821 - Android Primetime player se bloquea cuando encuentra la marca de tiempo de presentación (PTS) para WWE. Este problema se ha solucionado en esta versión.
* Zendesk #33572 - Error en el Inicio de anuncios de VideoAnalyticsProvider. El uso de la combinación adecuada de la versión conjunta del SDK de VHL+Nielsen de VideoHeartbeat.jar ha corregido este problema.
* Zendesk #33355 - Televisor de incendios: Anule 15 segundos números. No hay ninguna corrección por parte de TVSDK y los clientes están verificando esto en sus versiones de Fin y Tercero.

**Versión 1.4.40 (1764)**

* Zendesk #33068 - Problema de sincronización de labios de Amazon en el nuevo dispositivo. En esta versión se ha solucionado el problema de sincronización de clips.
* Zendesk #32215 - Problemas de seguridad de Android TVSDK 1.4.38 `[Hotlist]`. Actualizado a los últimos OpenSSL-1.1.0 y curl-7.55.1.
* Zendesk #32920 - Pantalla en blanco dentro de una pausa publicitaria y sin finalización de pausa publicitaria. Se corrigió un problema en el cual un contenedor VPAID podía pasar a un estado de bloqueo y se manejaba un problema en el cual las publicidades VPAID de Facebook solían devolver varios bloques CDATA en un solo \&amp;lt;AdParameters\&amp;gt; Nodo VAST.

**Versión 1.4.39 (1744)**

* Zendesk #28976 - La solicitud de licencia tarda más de un segundo. Mientras se ejecutan las llamadas de solicitud de licencia de DRM que utilizan POST, Curl agrega &quot;Expect: Encabezado &quot;100-continue&quot;. Se ha eliminado el encabezado &quot;Expect:&quot; en TVSDK.
* Zendesk #27707 - entornos de CSAI que no respetan los marcadores CUE IN para una pronta devolución o retorno al contenido. Se proporcionó compatibilidad para varios generadores de oportunidades.

**Versión 1.4.38 (1722)**

* Zendesk #21590 - Rendimiento y seguimiento de vídeo en los últimos Orígenes

Integración y certificación de VHL 2.0 en TVSDK para reducir la barrera en la implementación VideoHeartbeatLibrary disminuyendo la complejidad de las API.

* Zendesk #29688 - Compatibilidad con clientes de Android O Beta.

Compatibilidad con TVSDK para la nueva versión beta de Android.

**Versión 1.4.36 (1713)**

* Zendesk #27392 - Omisión de contenido en Android

Para dar cabida a la descodificación, el TVSDK de Android ampliaba incorrectamente el intervalo de bytes del contenido que no es iframe en 16 bytes. La ampliación es necesaria para flujos de iframe, pero no para flujos que no sean iframe.

**Versión 1.4.34 (1702)**

* Zendesk #27638 - Filtración en objeto cURL INet

El objeto Posix cURL INet presentaba una fuga mientras se mantenía en el administrador de recursos compartidos y la caché DNS que se utilizaban en las conexiones cURL.

Este problema se resolvió eliminando el objeto INet cURL de Posix del deconstructor INet.

**Versión 1.4.33 (1694)**

* **Biblioteca OpenSSL**

La biblioteca OpenSSL se ha actualizado con la versión 1.0.2j de OpenSSL.

* Zendesk #21701 - Envíe la URL creativa original para la solicitud de CRS 1401 en lugar de la URL normalizada.
Este problema se resuelve enviando las direcciones URL creativas originales.

* Zendesk #25023 - Reproducción de vídeo de larga duración: congelación de vídeo, parpadeos de pantallaEste problema se resolvió estableciendo las dimensiones máximas de formato de vídeo para los dispositivos set-top box CenturyLink.

* Zendesk #27460 - La nueva cuenta de Akamai no puede gestionar una solicitud de cdn de POST.
El código se actualizó para que la solicitud de `cdn.auditude.com` publicidad sea GET en lugar de POST.

* Zendesk #28245 - El estado de reproducción no se notifica correctamente cuando la aplicación pasa de fondo a primer planoEste problema se ha resuelto restaurando correctamente el estado de reproducción para que se reproduzca o se detenga cuando la aplicación vuelve al primer plano.

**Versión 1.4.32 (1682)**

* Zendesk #25779 - Vulnerabilidad de seguridad encontrada con TVSDKAndroid 4.2 y versiones posteriores tiene una vulnerabilidad de seguridad cuando JavaScript está habilitado en un WebView. El uso de WebView por TVSDK se ha desactivado para dispositivos que ejecutan OS 4.2 o inferior. Esto deshabilita el uso de anuncios VPAID en TVSDK en estos dispositivos.

* Zendesk #26890 - Problema en estado de PANTALLA (ENCENDIDO/APAGADO) con referencia. ReproductorCuando el motor de vídeo de Adobe (AVE) se reanuda a partir de un estado SUSPENDIDO, DefaultMediaPlayer no actualiza su estado. Como resultado, DefaultMediaPlayer permanece en un estado SUSPENDIDO aunque el AVE esté en estado REPRODUCIENDO. Este problema se ha resuelto estableciendo el estado DefaultMediaPlayer en PLAYING al recibir el estado PLAY del AVE, aunque el estado actual de DefaultMediaPlayer esté SUSPENDIDO.

**Versión 1.4.31 (1675)**

* Zendesk #21974 - Excepciones debidas a objetos nulos
   * AdIndex raramente se incrementa cuando es nulo. Esto puede deberse a llamadas de API incorrectas recibidas para adBreak previo al lanzamiento. Se corrigieron los tipos de datos para evitar estas excepciones

* Zendesk #24714 - Desactivar registro superfluo
   * Se ha actualizado TVSDK para desactivar el registro superfluo

* Zendesk #24488 - Problemas de sincronización AV en Fire TV
   * Se corrigió mejorando la gestión de los subprocesos del decodificador AV. Específicamente, cada vez que se modifican las colas de entrada o salida del marco, se ejecuta el subproceso de descodificador específico del tipo de contenido del marco.

* Zendesk #26551 - Corrección de errores de CRS
   * Cuando la solicitud es HEAD (http head), no es necesario que leamos el contenido porque está vacío. Aunque está bien tratar de leerlo, el antiguo Android (4.0.x) se bloquea mientras llamamos a read() y el nuevo Android devuelve el valor correcto (-1) cuando llamamos a read(). En función de esto, se cambió el código a no leer contenido para &quot;head&quot;

* Excepción de puntero nulo Zendesk #26696 al acceder a TrickPlayManager
   * Se corrigió al comprobar si el objeto TrickPlayManager no es nulo antes de utilizarlo.

**Versión 1.4.30 (1659)**

* Zendesk #22675 La duración de los recursos no se actualiza para flujos interactivos/linealesEste problema se ha resuelto proporcionando una nueva API, assetDuration, en PTVideoAnalyticsTrackingMetadata que proporciona la duración de los recursos para flujos interactivos y lineales.

* Zendesk #25853 Pérdida de memoria en TVSDK al cambiar de canalSe ha solucionado el problema de una fuga de búfer de lectura de archivo cuando se restablece o se libera MediaPlayer durante la descarga de un archivo.

**Versión 1.4.29 (1653)**

* Zendesk #21200 - El reproductor no se recupera del estado suspendido cuando la aplicación se encontraba en segundo plano. Cuando el reproductor se suspendió después de haber señalizado el cambio de flujo, la resolución permite al reproductor realizar el cambio de flujo al restaurar el reproductor del estado de suspensión, en lugar de restaurar a la posición anterior.

* Zendesk #23412 - El jugador está atascado con una casilla negra si hace clic en cualquier Anuncio dentro de los últimos tres años de la pausa publicitaria. Este problema es el mismo problema que Zendesk #21200.

* Zendesk #23616 - La pausa publicitaria omitida busca demasiado en el futuroSegún el tipo de inserción de publicidad (insertar/reemplazar), TVSDK determina si la duración de la publicidad se utiliza en el cálculo para determinar el punto final de la pausa publicitaria.

* Zendesk #25078 - DRM TVSDK Pérdida de memoria en Android TV STBTla fuga de memoria para el objeto de adaptador DRM se ha localizado y corregido.

* Zendesk #25067 - Bloqueo en VideoEngineTimelineEsto sucede porque los objetos no se limpiaron correctamente y se llamó a los eventos después de que se destruyeron los objetos. El problema se resolvió agregando comprobaciones para evitar excepciones nulas.

* Zendesk #25352 - Definición del encabezado HTTP personalizadoEste problema se resolvió agregando un nuevo encabezado personalizado a la lista de permitidos en TVSDK.

* Zendesk #25617 - El rollover PTS de flujo en directo provocaba la discontinuidad del reproductor y el bloqueo de memoriaEste problema se resolvió añadiendo un control de rollover PTS en FragmentedHTTPStreamer cuando se producía un rollover en medio de un segmento.

**Versión 1.4.28 (1637)**

* Zendesk #23618 - Los eventos de pausa publicitaria se activan antes de que se consulte la política de publicidad. Este problema se resolvió al no activar los eventos AD_BREAK_INICIO y AD_INICIO cuando el anuncio se omite debido al perdón publicitario. En su lugar, se envía el evento AD_BREAK_SKIPPED.

**Versión 1.4.27 (1631)**

* Zendesk #23174 - Problema de rendimiento al cambiar el tamaño del vídeoEste problema se resolvió probando una nueva API, MediaPlayerView.setSurfaceFixedSize, que permite que TVSDK acceda a SurfaceHolder.setFixedSize() desde MediaPlayerView.

* Zendesk #24450 - TVSDK realiza solicitudes de anuncios de duplicado Este problema se producía cuando el tiempo transcurrido se convertía a largo y no a doble, y este problema se ha solucionado.

**Versión 1.4.26 (1627)**

* Zendesk #21436 - Actualización de la biblioteca OpenSSL a la versión 1.0.2h
* Zendesk #23825 - Las cookies no se incluyen en las rellamadas corregidas proporcionando compatibilidad con las cookies androides.

**Versión 1.4.25 (1620)**

* Zendesk #22900 - El flujo DRM de Adobe Primetime en directo no se está reproduciendo en el reproductor de referencia de AndroidSe ha solucionado el problema de asignación de memoria.
* Zendesk #23176 - La aplicación se bloquea cuando intenta reproducir anuncios VPAIDEl bloqueo se produce porque la aplicación no crea una vista de publicidad personalizada para representar una publicidad VPAID. Este problema se resolvió ignorando las publicidades VPAID en la respuesta del servidor de publicidad cuando no hay ninguna vista de publicidad personalizada.

* Zendesk #23153 - SampleAES DRM Stream - Reproducción estancada en el reproductor de referencia TVSDKEste problema es el mismo que Zendesk #22900.

**Versión 1.4.24 (1612)**

* Zendesk #20784 - Análisis: Activación de finalizaciones de contenido para transiciones de vídeo en directoEste problema se resolvió añadiendo una API (trackVideoComplete) para activar manualmente la finalización de contenido durante una sesión de seguimiento de vídeo en directo o lineal.

* Zendesk #21977 VideoEngineCronología bloqueada durante la operación placeAdBreak/acceptAd
   * En este número, se actualizaron las bibliotecas siguientes:
      * Biblioteca de AdobeMobile con la versión 4.10.0
      * Biblioteca VHL a la versión 1.5.6
      * Biblioteca VHL-Nielsen a la versión 1.6.7

Este problema se resolvió agregando una marca de verificación nula antes de agregar publicidades a la lista de publicidad aceptada.

* Zendesk #22313 La velocidad de bits para los STBs con chipset Amilogic no va más allá de 1.2MTsu problema se resolvió al precargar las capacidades del códec de medios y deshabilitar el conmutador sin fisuras para los dispositivos de chipset Amilogic.

* Zendesk #19520 Recurso AES HLS de muestra que no se reproduce en reproductores TVSDKEste problema se resolvió al gestionar varios descriptores PMT para flujos HLS cifrados AES de muestra.

**Versión 1.4.23 (1602)**

* Zendesk #18852 - Actualización de la lógica de selección creativa basada en las reglas de CRSEste problema se resolvió añadiendo un archivo de configuración JSON para especificar la prioridad de selección creativa.

* Zendesk #20861 - Android NTesta versión ofrece compatibilidad con Android N al eliminar la posibilidad de utilizar directamente las bibliotecas nativas de la plataforma Android que ya no son accesibles para las aplicaciones que se ejecutan en Android N.

* Zendesk #21018 - Android N crashLa misma resolución que ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter se bloquea por un error Invalid_KeyEl error Invalid_Key no incluye una descripción del AVE, por lo que el análisis del texto resultó en NPE. El problema se resolvió agregando una comprobación nula de la descripción durante onError antes de analizar la descripción.

* Zendesk #22286 - La biblioteca nativa está asignando clave/fragmento de lectura de memoria que provoca el bloqueoEste bloqueo que se produjo en Android al intentar cargar un manifiesto con varias claves simultáneamente se ha corregido.

**Versión 1.4.22 (1581)**

* Zendesk #17236 - Tiempo de reproducción no fiable para vídeos HLS con DRMTse ha corregido el salto de tiempo con los flujos LBA, en el que el tiempo de inicio del segmento de audio no coincide con el tiempo de inicio del segmento de vídeo.

* Zendesk #17680 - La reproducción de vídeo se está bloqueando en el cuadro de edición AndredoEl decodificador de vídeo de este dispositivo a veces devuelve un salto de tiempo de salida significativo al eliminar el fotograma de vídeo del búfer de salida y esta marca de tiempo de salida permanece alta. Este problema se resolvió devolviendo un error de perfil de *vídeo no admitido* que no fuerza al reproductor a reintentar el mismo perfil o elegir un perfil diferente.

* Zendesk #19074 - Bloqueo de vídeo durante la reproducción de trucos de FFWD y REW Este problema se resolvió añadiendo una nueva advertencia TRICKPLAY_ENDED_DUE_TO_ERROR para notificar a la aplicación que se ha salido de la reproducción y que el vídeo se ha pausado debido a un error irrecuperable.

* Zendesk #19574 - TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM Este problema se ha resuelto de las siguientes formas:

* Zendesk #19986 - Comportamiento de OP dañado para determinados dispositivos como Android TV
* Añadiendo un error FILE_NOT_FOUND en la condición.
* Cuando el error proviene de un *archivo no encontrado* error, separando la dirección URL y la respuesta de la descripción del error si la respuesta está disponible.
Se ha solucionado el error lógico que introdujo la compatibilidad con NVidia shield OP. En dispositivos de protección que no son NVidia, confíe en los indicadores de seguridad de visualización incluso cuando se desconozca el tipo de visualización.

* Zendesk #20549 - Gestión de listas de reproducción antiguas. Este problema se resolvió reduciendo el intervalo entre la actualización del manifiesto activo y la mitad de la duración del segmento esperada, si la recuperación anterior no recibe nuevos segmentos.

* Zendesk #20742 - El uso de la memoria parece seguir aumentando cuando se reproduce contenido en directo en FireTV. El bloqueo se debe a la tabla de referencia de objetos JNI que ha alcanzado el límite. Este problema se resolvió eliminando la referencia al objeto MediaFormat que se creó durante el reinicio del decodificador.

* Zendesk #21125 - Regreso de la pausa publicitaria en directo/lineal antes de tiempo (CSAI). Se añadió una función que permite al reproductor volver al contenido principal durante una pausa publicitaria si el reproductor registra la empalme en señales publicitarias mediante el detector de oportunidades de splice.

* Zendesk #21334 - Valor de tiempo de espera de solicitud de publicidad TVSDK para solicitudes de publicidad de terceros. Se agregó una configuración adRequestTimeout a AdvertisingMetadata que habilita un tiempo de espera global para la llamada de publicidad.

**Versión 1.4.21 (1566)**

* Zendesk #17781 - La captura de pantalla de ADB ya no funcionaEste problema se resolvió agregando la API DefaultMediaPlayer.create(Context context, boolean secureSurface), que permite la captura de pantalla.
Para permitir capturas de pantalla, pase false para secureSurface.
Importante: Se recomienda encarecidamente no activar esta función de captura de pantalla en un ajuste de producción.

* Zendesk #19074 - Congelamiento de vídeo durante el juego de trucos FWD y REWse han resuelto los siguientes problemas que se producían cuando el juego de trucos podía congelarse en el reproductor:

* Zendesk #19532 - El subtítulo de cierre aparece fuera de orden
   * Los inicios FHS se reventan con trinquete, pero el primer segmento de iframe no tenía un fotograma.
   * Al descargar un segmento de iframe, si FHS detecta una condición de error, sale de la reproducción de trucos y pone en pausa la reproducción.
   * La implementación de MediaCodec de Android espera para siempre la disponibilidad de la cola de entrada mientras se le pedía que vaciara todos los búferes de entrada y salida.
Este problema se resolvió invirtiendo el orden de las indicaciones de WebVTT para que aparecieran varias pistas superpuestas para &quot;desplazarse hacia arriba&quot;.

* Zendesk #19574 - El TVSDK no devuelve datos de respuesta M3U8 para contenido DRM o no DRM. En la carga inicial del archivo de manifiesto en PTMediaPlayerItem.prepareToPlay, si la carga falla, el TVSDK no informa del cuerpo de la respuesta de error a la aplicación.
Este problema se resolvió permitiendo que el TVSDK informara de la respuesta de error como un error en la aplicación.

* Zendesk #19701 - Congelación de la reproducción con SAP/DiscontinuidadEl reproductor se bloquea cuando el audio y el vídeo se desalinean cuando se ha resuelto la discontinuidad.

* Se ha solucionado el error #PTPLAY-11162 - Se ha solucionado la actualización de la biblioteca OpenSSL a la versión 1.0.2f.

**Versión 1.4.20 (1546)**

* Zendesk #17384 - Solicitud de función: Compatibilidad con metadatos ID3 para la reproducción de AACnse ha proporcionado compatibilidad con etiquetas ID3 en medios AAC en el TVSDK para Android a partir de la versión 1.4.20.

* Zendesk #18358 - El reproductor se congela en el conmutador de velocidad de bits con discontinuidades no sincronizadasEste problema se resolvió manejando adecuadamente los casos de aristas de puntos ABR.

* Zendesk #19232 - La aplicación que utiliza TVSDK 1.4.18 se está comportando de forma extraña en la versión anterior de Amazon OS 4Este problema se ha resuelto eliminando la creación de vistas web ocultas en el proceso de inicialización del reproductor TVSDK para evitar conflictos con dispositivos que no admiten Android Webview.

* Zendesk #19585 - Reproducción de cámara lenta cuando se produce una transición de velocidad de bits adaptable.
Durante el cambio de ABR, si el nuevo perfil tiene una velocidad de muestreo de audio diferente a la del perfil actual, la reproducción se convierte en movimiento rápido o lento. Esto se debe a que no se notifica al presentador de vídeo que el formato de audio ha cambiado.
Este problema se resolvió asegurándose de que el indicador de notificación está establecido en el lugar correcto.

* Zendesk #19683 - Reproducción SAP DAI - Sin audio durante unos segundos.
En varios casos en la lógica del TVSDK, cuando se comparaba la marca de tiempo de dos segmentos de representación, se utilizaba RENDITION_TIMEOUT_THRESHOLD como un rango de valor aceptable, ya que la marca de tiempo no siempre se podía comparar con una diferencia de 0 ms. Si el espacio está dentro del rango de RENDITION_TIMEOUT_THRESHOLD, se supone que es una coincidencia.

El RENDITION_TIMEOUT_THRESHOLD se estableció en 100 ms, pero resultó insuficiente para determinados flujos. Este problema se resolvió aumentando el RENDITION_TIMEOUT_THRESHOLD a 200 ms.

* Zendesk #19699 - El TVSDK no puede cambiar entre las pistas de subtítulos de VTT. Este problema se resolvió haciendo que el reproductor volcara y volviera a cargar el manifiesto cuando cambia un seguimiento y corrigiendo el problema de conversión de cadenas UTF8 que afectaba a los nombres de seguimiento de subtítulos WebVTT de byte doble.

* Zendesk #19717 - Problema de visualización de opciones CC Este problema se resolvió al gestionar correctamente la cadena Unicode.

* Zendesk #19910 - No se detectaron las etiquetas TIT2 ID3. Este problema se resolvió proporcionando una compatibilidad más completa para las codificaciones de cadenas ID3 v2.4 y para la compatibilidad con ID3 v2.3.

* Zendesk #20135 - El TVSDK activa varios onComplete para contenido de VOD.
Este problema se resolvió agregando el detector de evento post_roll_complete en el lugar correcto, en lugar de en la mayúsculas y minúsculas del evento de cambio de estado.

**Versión 1.4.19 (1521)**

* Zendesk #4180 - El TVSDK no está aplicando HDCP.
   * Esta es una corrección parcial para este ticket y aborda solamente el problema de los dispositivos de protección NVidia.
Debe utilizar la API de detección de HDCP implementada correctamente en Nvidia Shield para realizar un seguimiento dinámico del estado de HDCP.

* Zendesk #18358 - El TVSDK se bloquea en el conmutador de velocidad de bits sin interrupciones no sincronizadas.
   * Este problema se resolvió agregando una nueva advertencia para detectar la discontinuidad de PTS y obligando a la comprobación de PTS a rehacer la búsqueda del segmento correcto para cada conmutador ABR.
Para corregir el bloqueo, la llamada al método mediaPlayer.setCustomConfiguration debe incluir forcePTSCheckForABR como argumento.

* Zendesk #19038 - No hay transmisión en vivo en Asus Zenpad 10.

   Este problema se resolvió al precargar la información del códec de medios, de modo que no se consulta la función en tiempo de ejecución.

* Los siguientes problemas son los mismos que Zendesk #19038:
   * Zendesk #19483 - El TVSDK se está bloqueando en la plataforma Intel.
   * Zendesk #19171 - Bloqueos en Asus Memo Pad 7 con Android 5.0.

**Versión 1.4.18 (1503)**

* Zendesk #3324 - El sistema de informes de anuncios Primetime no rastrea las pausas publicitarias cuando no hay medios publicitarios en un VMAP.
Cuando una pausa publicitaria está vacía, el inicio de la pausa publicitaria y los eventos de seguimiento completos no se estaban ping. Este problema se resolvió enviando pings de inicios de desglose de anuncios en los saltos de anuncios vacíos, como por ejemplo AdBreak de VMAP, con un nodo AdSource válido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) se omite después de llamar a MediaPlayer.reset(). Este problema se resolvió añadiendo setCCVisibility(Visibility.INVISIBLE); a la función reset() en la clase MediaPlayer.

* Zendesk #18328 - Se ha eliminado el problema de los fotogramas en los dispositivos de segunda generación de Amazon Fire TV para los contenidos con 60FPSTsu problema se ha resuelto aplicando el FPS codificado para la toma de decisiones en tiempo de espera y con una lógica de predicción FPS mejor codificada.

**Versión 1.4.17 (1472)**

* Zendesk #2231 - Error al recuperar el manifiesto no disponible en MediaPlayerNotificationEste problema se resolvió incluyendo el cuerpo de respuesta del manifiesto cuando se producía un error de análisis.

* Zendesk #17703 - VideoEngineView no impide las capturas de pantalla durante la reproducción de vídeo. El método setSecure ha estado disponible desde la API 17, pero como la API 17 abarca 4.2, 4.2.1 y 4.2.2, no se sabe cuál generará una excepción o si es específica del dispositivo. Este problema se resolvió ajustando VideoEngineView.setSecure a la cláusula try catch.

* Zendesk #17919 - La búsqueda de contenido causa un error de latidoSe producía un error de posición de datos de entrada no válido como resultado de la llamada de latido que se generó cuando se inició la búsqueda después del prelanzamiento. Este problema se ha resuelto.

**1.4.16a** (1454a)

* Zendesk #18215 - Algunos flujos AES no pueden cargarse.
Este problema se resolvió comprobando el tamaño de metadatos DRM de perfil antes de cargar la clave AES.

**Versión 1.4.16 (1454)**

* Zendesk #3875 - Tab S se bloquea durante la reproducciónRevertir la dependencia de OKHTTP en Auditude para CRS porque TVSDK ahora utiliza httpurlconnection directamente en lugar de curl. El problema se resolvió eliminando excepciones antes de realizar cualquier otra llamada de JNI.

* Zendesk #4487 - Seguimiento del Canal lineal del contenido El problema se resolvió permitiendo la reinicialización del rastreador de Video Heartbeat durante una sesión de reproducción lineal de flujo.

* Zendesk #17919 - Android - la búsqueda de contenido causa un error de latidoSe ha solucionado el problema de los latidos cuando hay una búsqueda en un capítulo.

* Zendesk #18053 - Adobe Primetime se bloquea en MarshmallowEl SDK de TVSDK se bloqueaba en Android M OS cuando la biblioteca TVSDK utilizaba código neon que realiza la conversión de color YUV -> RGB. El problema se resolvió actualizando las funciones que causan este problema mediante la versión no neón del código.

* Zendesk #18072 - Android M - Application CrashAl comprobar si el perfil y el nivel son compatibles, se produce un bloqueo al llamar a las API MediaCodecList y MediaCodecInfo. El problema se resolvió proporcionando un trabajo temporal cargando toda la información del códec con antelación para evitar llamar a estas API solo cuando se necesita información del códec.

* Zendesk #18074 - Subtítulos en árabe que no funcionan en Nexus con Android 6.0El problema se resolvió proporcionando compatibilidad con mapas de fuentes CTS para Android.

**Actualización de la versión 1.4.15 (1438)**

* Zendesk #17437 - Largo retraso en el inicio del contenido de VOD con algunos flujos de AES.
Para resolver este problema, si hay varias claves enumeradas en el manifiesto, descargue todas las claves AES en paralelo.

**Versión 1.4.15 (1435)**

* Zendesk #4278 - Glitches on Android establece los primeros cuadros cuando cambia la velocidad de bits adaptable (ABR).
La corrección era añadir compatibilidad para el conmutador ABR sin problemas con el último códec de medios Android.

* Zendesk #17063 - Al llamar a mediaPlayer.reset(), se produce un error de restablecimiento del motor de vídeo.
La corrección consistía en incluir el MediaErrorCode original de VideoEngineExceptions al enviar eventos de error.

* Zendesk #17130 - Una breve pero notable pausa cuando se cambia la velocidad de bits vista en FireTV.
(Igual que el número 4278 anterior) La corrección consistía en añadir compatibilidad con el conmutador ABR sin interrupciones con el último códec de medios Android.

* Zendesk #17666 - Marcadores de publicidad adicionales, inesperados o sin anuncios al reanudar el contenido.
La corrección era un problema al realizar prepareToPlay en contenido de vídeo a petición (VOD), la búsqueda inicial se realizaba en tiempo local en lugar de en tiempo virtual.

* Zendesk #17437 - Largo retraso en el inicio del contenido de VOD con algunos flujos de AES.
La corrección consistía en descargar todas las claves AES en paralelo cuando aparecen varias claves en el manifiesto.

* Zendesk #17851 - Android TV - Black Frame durante ABRTla corrección era especificar KEY_MAX_WIDTH y KEY_MAX_HEIGHT para habilitar la reproducción adaptable.

**Versión 1.4.14 (1415)**

* Zendesk #3875 - La ficha S se bloquea durante la reproducción.
Se requiere una corrección adicional para evitar el bloqueo.

* Zendesk #17245 - Las réplicas en Android TV no funcionan.
Se ha corregido un problema adicional que hacía que la reproducción se bloqueara cuando la opción de reserva estaba activada y la respuesta de VMAP tenía una pausa publicitaria vacía.

**Versión 1.4.14 (1412)**

* Zendesk #17245 - Las réplicas en Android TV no están funcionando.
Se ha eliminado una restricción para desactivar el reempaquetado creativo en las publicidades de reserva.

**Versión 1.4.13 (1388)**

* Zendesk #3502 - Compatibilidad con failover basado en cliente HLS durante una pausa publicitariaPermitir la conmutación por error al manifiesto principal cuando se produce un error de perfil activo durante el período de pausa publicitaria.

* Zendesk #3875 - Tab S se bloquea durante la reproducciónPara resolver el conflicto entre HttpUrlConnection y cURLm, utilice una biblioteca de terceros.

* Zendesk #4450 - problema al configurar metadatos personalizados para una sola colocación en una resolución de contenidoAgregar un establecedor a la configuración de oportunidad.

**Versión 1.4.12 (1388)**

* Zendesk #2751 - CSAI y CRS | Mejorar: Gestionar elementos dinámicos en determinadas direcciones URL de archivos multimedia.
Se ha actualizado el servicio de reempaquetado creativo para gestionar correctamente las publicidades con direcciones URL creativas dinámicas.

* Zendesk #3965 - Al volver a la reproducción normal desde el trickplay, el resultado es un salto hacia delante un poco antes de iniciar la reproducción.
   * La corrección incluye que TVSDK devuelva el tiempo antes del cambio de velocidad hasta que se actualicen todas las variables, en lugar de intentar calcular GetStreamTime.
   * Se corrigió un bloqueo al cambiar la velocidad de reproducción de trucos cerca del final del flujo.
   * Se corrigió el cálculo de tiempo actual durante la reproducción de trucos.

* Zendesk #3978 - El juego de trickplay a 8x y 16x se congela con frecuencia.
   * Siempre elija el perfil de reproducción de trucos con la velocidad de bits más baja para evitar el almacenamiento en búfer constante.
   * Aumente el intervalo de omitir fotograma para una velocidad de reproducción de trucos alta.
   * Se ha corregido un problema que hacía que el búfer siguiera creciendo después de alcanzar la longitud de destinatario durante la reproducción mediante trucos.

* Zendesk #3992 - Velocidades adicionales de los trickplay.
TrickPlay se ha actualizado para aceptar tasas superiores a 16x; +/- 32, +/-64 y +/-128 ahora también están permitidos.

* Zendesk #4007 - Interpretación del objeto GEOB como parte de los metadatos de la línea de tiempo (Android y Web).
API setByteArray y getByteArray añadidas.

* PTPLAY-7301 - inicio instantáneo en punto de acceso aleatorio.
Instant On se ha actualizado para permitir un punto de partida distinto de cero.

**Versión 1.4.11 (1363)**

* Zendesk #2076 - Frecuente tartamudeo al reproducir vídeo en Motorola Xoom con dispositivos Android 4.0.3 Añadido a la lista de permitidos para evitar que intenten reproducir contenido de alto perfil.

* Zendesk #2197 - `[Ads]` Seguimiento de errores de envío OperationFailedEvent con notificación de advertencia.

* No se rellena la macro de Zendesk #3304 - VAST 3.0 `[ERRORCODE]`
   * el código de error 400 se mostrará si la publicidad en línea tiene un elemento creativo incorrecto.
   * `[ERRORCODE]` la macro estará codificada para la dirección URL

**Versión 1.4.10 (1354)**

* Zendesk #2941 - Los recursos activos no tienen &quot;0&quot; en el rango buscableAnteriormente había un búfer de 3 segmentos cuando se buscaba el principio de un flujo en directo, ahora es posible buscar el principio mismo de un flujo en directo (es decir, el inicio del primer segmento).

* Zendesk #3169 - Actualización del reproductor de referencia con la integración de Adobe AnalyticsEl reproductor de referencia se ha actualizado con la biblioteca Adobe Analytics como ejemplo de implantación.
* Zendesk #3299 - Comportamiento inexplicable del juego de trucos
   * Se ha corregido un error por el que volver al estado de reproducción después de detener la reproducción mediante trucos podía tardar varios segundos (a veces más de 25 segundos).
   * Se ha corregido un error que provocaba que el truco de invocación se reprodujera por segunda vez en el mismo medio, lo que podía hacer que el flujo se bloqueara en el momento actual.
* Zendesk #3433 - Android y Flash - Problemas con subtítulos

GetLine para WebVTT no respetaba una longitud ajustada &lt;CR>&lt;LF> para un paquete; el último rótulo puede contener caracteres de rótulos anteriores.

* PTPLAY-6243 - Mejore el reproductor de referencia para capturar información de depuración

Los reproductores de referencia de ejemplo de Android se han mejorado con una opción para activar los registros de depuración y enviar los resultados por correo electrónico. Esta opción se encuentra en el menú Registro del reproductor de referencia.

**Versión 1.4.9 (1332)**

* Zendesk #2649: el búfer completado se produce antes de que el búfer inicial esté lleno

Después de una búsqueda, es posible que el motor de vídeo defina el estado PLAYING antes de que el presentador de vídeo esté listo para la reproducción. Se produce cuando el estado del búfer es alto antes de la búsqueda. Se corrige notificando al motor de vídeo el estado del búfer bajo. Con el estado del búfer bajo del motor de vídeo, la llamada a Reproducir provoca un cambio de estado en BUFFERING en lugar de PLAYING. La reproducción se reanuda cuando el estado cambia a REPRODUCCIÓN.

* Zendesk #2846 - Solicitud de mejora: Permite establecer diferentes cadenas de usuario-agente para las llamadas realizadas por la biblioteca de audiencias

Se ha agregado una nueva API para establecer el agente de usuario para las llamadas relacionadas con la publicidad, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Si no se establece ningún agente de usuario, se utilizará el valor predeterminado. Esto solo afecta al agente de usuario para llamadas relacionadas con la publicidad, el agente de usuario para llamadas de medios no cambia, que es &quot;Adobe Primetime&quot;+&lt;agente de usuario predeterminado>.

**Versión 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Error local... Si se produce un error al cargar el manifiesto en FragmentedHTTPStreamer::ThreadParseManifest(), compruebe si el dominio de URL es localhost y, si es así, cambie el dominio a 127.0.0.1 y recupere ThreadParseManifest.
* Zendesk #3072 - Cambio automático a velocidades de bits más bajas. Se ha cambiado el cálculo de la longitud del búfer para omitir la carga útil PTS cero.
* Zendesk #3168 - Los subtítulos WebVTT solo se muestran durante los primeros 10 segundos.
* Zendesk #3193 - Se ha añadido la solicitud de una API de cambio de Perfil en TVSDK, PlaybackEventListener.onProfileChanged().

**Versión 1.4.7 (1311)**

* Zendesk #2197 - Seguimiento de errores de publicidad. La notificación añadida para el recurso no pudo cargar el manifiesto
* Zendesk #2575 - PSDK ignora el anuncio MARK personalizado en el flujo antes del vídeo
* Zendesk #2719 - Win Death with auditude ads, seguimiento de señalizaciones fijo cuando se redirige a la dirección URL relativa en el complemento de audiencias
* Zendesk #2760 - Etiqueta DISCONTINUITY ignorada durante el modo TrickPlay
* Zendesk #2805 - Bloqueo del reproductor al comienzo de la reproducción, la misma corrección que Zendesk #2719
* Zendesk #2817 - Reproductor de Android - El reproductor a veces se bloquea y deja de reproducir, corregido al ampliar los búferes de descodificación de 2,0 a 3,0 segundos
* Zendesk #2839 - ¿Adobe Primetime PSDK admite chipsets ARMv8?, se ha añadido una corrección para el bloqueo que se encuentra en Galaxy S6.
* Zendesk #2885 - Reproducción de bloqueo de audiencia, la misma corrección que Zendesk #2719
* Zendesk #2895: error de HLS en directo de forma consistente tras 10 minutos de reproducción
* Zendesk #2925 - Comentarios respecto a la compilación de desarrollo de Android (1.4.5), en determinados dispositivos cuando ponemos el paquete en la cola de entrada, si el PTS es negativo, el decodificador pasa a un estado extraño de que siempre obtenemos un PTS de salida negativo para futuros paquetes. La corrección establecerá la PTS de entrada en cero si es negativa para evitar este problema.
* PTPLAY-4645 - Desactive la compatibilidad con cifrado RC4 en openssl. Existen explosiones conocidas para RC4. Esto significa que si se intenta conectar con un servidor que solo admite RC4, se producirá un error.

**Versión 1.4.6 (1282)**

* Zendesk #2192 - La velocidad de bits no siempre disminuye en las malas condiciones de red, ya que se corrige eliminando la rápida implementación del conmutador.
* Zendesk #2631 - Subtítulos en árabe en Android: El texto de varias líneas aparece cortado, corregido por el ajuste del tamaño de fuente de las fuentes árabes.
* Zendesk #2844 - El almacenamiento en búfer en la Nota 4 y el tiempo de descarga del fragmento no es exacto.

Este problema se ha corregido agregando latencia entre las descargas de segmentos de vídeo en el cálculo del ancho de banda y haciendo que la lógica de cálculo del tiempo de descarga utilice el tiempo completo del ciclo de solicitud.

* Zendesk #2908 - Subtítulos en árabe que no funcionan en Nexust 5, 6 y 7, se corrigen agregando dos fuentes de reserva más para scripts en árabe.
* PTPLAY-4627 - actualizar la aplicación Nielson a la versión 1.2.3.7
* PTPLAY-5084 - Compatibilidad con failover de actualización de manifiesto maestro activo

**Versión 1.4.5 (1248)**

* Zendesk #1757 - Se ha corregido el bloqueo del Nexus 4 y Nexus 7 solo en el audio reproducido o el reproductor se bloquea en algunos perfiles de velocidad de bits de vídeo
* Zendesk #2072 - TimedMetadata para AdEvent no contiene la dirección URL completa solo &quot;http&quot;
* Zendesk #2192 - La velocidad de bits no siempre baja en malas condiciones de red
* Zendesk #2256 - Acceso a la lista de reproducción maestra, PSDK actualizado para distribuir eventos timedMetadata para las etiquetas suscritas en la lista de reproducción maestra.
* Zendesk #2269 - Dos idiomas de subtítulos diferentes aparecen en la pantalla al mismo tiempo que WebVTT
* Zendesk #2417 - El reproductor que intentaba descargar subtítulos antes del inicio de reproducción, WebVTT estaba usando la variable de número de segmento incorrecta para la coincidencia de número de segmento. El error solo se mostraba para los medios que tenían índices de segmentos que empezaban en cero.
* Zendesk #2470 - PSDK no regresa del estado SUSPENDED cuando se produce un cambio en la velocidad de bits después de la suspensión. En una situación especial en la que RestoreGPUResource (restore player from cancel state) llama a la búsqueda inteligente y el conmutador de flujo detectado antes, la búsqueda inteligente no puede completarse y resulta en un almacenamiento en búfer constante.
* Zendesk #2451 - Subtítulos opcionales &#39;inserción inferior&#39;, parámetro &#39;bottomInset&#39; añadido al código de subtítulo
* Zendesk #2480 - Desactivación de la optimización de redireccionamiento HTTP 302, Añade la compatibilidad con la configuración de la propiedad useRedirectUrl
* Zendesk #2486 - señalizaciones de terceros
* Zendesk #2547 - subtítulos en árabe: El texto debe alinearse con la justificación correcta

**Versión 1.4.4 (1195)**

* Zendesk #1158 - Falla la reproducción en el valiante Huawei (Y301A1)
* Zendesk #1709 - Tamaño incorrecto de los medios y vídeo estirado
* Zendesk #1757 - Solo se reproduce el audio después del cambio de perfil entre flujos con datos idénticos de spa/ps
* Zendesk #2095 - Estado HTTP 307 (redirección) hace que el reproductor de Adobe detenga la reproducción
* Zendesk #2126 - Falta el evento TimedMetaData para el último ADEVENT, las etiquetas suscritas que existen después del último segmento no se notificaron al PSDK desde AVE
* Zendesk #2227 - Bloqueo en VideoEngine nativeReset y nativePause
* Error #3921755 - Actualización de la biblioteca OpenSSL a la versión 1.0.1L

**Versión 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Encendido y apagado de subtítulos
* PTPLAY-1818 - El juego de trucos de rebobinado se detiene en el anuncio en lugar de retroceder más allá
* PTPLAY-2736: se muestra en pantalla un rótulo WebVTT que se ha mostrado anteriormente cuando se termina de reproducir un flujo con un rótulo WebVTT
* PTPLAY-3773 - No se reproduce un anuncio intermedio cuando se inicia la reproducción del flujo después de la posición del anuncio

**Versión 1.4.2**

* Zendesk #1561: compatibilidad con failover basado en cliente HLS en horario estelar. Utilizará la fecha y hora del programa para abordar la conmutación por error
* Zendesk #1590 - LoadInfo.MediaDuration siempre es 0 (no se corrige solo para audio)
* Zendesk #1626 - Posible fuga de memoria en el reproductor. No se produjo una fuga de memoria real, se produjo un problema con NotificationHistory que guardaba las últimas 1000 notificaciones, se ha reducido a 100.
* Zendesk #2192 - La velocidad de bits no siempre baja en malas condiciones de red

**Versión 1.4.1 (1121)**

* Zendesk #1951 - Bloqueo en VideoEngine.nativeReset() en dispositivos 4.0.x
* Zendesk #2064 - Native Crash SIGSEGV en dispositivos Android específicos basados en intel
* Zendesk #2075 - Bloqueo en VideoEngine.nativeReleaseGPUResources en dispositivos 4.0.x Nota: Esta compilación es ***obligatoria*** para la compatibilidad con Android 5.0 (Lollipop)
* Zendesk #1513 - Compatibilidad con Android Lollipop
* Zendesk #1709 - Tamaño incorrecto de los medios y vídeo estirado
* Zendesk #1871 - Los subtítulos WebVTT desaparecen ocasionalmente y vuelven a aparecer al ver una emisión en directo con subtítulos WebVTT
* Zendesk #1996 - No se ven marcadores de línea de tiempo en PSDK 1.4.0
* Zendesk #2046 - Bloqueo con PSDK 1.4.1.1113, bloqueo corregido para flujos en directo cuando no se devuelve ningún anuncio de la audiencia
* Error #3769657 - Actualizar la versión de curl a 7.38.0
* PTPLAY-1575 - Cuando la reproducción de ABR se inicio con un flujo de solo audio y luego cambia al flujo de audio/vídeo, el vídeo nunca se procesa mientras el audio continúa
* PTPLAY-2499 - Actualización a OpenSSL a la versión 1.0.1j para abordar las vulnerabilidades recientes
* PTPLAY-2632 - El vídeo no se recupera después de completar el anuncio de mitad de ciclo en Android Lollipop
* PTPLAY-2678 - Paradas de vídeo durante pruebas de longevidad en directo en Android Lollipop

**Versión 1.4.0**

* Zendesk #1024 - Función para eliminar anuncios del flujo mediante manifiesto
* Zendesk #1293 - Problema de selección de pista de subtítulos opcionales.
* Zendesk #1590 - LoadInfo.MediaDuration siempre es 0, mediaDuration ahora muestra el valor correcto.
* Zendesk #1629: el reproductor/aplicación se bloquea al final de la reproducción del anuncio en Galaxy S4
* Zendesk #1674 - ClosedCaption No aparece, se muestra correctamente el 708 subtítulos cuando faltan los códigos 0x03 ETX.
* PTPLAY-2157 - Los captadores devolvían los estilos de subtítulos opcionales predeterminados aunque se hubieran definido y verificado visualmente en el flujo diferentes estilos. Las propiedades de estilo de subtítulos opcionales ahora mostrarán el valor en el que se han establecido.

## Problemas conocidos en 1.4 {#known-issues-in}

**Versión 1.4.31**

* PTPLAY-16803 - Los subtítulos opcionales no funcionan con contenido de solo audio, ya que el sistema de subtítulos necesita vídeo para poder funcionar. Sin vídeo, no hay ninguna dimensión de ventanilla móvil y sin una dimensión de ventanilla móvil, no podemos mostrar gráficos para rótulos.
* PTPLAY-1634 - La misma etiqueta de suscripción tiene distintas marcas de hora en diferentes ventanas activas. Cuando se mueve la ventana activa, la misma etiqueta debe tener las mismas marcas de hora. Sin embargo, a veces incluso las mismas etiquetas tienen marcas de hora diferentes.
* PTPLAY-3197 - Bloqueo con el error de señal 11 SIGSEGV en el dispositivo Acer Iconia después de aproximadamente 1 hora de reproducción continua
* PTPLAY-3310 - Con una velocidad de bits más baja, el audio se vuelve entrecortado/entrecortado en Acer Iconia
* PTPLAY-3355 - WIN MUERTE se bloquea en Motorola Xoom con 4.0.x después de ~ 1 hora de reproducción continua.
* PTPLAY-3557 - El rebobinado en una pausa publicitaria está provocando que el flujo se complete
* PTPLAY-7079 - La ventana de reproducción en el cliente androide no funciona con Parada segura/Parada dura
* Error #3760144 - La resolución puede cambiar o parecer que impulsa cuando el flujo se pone en pausa en algunos dispositivos como Kindle Fire 7 y Samsung Galaxy Nexus. Sólo observable bajo estrecha inspección
* Error n.º 3761170 - SearchToLocal en directo con anuncios no puede volver a buscar en el contenido de la publicidad, lo mejor es usar las API de tiempo actual para flujos en directo
* Error #3763370 - Las transmisiones en directo con anuncios ocasionalmente mostrarán dos marcadores de publicidad juntos cuando solo debería haber uno. Estos marcadores de publicidad representan el mismo anuncio y solo se reproducirá uno
* Error #3763373 - El marcador de publicidad puede desaparecer brevemente al buscar más allá de un anuncio en flujos VOD. El marcador de publicidad se restaura y no hay ningún otro efecto adverso en la línea de tiempo
* Algunos dispositivos tienen problemas de reproducción conocidos. Consulte Problemas [conocidos del dispositivo en 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementación de referencia: la reproducción de trucos no se implementa en la aplicación de ejemplo
* En algunos dispositivos de TV Android, se puede ver un fotograma negro debido a un restablecimiento del decodificador en los siguientes puntos de transición:
   * entrada y salida del modo de reproducción irregular
   * cambio entre pistas de audio de enlace tardío
   * de una publicidad al contenido principal.

**Versión 1.4.23**

* El subtítulo cerrado no funcionará con contenido de solo audio porque el sistema de subtítulos necesita que el vídeo funcione. Sin vídeo, no hay ninguna dimensión de ventanilla móvil y, sin ella, no se puede mostrar ningún gráfico para los rótulos.
* A partir de la versión 1.4.23, el TVSDK no será compatible con Gingerbread OS 2.3. Esto se debe a que el TVSDK utilizó las siguientes bibliotecas privadas de Android para recopilar información de hardware sobre dispositivos con el sistema operativo Gingerbread:

   * `libstagefright.so`
   * `libcutils.so`

En la versión de Android N, Google ha eliminado el acceso a estas bibliotecas privadas. El sistema operativo Gingerbread representa actualmente menos del 1 % de la cuota de mercado del sistema operativo Android en todo el mundo, por lo que después de la versión 1.4.23, el sistema operativo Gingerbread ya no será compatible con el TVSDK.
Cuando utilice la versión 1.4.23 (que incluye compatibilidad con Android N) o posterior:
* Actualice sus aplicaciones para utilizar la versión 11 de minSdkVersion.
* Si el usuario final está ejecutando OS 2.3, la versión del SDK es inferior a minSdkVersion de la aplicación. El sistema anula la instalación o actualización de la aplicación.
* Si el usuario final está ejecutando una versión superior a OS 2.3, la aplicación se instalará correctamente.

Si actualiza minSdkVersion:

* Si el usuario final ejecuta OS 2.3, la aplicación se instala pero la reproducción no funcionará.
Esto se aplica tanto a la actualización como a la nueva instalación.
* Si el usuario final está ejecutando un sistema superior a OS 2.3, la aplicación se instala correctamente y el contenido se reproduce correctamente.

**Versión 1.4.22**

* La salida anticipada de las publicidades no funciona con algunas de las publicidades intermedias cuando las etiquetas de empalme y empalme están demasiado próximas entre sí.

**Versión 1.4.2**

* El rebobinado en una pausa publicitaria está provocando que se complete el flujo.

Media Player envía de forma incorrecta MediaPlayerState.Complete durante la operación de rebobinado Trick Play cuando alcanza el límite del anuncio. El reproductor debe ignorar este evento cuando se encuentra en el modo de reproducción ficticia; de lo contrario, el SDK gestiona el estado correctamente.

**Versión 1.4.0 (1086)**

* PTPLAY-1634 - La misma etiqueta de suscripción tiene diferentes marcas de hora en diferentes ventanas activas. Cuando se mueven ventanas en vivo, la misma etiqueta de cada una de ellas debe tener las mismas marcas de hora. Sin embargo, a veces incluso las mismas etiquetas tienen marcas de hora diferentes.
* PTPLAY-2541 - A veces, COMPONENT_CREATION_FAILURE se ve después de varios conmutadores que conducen o salen del flujo alternativo en apagones
* Error #3726865 - Si un flujo LBA de varias velocidades de bits inicio desde un flujo de solo audio, el vídeo no se mostrará si se cambia a un flujo de audio/vídeo. El inicio desde un flujo de audio/vídeo no mostrará este problema y puede cambiar correctamente entre flujos de audio y audio/vídeo
* Error #3760144 - La resolución puede cambiar o parecer que impulsa cuando se pone en pausa un flujo en algunos dispositivos como Kindle Fire 7 y Samsung Galaxy Nexus. Sólo observable bajo estrecha inspección
* Error #3761170 - SearchToLocal en vivo con anuncios no puede volver a buscar en contenido de publicidad; es mejor utilizar las APIs currentTime para flujos en directo
* Error #3763370 - Las transmisiones en directo con anuncios ocasionalmente mostrarán dos marcadores de publicidad juntos cuando solo debería haber uno. Estos marcadores de publicidad representan el mismo anuncio y solo se reproducirá uno
* Error #3763373 - El marcador de publicidad puede desaparecer brevemente al buscar más allá de un anuncio en flujos VOD. El marcador de publicidad se restaura y no hay ningún otro efecto adverso en la línea de tiempo
* Algunos dispositivos tienen problemas de reproducción conocidos. Para obtener más información, consulte Problemas [conocidos de dispositivos en 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementación de referencia: la reproducción de trucos no se implementa en la aplicación de ejemplo.

## Problemas conocidos del dispositivo en 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Solución alternativa |
|--- |--- |--- |--- |--- |
| Droid X | OMAP3 TI | Se espera un retraso en ABR, ya que se está reiniciando el decodificador. |  |  |
| HTC Desire (diferente de HTC Desire HD) | QSD8250 | No se puede reproducir el vídeo. Devuelve el error VIDEO_PERFIL_NOT_SUPPORTED. | Desire no proporciona un decodificador de hardware adecuado. Proporciona el decodificador SW de Stagefright. | Reinicie el dispositivo. |
| HTC EVO 4G | QSD8650 | Sin decodificador de hardware. | Qualcomm no tiene un decodificador de hardware. | Actualice a Android 4.x. |
| Kindle FireSystem versión 6.0 | OMAP4 TI | No reproduce flujos HLS. El vídeo en AIR no funciona. |  | Actualice a la versión 6.3 del sistema. |
| Kindle Fire HD | OMAP4 TI | Puede llegar a un estado en el que no pueda reproducir vídeo. Devuelve los errores VIDEO_PERFIL_NOT_SUPPORTED y UNRECOVERABLE_ERROR. | El decodificador de hardware se encuentra en un estado irrecuperable cuando la aplicación no cierra completamente el decodificador de hardware, por ejemplo, después de encontrarse con un bloqueo. También sucede en las aplicaciones nativas del dispositivo. | Reinicie el dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE se bloquea después de varios conmutadores ABR. |  |  |
| Motorola ASymmetrix | Tegra2 | Problemas generales de rendimiento con AVE en lugar de AIR. La reproducción de audio y vídeo no se sincroniza y se congela después de reproducirse entre 9 y 15 minutos. Bloqueos. | Posiblemente relacionado con openGLES que habilitamos en AIR. Se está investigando. |  |
| Nexo 7 (2.ª generación) | S4Pro APQ8064 (Qualcomm) | El dispositivo se bloquea cuando se pone en pausa una película durante más de 30 minutos. | Problema de dispositivo que se ha informado a Google. | La aplicación debe agotarse para no permitir un estado de pausa largo. |
| Nexus S (GB) | Pájaro zumbador | No se puede reproducir ningún vídeo con el decodificador de hardware. | No hay un decodificador HW basado en Stagefright en Nexus S, por lo que para Android 2.3 utilizamos un decodificador SW. | Actualice a ICS. |
| Nexo S (ICS) | Pájaro zumbador | El vídeo parpadea ocasionalmente. | Los datos incorrectos pueden hacer que el descodificador pase a un estado incorrecto. | Reinicie el dispositivo. |
| Nook tabletSistema operativo Android: 2,3 | OMAP TI 4 | El vídeo no se reproduce y la aplicación se bloquea. | Stagefright entra en un estado inestable después de ejecutar la aplicación varias veces. Llamadas a mediaplayer::QueryCodecs bloqueadas. | Reinicie el dispositivo para restablecer el estado. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | No se puede instalar la aplicación SampleMediaPlayer. | Utiliza ARM v6 en lugar del chipset ARM v7 más común. FP/AIR no admite este dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | No se puede reproducir el vídeo. | Este chipset es un decodificador desconocido para Android pre-ICS en AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | El rendimiento del vídeo no está a la altura de este dispositivo. | El decodificador de hardware devuelve fotogramas descodificados con el PTS incorrecto. Parece que el decodificador utiliza tiempo de descodificación en lugar de tiempo de presentación. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | OMAP4 TI | Se bloquea al iniciar el vídeo. |  | Actualice a Android 2.3.7 o 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | De forma intermitente, el vídeo se congela y solo se reproduce el audio y, a continuación, deja de responder. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | El vídeo se congela. | Investigando. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | La transición MBR puede tardar hasta tres segundos. | Como solución para los bloqueos MBR, reiniciamos el decodificador para cada conmutador de flujo, que puede tardar hasta tres segundos. |  |
| Samsung Galaxy Y |  | No se puede instalar la aplicación SampleMediaPlayer. | Utiliza ARM v6 en lugar del chipset ARM v7 más común. FP/AIR no admite este dispositivo. |  |
| Xoom | Tegra | Se eliminan algunos fotogramas para cambiar. El decodificador no se reinicia. | Límite OMXAL. |  |

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
