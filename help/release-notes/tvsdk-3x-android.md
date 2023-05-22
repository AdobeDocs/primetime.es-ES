---
title: Notas de la versión de TVSDK 3.15 para Android
description: Las notas de la versión de TVSDK 3.15 para Android describen las novedades o los cambios, los problemas resueltos y conocidos, y los problemas de los dispositivos en TVSDK para Android 3.15
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: cd2c64ef-dd42-4dc2-805f-eeb64a8a53d9
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Notas de la versión de TVSDK 3.15 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 3.15 para Android describen las novedades o los cambios, los problemas resueltos y conocidos, y los problemas de los dispositivos en TVSDK y Android 3.15.

El reproductor de referencia de Android se incluye con el TVSDK de Android en el directorio samples/ de su distribución. El archivo README.md que lo acompaña explica cómo crear el reproductor de referencia.

>[!NOTE]
>
>Para crear correctamente el reproductor de referencia, tal como se describe en el archivo README.md distribuido con la versión, asegúrese de hacer lo siguiente:
>
>1. Descargar VideoHeartbeat.jar desde [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (Biblioteca de VideoHeartbeat para Android v2.0.0)
>1. Extraiga VideoHeartbeat.jar en la carpeta libs/.


TVSDK para Android proporciona muchas mejoras de rendimiento con respecto a versiones anteriores. Proporciona una experiencia de visualización de alta calidad y lleva todas las funciones de la versión 1.4, con la excepción de la compatibilidad con Multi-CDN.

El conjunto completo de funciones admitidas y no admitidas se presenta en la [Matriz de características](#feature-matrix) de las notas de la versión.

## Android TVSDK 3.15

Esta versión corrige el problema en el que la aplicación se bloquea varias veces cuando falta la etiqueta creative o cuando [!UICONTROL url CDATA] está vacío en [!UICONTROL VAST] respuesta.

Para obtener más información sobre las correcciones de errores en esta versión y en las anteriores, consulte [problemas corregidos en TVSDK para Android](#resolved-issueszd).

### Nuevas funciones y mejoras en las versiones anteriores

**Android TVSDK 3.14**

Esta versión corrige el problema en el que la aplicación se bloquea cuando [!UICONTROL CDATA] el nodo está vacío para cualquiera de los [!UICONTROL ClickTracking], [!UICONTROL CustomClick] o [!UICONTROL CompanionClickTracking] elementos en la respuesta VAST.

**Android TVSDK 3.13**

El flujo DRM de Widevine se congela o muestra marcos negros en el interruptor ABR en los dispositivos FireTV, que incluyen dispositivos Fire TV de 3ª generación y Fire TV Cube de 1ª y 2ª generación.

Para resolver el problema, establezca la API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` para los dispositivos Fire TV especificados antes de iniciar la reproducción. El valor predeterminado es false.

**Android TVSDK 3.12**

Versión de gradle de la aplicación de referencia de Primetime actualizada a la versión 5.6.4.

Para configurar y ejecutar la aplicación de referencia mediante Android Studio, siga las instrucciones del archivo Léame disponible con el zip de TVSDK en `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

Los principales problemas de los clientes corregidos en la versión actual se mencionan en [problemas resueltos](#resolved-issues) sección.

**Android TVSDK 3.11**

* **Se permite la captura de cajas con encabezado específico del sistema de protección (PSSH)** : TVSDK permite recuperar el cuadro de encabezado específico del sistema de protección asociado al recurso de medios cargado actualmente. Nueva API `getPSSH()` añadido a `com.adobe.mediacore.drm.DRMManager`.

Para obtener más información, consulte [DRM de Widevine](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

La versión se centró en solucionar los principales problemas de los clientes, tal como se menciona en [problemas resueltos](#resolved-issues) sección.

**Android TVSDK 3.9**

* **Envío seguro a través de HTTPS** - Android TVSDK 3.9 introdujo las funciones de entrega segura a través de HTTPS para ofrecer contenido de forma segura con una escala y un rendimiento sin precedentes.

   Para habilitar la entrega segura a través de HTTPS, se ha introducido una nueva API en `NetworkConfiguration` clase.

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Compatibilidad previa a la emisión con la función de desglose parcial de anuncios** : Con esta mejora, TVSDK 3.8 admite anuncios previos a la emisión con la función de desglose parcial de anuncios (PABI).

El anuncio previo a la emisión, si está disponible, se reproduce y, a continuación, el contenido se reproduce desde el punto en directo emulando la experiencia de la televisión en directo.

**Android TVSDK 3.7**

* Para el contenido de prueba de Widevine, una nueva API `setMediaDrmCallback` en la clase DRManager se expone para anular la implementación predeterminada de la interfaz MediaDrmCallback.

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* Se ha corregido el error AppCrash por no gestionar `MediaPlayerEvent.ITEM_UPDATED` en la capa C++ (Android de 64 bits).

**Android TVSDK 3.6**

* **Mejore sus aplicaciones para el requisito de 64 bits** - La biblioteca nativa `(libAVEAndroid.so)` ahora se actualiza y está disponible en dos versiones. La ubicación de la biblioteca nativa de armeabi (32 bits) existente se ha cambiado de `/framework/Player to /framework/Player/armeabi` y se introduce una biblioteca arm64-v8a (64 bits) adicional en `/framework/Player/arm64-v8a.`

**Versión 3.5**

* **Justo A Tiempo Y Resolución De Anuncios** - TVSDK 3.5 elimina la compatibilidad con los anuncios reproducidos de la cronología.

* **Compatibilidad habilitada para la reproducción sin conexión** - Con la reproducción sin conexión, los usuarios ahora pueden descargar contenido de vídeo en sus dispositivos y verlo cuando no están conectados. Para obtener información detallada, consulte &quot;[Reproducción sin conexión con Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).&quot;

**Versión 3.4**

* TVSDK ahora es compatible con la reproducción de flujos CMAF para flujos CBC cifrados y simples.

**Versión 3.3**

* **Cambios de API**

   * Se agrega una nueva API a `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` para gestionar errores y tiempos de espera de red.
      * donde (n) es el número de reintentos.

**Versión 3.2**

* **Compatibilidad con resolución de anuncios paralelos y descarga de manifiestos**

   * TVSDK 3.2 admite la resolución simultánea, en lugar de la resolución secuencial para todas las solicitudes de publicidad y las pausas publicitarias, excepto VMAP.

   * Todos los manifiestos de anuncio de una pausa publicitaria se descargan simultáneamente.

* **Se habilitó la compatibilidad con la resolución de anuncios y el tiempo de espera de descarga de manifiesto.**

   * Los usuarios ahora pueden establecer el valor de tiempo de espera para la resolución general de anuncios y las descargas de manifiestos.  En el caso de VMAP, el valor de tiempo de espera se aplica a las pausas publicitarias individuales, ya que todas las pausas publicitarias se resuelven secuencialmente.

* **Se han introducido nuevas API en la clase Advertising Metadata:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **Se han eliminado las siguientes API de la clase AdvertisingMetadata:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **Reproducción de emisiones con codec de audio AC3/EAC3**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` in `MediaPlayer` clase

* **TVSDK admite CMAF y reproducción de flujos simples para Widevine CTR cifrado.**

* **Ahora se admite la reproducción de flujos HEVC de 4K.**

* **Solicitudes de llamada de anuncio paralelas** : TVSDK ahora recupera previamente 20 solicitudes de llamada de anuncio en paralelo.

**Versión 3.0**

* **TVSDK 3.0 es compatible con flujos de codificación de vídeo de alta eficiencia (HEVC).**

* **Just in Time: resolución de anuncios más cerca de los marcadores de publicidad**
La resolución diferida de anuncios ahora resuelve cada pausa publicitaria de forma independiente. Anteriormente, la resolución de la publicidad se realizaba en dos fases: las ediciones previas a la emisión se resolvían antes del inicio de la reproducción y todas las ranuras intermedias/posteriores a la emisión se combinaban después de iniciarse la reproducción. Con esta función mejorada, cada pausa publicitaria ahora se resuelve en un momento específico antes del punto de referencia de anuncio.

>[!NOTE]
>
>La resolución de anuncios diferidos ahora se ha cambiado a desactivada de forma predeterminada y debe habilitarse explícitamente.

Se agrega una nueva API a `AdvertisingMetadata::setDelayAdLoadingTolerance` para obtener la tolerancia de carga de publicidad retrasada asociada a estos metadatos de publicidad.\
Ahora se permite la búsqueda inmediatamente después de la PREPARACIÓN, la búsqueda de más y las pausas resultarán en una resolución inmediata antes de la finalización de la búsqueda.\
Modos de señalización `SERVER_MAP` y `MANIFEST_CUES` son compatibles.

Para obtener más información, consulte [Guía del programador de TVSDK 3.0 para Android](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) sobre la API y los cambios de eventos.

* **Actualizado `targetSdkVersion` a la última versión**

Actualizado `targetSdkVersion` de 19 a 27 para un buen funcionamiento.

* **Placement.Type getPlacementType() es ahora un método en la interfaz TimelineMarker**

   Este método devolverá un tipo de posición de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Si no se resuelve una pausa publicitaria, el método getDuration() de la interfaz TimelineMarker devolverá 0.

**Versión 2.5.6.**

* **TVSDK 2.5 es compatible con Android P.**

* **Habilitar audio de fondo**

   Para habilitar la reproducción de audio cuando la aplicación se mueve de primer plano a segundo plano, la aplicación debe llamar a `enableAudioPlaybackInBackground` API de MediaPlayer con true como argumento cuando el reproductor está en estado PREPARED.

* **alwaysUseAudioOutputLatency(valor booleano) en la clase MediaPlayer**

Cuando esté configurado, utilice la latencia de salida en el cálculo de la marca de tiempo del audio.
Los parámetros booleanos val - True utilizarán la latencia de salida de audio en el cálculo de la marca de tiempo de audio.

* **Optimizado para obtener la mejor experiencia de reproducción incluso si la velocidad del ancho de banda disminuye de repente**

TVSDK ahora cancela la descarga del segmento en curso, si es necesario, y cambia dinámicamente a la representación adecuada. Esto se realiza cambiando sin problemas entre las velocidades de bits sin interrupciones.

**Versión 2.5.5**

* **Inserción parcial de desglose de anuncios**

   Experiencia similar a la de una TV de unirse en medio de un anuncio sin activar el seguimiento del anuncio parcialmente visto.\
   Ejemplo: Las uniones de usuarios se producen en medio (a los 40 segundos) de una pausa publicitaria de 90 segundos y consisten en tres anuncios de 30 segundos. Son 10 segundos del segundo anuncio de la pausa.

   * El segundo anuncio se reproduce durante el tiempo restante (20 segundos) seguido del tercer anuncio.

   * Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Los rastreadores solo del tercer anuncio se activan.

* **Carga segura de publicidad a través de HTTPS**

   Adobe Primetime proporciona una opción para solicitar la primera llamada al servidor de publicidad de primetime y a CRS a través de https.

* **Se ha agregado un ID de sistema de anuncios y creativo a las solicitudes CRS**

   Ahora se incluye `AdSystem` y `CreativeId` como nuevos parámetros en las solicitudes 1401 y 1403.

* **API setEncodeUrlForTracking en la clase NetworkConfiguration eliminada** ya que los caracteres no seguros de una dirección URL deben codificarse.

**Versión 2.5.4**

Android TVSDK v2.5.4 ofrece las siguientes actualizaciones y cambios en la API:

* Cambios en el valor predeterminado para `WebViewDebbuging`

   `WebViewDebbuging` el valor se establece en `Fals`e de forma predeterminada. Para habilitarlo, llame a `setWebContentsDebuggingEnabled(true)` en la aplicación.

* **Actualización de la versión de OpenSSL y Curl**

   Se ha actualizado libcurl a la versión 7.57.0 y OpenSSL a la versión 1.0.2k.

* Acceso de nivel de aplicación para el objeto de respuesta VAST

   Se ha introducido una nueva API `NetworkAdInfo::getVastXml()` que proporciona acceso al objeto de respuesta VAST a la aplicación.

**Versión 2.5.3**

Android TVSDK v2.5.3 ofrece las siguientes actualizaciones y cambios en la API.

* Se recomienda a todos los clientes de TVSDK que utilicen CRS que actualicen sus aplicaciones con TVSDK 2.5.3.85 o la versión más reciente en Android. Esto sustituirá a la implementación de la aplicación existente. Después de la actualización de TVSDK, compruebe las solicitudes de URL creativas de CRS en una herramienta proxy (por ejemplo: Charles) y confirme que el nombre de host y la versión en la ruta se reflejan como en la estructura de URL de ejemplo a continuación.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente de usuario de TVSDK personalizable: hemos agregado algunas API nuevas para personalizar los agentes de usuario.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Compartir cookies entre la aplicación de Android y TVSDK: Android TVSDK ahora admite el acceso de cookies entre la capa JAVA (almacenada en CookieStore de la aplicación Android) y la capa TVSDK de C++. Ahora, es posible establecer o modificar las cookies en la capa nativa de C++, ya que se expondrán al almacén de cookies de Java.

* Cambios de API:

   * Un nuevo evento `CookiesUpdatedEvent` se ha añadido. El reproductor de medios lo envía cuando se actualiza su cookie.

   * Se agrega una nueva API a `NetworkConfiguration::set/ getCustomUserAgent()` para utilizar el agente de usuario personalizado.

   * Se agrega una nueva API a `NetworkConfiguration::set/ getEncodedUrlForTracking` para forzar la codificación de caracteres no seguros.

   * Se agrega una nueva API a `NetworkConfiguration::getNetworkDownVerificationUrl()` para establecer una dirección URL de verificación de red en caso de conmutación por error.

   * Se agrega una nueva propiedad a `TextFormat::treatSpaceAsAlphaNum` que definen si se debe tratar el espacio como alfanumérico mientras se muestran los subtítulos.

* Cambios en `SizeAvailableEvent`. Anteriormente, `getHeight()` y `getWidth()` métodos de `SizeAvailableEvent` en la versión 2.5.2 se utilizaba para devolver la altura y la anchura de los fotogramas, lo que se devolvía mediante el formato multimedia. Ahora devuelve la altura de salida y la anchura de salida respectivamente devueltas por el decodificador.

* Cambios en el comportamiento del almacenamiento en búfer: El comportamiento del almacenamiento en búfer cambia. Depende del desarrollador de la aplicación lo que quiera hacer en caso de que el búfer esté vacío. 2.5.3 utiliza el tamaño del búfer de reproducción en una situación de vacío del búfer.

**Versión 2.5.2**

Android TVSDK v2.5.2 ofrece importantes correcciones de errores y algunos cambios en la API.

**Versión 2.5.1**

Las nuevas e importantes funciones incluidas en Android 2.5.1.

* **Mejoras de rendimiento -** La nueva arquitectura de TVSDK 2.5.1 ofrece una serie de mejoras de rendimiento. Basada en las estadísticas de un estudio de evaluación comparativa de terceros, la nueva arquitectura ofrece una reducción del 5 veces el tiempo de inicio y 3,8 veces menos fotogramas perdidos en comparación con la media del sector:

* **Instantáneo para VOD y en directo:** Cuando se activa el inicio instantáneo, el TVSDK inicializa y almacena en búfer el contenido antes de que comience la reproducción. Dado que puede iniciar varias instancias de MediaPlayerItemLoader simultáneamente en segundo plano, puede almacenar en búfer varias secuencias. Cuando un usuario cambia el canal y el flujo se ha almacenado en búfer correctamente, la reproducción en el nuevo canal se inicia inmediatamente. TVSDK 2.5.1 también es compatible con Instant On para **live** también transmite. Los flujos en directo se vuelven a almacenar en búfer cuando se mueve la ventana en directo.

* **Lógica ABR mejorada:** La nueva lógica ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúa y también optimiza el número de veces que el conmutador de velocidad de bits realmente se produce al monitorizar la velocidad a la que cambia la longitud del búfer.

* **Descarga parcial de segmentos/Subsegmentación -** TVSDK reduce aún más el tamaño de cada fragmento para iniciar la reproducción lo antes posible. El fragmento ts debe tener un fotograma clave cada dos segundos.

* **Resolución de anuncio diferida -** TVSDK no espera la resolución de anuncios que no son previos a la emisión antes de iniciar la reproducción, lo que reduce el tiempo de inicio. Las API como seek y trick-play siguen sin estar permitidas hasta que se resuelvan todos los anuncios. Esto es aplicable a los flujos de VOD utilizados con CSAI. No se permiten operaciones como buscar y avanzar rápidamente hasta que se complete la resolución del anuncio. Para emisiones en directo, esta función no se puede habilitar para la resolución de anuncios durante un evento en directo.

* **Conexiones de red persistentes:** Esta función permite a TVSDK crear y almacenar una lista interna de conexiones de red persistentes. Estas conexiones se reutilizan para varias solicitudes, en lugar de abrir una nueva conexión para cada solicitud de red y después destruirla. Esto aumenta la eficacia y disminuye la latencia en el código de red, lo que da como resultado un rendimiento de reproducción más rápido.
Cuando TVSDK abre una conexión, solicita al servidor una *keepalive* conexión. Es posible que algunos servidores no admitan este tipo de conexión, en cuyo caso TVSDK volverá a establecer una conexión para cada solicitud. Además, aunque las conexiones persistentes estarán activadas de forma predeterminada, TVSDK ahora tiene una opción de configuración para que las aplicaciones puedan desactivar las conexiones persistentes si lo desean.

* **Descarga paralela:** La descarga de vídeo y audio en paralelo en lugar de en serie reduce los retrasos de inicio. Esta función permite reproducir archivos HLS Live y VOD, optimiza el uso del ancho de banda disponible de un servidor, reduce la probabilidad de entrar en situaciones de fallo de búfer y minimiza el retraso entre la descarga y la reproducción.

* **Descargas de anuncios paralelos:** TVSDK recupera previamente los anuncios en paralelo a la reproducción del contenido antes de llegar a los saltos de publicidad, lo que permite una reproducción perfecta de los anuncios y el contenido.

* **Reproducción**

* **Reproducción de contenido MP4:** Los clips cortos MP4 no necesitan volver a transcodificarse para reproducirse en TVSDK.

   >[!NOTE]
   >
   >La reproducción de MP4 no admite la conmutación ABR, la reproducción con trucos, la inserción de anuncios, el enlace de audio tardío ni la subsegmentación.

* **Juego de trucos con velocidad de bits adaptable (ABR) -** Esta función permite a TVSDK cambiar entre flujos de iFrame en el modo de reproducción con trucos. Puede utilizar perfiles que no sean de iFrame para realizar trucos a velocidades más bajas.

* **Juego de truco más suave -** Estas mejoras mejoran la experiencia del usuario:

   * Selección de velocidad de bits adaptable y velocidad de fotogramas durante el truco, según el ancho de banda y el perfil del búfer

   * Utilice el flujo principal en lugar del flujo IDR para obtener una reproducción rápida de hasta 30 fps.

* **Protección de contenido**

   * **Protección de salida basada en resolución:** Esta función vincula las restricciones de reproducción a resoluciones específicas, proporcionando controles DRM de grano más preciso.

* **Compatibilidad con flujo de trabajo**

   * **Integración de facturación directa -** Esto envía métricas de facturación al backend de Adobe Analytics, que cuenta con la certificación de Adobe Primetime para los flujos que utiliza el cliente.

   TVSDK recopila automáticamente las métricas, cumpliendo con el contrato de ventas del cliente, para generar los informes de uso periódicos necesarios para la facturación. En cada evento de inicio de flujo, TVSDK utiliza la API de inserción de datos de Adobe Analytics para enviar métricas de facturación como tipo de contenido, indicadores habilitados de inserción de publicidad y indicadores habilitados para drm, en función de la duración del flujo facturable, al grupo de informes propiedad de Adobe Analytics Primetime. Esto no interfiere ni se incluye en los grupos de informes de Adobe Analytics del cliente ni en las llamadas al servidor. Si se solicita, este informe de uso de la facturación se envía periódicamente a los clientes. Esta es la primera fase de la función de facturación que solo admite la facturación de uso. Se puede configurar en función del contrato de venta utilizando las API descritas en la documentación. Esta función está habilitada de forma predeterminada. Para desactivar esta función, consulte la muestra del reproductor de referencia.

   * **Compatibilidad con failover mejorada:** Estrategias adicionales implementadas para continuar la reproducción ininterrumpida, a pesar de los errores de los servidores host, los archivos de lista de reproducción y los segmentos.


* **Publicidad**

   * **Integración de foso -** Compatibilidad con la medición de la visibilidad de anuncios de Moat.

   * **Banners de Companion -** Los banners de acompañamiento se muestran junto a un anuncio lineal y, a menudo, siguen apareciendo en la vista una vez finalizado el anuncio. Estos titulares pueden ser de tipo html (un fragmento de HTML) o de tipo iframe (una dirección URL de una página de iframe).

* **Analytics**

   * **VHL 2.0:** Se trata de la última integración de la biblioteca de latidos de vídeo (VHL) optimizada para la recopilación automática de datos de uso para Adobe Analytics. La complejidad de las API se ha reducido a para facilitar la implementación. Descargar la biblioteca VHL [Versión 2.0.0 para Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) y extraiga el archivo JAR en la carpeta libs.

* **SizeAvailableEventListener**

   * `getHeight()` y `getWidth()` métodos de `SizeAvailableEvent` ahora devolverá la salida en altura y anchura respectivamente. La proporción de aspecto de la pantalla se puede calcular de la siguiente manera:

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      La proporción de aspecto de almacenamiento en términos de anchura y altura de la estrella también se puede utilizar para calcular la anchura y la altura del cuadro:

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookies**

   * Android TVSDK ahora admite el acceso a las cookies JAVA almacenadas en el almacén de cookies de la aplicación Android. Se proporciona una API de devolución de llamada (onCookiesUpdated) para registrar cada vez que se introduce una nueva cookie como parte de **Establecer cookie** Encabezado de respuesta. Estas cookies están disponibles como una lista de cookies HTTP utilizadas para un URI/dominio diferente al establecer estos valores de cookies en ese URI/dominio en particular mediante CookieStore. Del mismo modo, los valores de las cookies en TVSDK se actualizan mediante la API de adición de CookieStore.

## Matriz de características {#feature-matrix}

TVSDK para Android admite una serie de funciones que puede implementar para agregar funcionalidad a las aplicaciones de vídeo.

En las tablas de funciones que aparecen a continuación, una &quot;Y&quot; indica que la función es compatible con la versión actual.

| Función | Tipo de contenido | HLS |
|---|---|---|
| Reproducción general (reproducir, pausar, buscar) | VOD + Activo | Y |
| FER: reproducción general (reproducción, pausa, búsqueda) | VOD FER | Y |
| Buscar cuando se esté reproduciendo un anuncio | VOD + Activo | No compatible |
| Reproducción de HEVC | VOD + Activo | Solo contenedor de fMP4 |
| AC3 y EAC3 | VOD + Activo | No compatible |
| MP3 | VOD | No compatible |
| Reproducción de contenido MP4 | VOD | Y |
| Lógica de conmutación de velocidad de bits adaptable | VOD + Activo | Y |
| Reproducción solo de audio | VOD + Activo | Y |
| Compatibilidad con varias CDN | VOD + Activo | No compatible |
| Reproducción de anuncios con medios solo de audio | VOD + Activo | No compatible |
| Subtítulos opcionales - 608/708 | VOD + Activo | Y |
| Subtítulos - WebVTT | VOD + Activo | Y |
| Conmutación por error de manifiesto | VOD + Activo | Y |
| Conmutación por error avanzada | VOD + Activo | Y |
| QoS y notificaciones del reproductor | VOD + Activo | Y |
| Compatibilidad con encabezados de cookie | VOD + Activo | Y |
| Compatibilidad con encabezados HTTP personalizados | VOD + Activo | Y (se requiere listado de permitidos) |
| Establecer parámetros de control de búfer | VOD + Activo | Y |
| Establecer controles de velocidad de bits adaptables | VOD + Activo | Y |
| Etiquetas de manifiesto personalizadas | VOD + Activo | Y |
| Enlace de audio tardío | VOD + Activo | Y |
| Redirección 302 | VOD + Activo | Y |
| Reproducción con desplazamiento | VOD + Activo | Y |
| Juego de trucos | VOD + Activo | Y |
| Cámara lenta en el juego de trucos | VOD + Activo | No compatible |
| Juego de trucos suave (con ABR) | VOD + Activo | Y |
| Análisis de ID3 | VOD + Activo | Y |
| Interrupción de anuncios | VOD + Activo | No compatible |
| Instant On | VOD + Activo | No compatible |
| Compatibilidad con marcadores de discontinuidad | VOD + Activo | Y |
| Adherencia de redirección 302 | VOD + Activo | Y |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Reproducción general, anuncios habilitados | VOD + Activo | Y |
| Contenido de FER con anuncios habilitados | VOD | Y |
| Comportamientos de publicidad predeterminados | VOD + Activo | Y |
| VAST 2.0/3.0 | VOD + Activo | Y |
| VMAP 1.0 | VOD + Activo | Y |
| Anuncios MP4 | VOD + Activo | Y (desde CRS) |
| Trick Play con anuncios habilitados | VOD + Activo | Y |
| Solo anuncio | VOD | Y |
| Parámetros de segmentación | VOD + Activo | Y |
| Parámetros personalizados | VOD + Activo | Y |
| Comportamientos de publicidad personalizados | VOD + Activo | Y |
| Etiquetas de publicidad personalizadas | Activo | Y |
| Resoluciones de anuncios personalizadas | VOD + Activo | Y |
| Freewheel Custom Ad Resolver | VOD | Y |
| C3 | VOD + Activo | No compatible |
| Resolución de publicidad diferida | VOD | Y |
| Compatibilidad con marcadores de discontinuidad - SSAI | VOD + Activo | Y |
| Anuncios complementarios, anuncios de banner y anuncios en los que se puede hacer clic | VOD + Activo | Y |
| VPAID 2.0 | VOD + Activo | Y (JS) |
| Salida anticipada del anuncio | Activo | Y |
| Priorización creativa basada en reglas | VOD + Activo | Y |
| Reglas CRS | VOD + Activo | Y |
| JSON Ad Resolver | VOD + Activo | No compatible |
| Integración de foso | VOD + Activo | Y |
| Inserción de pausa publicitaria parcial | Activo | Y |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Cifrado AES | VOD + Activo | Y |
| Ejemplo de cifrado AES | VOD + Activo | Y |
| Flujos Tokenizados | VOD + Activo | Y |
| DRM de Widevine | VOD + Activo | Solo contenedor de fMP4 |
| DRM de Primetime | VOD + Activo | Y |
| Reproducción externa (RBOP) | VOD + Activo | Solo DRM de Primetime |
| Rotación de licencia | VOD + Activo | Solo DRM de Primetime |
| Rotación de clave | VOD + Activo | Solo DRM de Primetime |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Integración de VHL de Adobe Analytics | VOD + Activo | Y |
| Factura | VOD + Activo | Y |

## Problemas resueltos {#resolved-issues}

Cuando la resolución está asociada con un problema del que se ha informado, se muestra una referencia de Zendesk, por ejemplo ZD#xxxxx.

**Android TVSDK 3.15**

Esta sección proporciona un resumen del problema resuelto en la versión TVSDK 3.14 para Android.

* ZD#46903: la aplicación se bloquea varias veces cuando falta la etiqueta creative o cuando [!UICONTROL url CDATA] está vacío en [!UICONTROL VAST] respuesta.

**Android TVSDK 3.14**

* ZD#46903: la aplicación se bloquea cuando [!UICONTROL CDATA] el nodo está vacío para cualquiera de los [!UICONTROL ClickTracking], [!UICONTROL CustomClick] o [!UICONTROL CompanionClickTracking] elemento en [!UICONTROL VAST] respuesta.

### Problemas resueltos en las versiones anteriores

**Android TVSDK 3.12**

* ZD#40584: La aplicación de referencia de Primetime no se crea con la última versión de gradle.

**Android TVSDK 3.11**

* ZD#41252: Los caracteres coreanos en WebVTT se han roto después de Android 7.1.

**Android TVSDK 3.10**

* ZD#40340: La aplicación se bloquea con el error &quot;La aplicación no responde&quot; al intentar la reproducción después de que se hayan bloqueado todos los archivos TS (TypeScript).

**Android TVSDK 3.8**

* No se han agregado nuevos problemas.

**Android TVSDK 3.7**

* No se han agregado nuevos problemas.

**Android TVSDK 3.6**

* No se han agregado nuevos problemas.

**Versión 3.5**

* ZD#37503: las respuestas JSON para las reglas CRS se almacenan en caché para evitar solicitudes duplicadas.

**Versión 3.4**

* ZD#37996: se ha corregido un problema de reproducción entrecortada en los flujos HEVC lineales y de VOD CMAF.
* ZD#37706: se ha corregido un problema relativo a los subtítulos ilegibles.
* ZD#37622: se ha corregido un problema sobre URISyntaxErrors fatal para anuncios específicos.
* ZD#36938: se ha corregido un problema por el que la velocidad de bits descendía hasta la velocidad media y, después, aumentaba hasta la velocidad más alta tras salir de las reproducciones con trucos.

**Versión 3.3**

* ZD#37394: el avance rápido de recursos CMAF causa artefactos después de los cambios de velocidad.
   * Se ha corregido un problema que se producía con un cambio de perfil durante la reproducción con trucos.
* ZD#37396: Faltan eventos de seguimiento de anuncios para algunas mid-rolls y post-rolls.
   * Se ha corregido un caso específico relacionado con los eventos de seguimiento de anuncios.
* ZD#37491: el código de estado HTTP con meta de error no está presente.
   * Se ha trabajado en propagar errores de red más arriba en la pila.
* ZD#37808 - Lista de permitidos Nuevo encabezado personalizado.
   * Se ha agregado compatibilidad con SAI_TAG como parte de esta corrección.
* ZD#37622: Errores de sintaxis de URI de pods de publicidad específicos.
   * Se ha corregido un problema con el bloqueo de reproducción de flujo cuando la aplicación del cliente de Android recibe anuncios que contienen un % sin codificar
* ZD#37631: mecanismo de reintento del manifiesto maestro para Android TVSDK.
   * Se ha añadido una nueva API en la configuración de red para gestionar esta mejora. Si no se utiliza esta API, no se vuelve a intentar el manifiesto. Si se utiliza, se volverá a intentar el manifiesto para controlar los errores y tiempos de espera de la red.

**Versión 3.2**

* ZD#37493: Las señalizaciones de seguimiento para la reproducción en directo no se activan de forma intermitente para el primer anuncio de la secuencia.
* ZD#36985: Las señalizaciones de seguimiento no se envían para pausas de anuncios vacías en la respuesta de VMAP.
* ZD#37134: TVSDK emite el ID incorrecto para la respuesta de VMAP de forma intermitente.

**Versión 3.0**

* ZD#33740: TVSDK emite una advertencia innecesaria justo después de crear un objeto MediaPlayer y llamar a replaceCurrentResource()

   * Se ha mejorado la corrección anterior llamando a la restauración solo cuando el reproductor está en estado suspendido

* ZD#36442: Cada nueva reproducción desconecta la sesión de depuración remota, lo que hace imposible la depuración.

   * La depuración no es posible de forma predeterminada en la vista web, ya que la depuración no está habilitada de forma predeterminada. La aplicación debe habilitar la depuración si es necesario llamando a setWebContentsDebuggingEnabled(true) en el objeto devuelto desde MediaPlayer.getCustomAdView().

* ZD#33688: Compatibilidad con la resolución de anuncios Just In Time

   * Las pausas publicitarias se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.

* ZD#36441: La duración de la ventana en directo sigue aumentando más allá de los 5 minutos, lo que provoca varios problemas.

   * Se ha corregido un problema por el cual virtualStartTime se agregaba dos veces al calcular el punto de vida virtual, lo que provocaba este problema.

**Android TVSDK 2.5.6**

* ZD #34992: el idioma está vacío en los subtítulos.

   * Se ha corregido un caso en el que TVSDK no analizaba #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS del manifiesto principal para obtener los detalles de seguimiento del pie de ilustración.

* #35078 ZD: validación de IP de Android.

   * TVSDK 2.5.6 se ha validado con las últimas versiones beta de Android P. No se han encontrado problemas debido al nuevo sistema operativo Android.

* ZD #34149: el reproductor sigue solicitando manifiestos aunque se encuentren errores.

   * Se ha corregido el caso en el que TVSDK hacía llamadas repetitivas incluso cuando todos los perfiles estaban inactivos (error 404).

* ZD #31533: Reproducción de audio en Android después de que la aplicación se envíe a segundo plano.

   * Añadido `enableAudioPlaybackInBackground` API de MediaPlayer a la que se debe llamar con &quot;True&quot; como argumento (cuando el reproductor está en estado PREPARED) para habilitar la reproducción de audio cuando la aplicación está en segundo plano.

**Android TVSDK 2.5.5**

* ZD #21647: Android TVSDK notifica 640 x 368 cuando el tamaño real del vídeo es de 640 x 360.

   * Debido a que la variable m_nOutputHeight (dentro de AndroidMCVideoDecoder) se actualiza con la altura del fotograma en lugar de la altura de salida real. Se han realizado cambios relevantes en la función getVideoFrame para calcular m_nOutputHeight correctamente.

* ZD #26614 - Urgente — Servicio de anuncios de terceros / programático — incapacidad para entregar impresiones.

   * Se ha mejorado la corrección anterior al administrar el caso en el análisis XML, donde el problema se podía reproducir cuando &quot;espacio&quot; está antes del signo &quot;igual&quot; como &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android: Añadir AdSystem y el ID creativo a las solicitudes de CRS.

   * Ahora se incluyen &quot;AdSystem&quot; y &quot;CreativeId&quot; como nuevos parámetros en las solicitudes 1401 y 1403.

* ZD #33062: TVSDK se bloquea al producirse el carácter de barra vertical en la respuesta VAST en el nodo CDATA

   * La API setEncodeUrlForTracking de la clase NetworkConfiguration se ha eliminado como caracteres no seguros de una dirección URL que se va a codificar

* #33063 de ZD: la lógica de selección de archivos CRS se ha dañado. TVSDK no enviaba una solicitud CRS para el formato webm, sino que la enviaba para archivos 3gpp.

   * Se ha corregido la lógica. Al utilizar archivos multimedia con formato webm y 3gpp, CRS solicita que se envíe para webm. Y al usar ambos archivos multimedia con formato 3gpp, la solicitud CRS que se enviará para el archivo 3gpp de mayor velocidad de bits.

* ZD #33125: La aplicación de Android se bloquea con una etiqueta DoubleClick específica dentro de VMAP.

   * Se ha corregido el escenario para evitar el bloqueo.

* ZD #32256 - Problema de rotación de licencias y rotación de claves - Acceso al Adobe

   * Se ha corregido la inicialización de segmentos con los metadatos DRM para el contenido SampleAES. Funciona bien con contenido AES128.

* ZD #33619: reenvío rápido de una lista de reproducción en crecimiento con contenido atascado en estado de almacenamiento en búfer cerca de un punto en directo.

   * Se ha gestionado el caso al cruzar el punto en directo en el modo de truco

* ZD #34151: los objetos TimedMetadata están desordenados.

   * Dos eventos TimedMetadata aparecían en orden aleatorio si pertenecían a la misma hora en la cronología. Mantuvieron su orden original en manifiesto.

* ZD #34189: problema al intentar iniciar la pausa publicitaria.

   * El problema era con los anuncios de SSAI que se vinculan mediante la discontinuidad. Y la causa fue un comportamiento cuando buscamos el comienzo de tales anuncios, buscamos un fotograma clave y no lo encontramos. El motivo era que la marca de tiempo de audio principal del anuncio era anterior a la marca de tiempo de vídeo principal. Por lo tanto, terminamos buscando un marco clave en un fragmento incorrecto de datos de volcado. Solucionado ahora.

* ZD #34528: la resolución de vídeo no se actualiza más allá de 640x360 en la llave FireTV de 3ª generación.

   * Se ha mejorado la corrección para incluir las últimas actualizaciones de firmware

* ZD #34793: TVSDK 2.5.x se bloqueaba con el solucionador de contenido personalizado en algunos casos en los que VideoEngine suponía que auditudeSettings está disponible y no lo estaba.

   * El bloqueo se producía debido a una llamada de función en un puntero compartido nulo (auditudeSettings). Se ha añadido una comprobación condicional dentro de VideoEngineTimeline::placeToSourceTimeline() para asegurarse de que auditudeSettings esté disponible antes de llamar a cualquier elemento de ese objeto.

* ZD #32584: no se puede acceder a la información completa presente en el &lt;extensions> nodo de una respuesta VAST.

   * Se ha corregido el problema relacionado con el análisis de XML y ahora NetworkAdInfo proporciona la información completa presente en el &lt;extensions> nodo

* ZD #35086: no se obtienen datos de extensión completos del reproductor en caso de respuestas de VMAP específicas.

   * El problema era específico del xml de extensión, ya que el análisis de XML no funcionaba si el xml de extensión tenía comillas dobles dentro del valor de atributo. Se ha corregido el problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659: sesión de reproducción que permite la depuración remota de la vista web.

WebViewDebuging se establece en False de forma predeterminada. Para habilitar la depuración, establezca como true mediante la aplicación, utilizando setWebContentsDebuggingEnabled(true).

* ZenDesk#33011: la cronología del anuncio no se resuelve en caso de que falle una solicitud de CRS.

   Cuando falla una solicitud de CRS a un anuncio, la cronología se resuelve y se reproducen los anuncios restantes.

* ZenDesk#34528 - La resolución de video no se actualiza más allá de 640x360 en el dongle de tercera generación FireTV.

   La resolución de vídeo cambia según la velocidad de bits.

* ZenDesk#33192: AudioTrack tiene un nombre nulo cuando el seguimiento se recupera mediante AudioUpdatedEventListener::onAudioUpdated.

   En algunos escenarios en FireTV Stick, el evento onAudioUpdate se activaba cuando no había ninguna actualización de audio real. Esto se ha solucionado.

**Android TVSDK 2.5.3**

* Zendesk#32216 - La suscripción a la etiqueta personalizada TimedMetadata no funciona.

   Se devuelven datos de ID3 como una matriz de bytes (para admitir datos APIC o genéricos) al cliente, mientras que en 1.4 se devuelve una cadena. La matriz de bytes no gestiona el propio carácter terminado nulo, por lo que mostraba un carácter especial al cliente. Este problema se ha corregido.
* Zendesk#32670 - Reproductor que no falla a la lista de reproducción redundante

   Esto funciona bien ahora y setNetworkDownVerificationUrl funciona según lo esperado.
* Zendesk#32369 - Subtítulos ocultos muestran diferentes colores de basura o artefactos.

   El problema con los problemas de CC se ha corregido en la última compilación
* Zendesk#25590 - Mejora: Almacén de cookies de TVSDK ( C++ a JAVA )

   Android TVSDK ahora admite el acceso de cookies entre la capa JAVA (almacenada en CookieStore de la aplicación Android) y la capa TVSDK de C++.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 no parece tener la solución para PTPLAY-20269

   Este problema se ha corregido e integrado en la rama 2.5.2.
* Zendesk#31806 - Palos de audiencia en PREPARACIÓN

   El reproductor se quedó atascado en el estado Preparación porque el xml de respuesta tenía una etiqueta vacía. Ahora el problema está solucionado.
* Zendesk#31727 - TVSDK 2.5: los caracteres de subtítulos se sueltan o se escriben incorrectamente.

   El problema se ha corregido y no se ha omitido ningún carácter.
* Zendesk#31485 - DrmManager en 2.5

   Se ha producido un error al crear DrmManager mediante el nuevo DrmManager (contexto de contexto). Se ha implementado la clase DRMService que proporcionaría DRMSanager.
* Zendesk#32794- Flujo de resolución 1080P que no se reproduce en Android

   Hemos cambiado SizeAvailableEvent y, anteriormente, los métodos getHeight() y getWidth() de SizeAvailableEvent en 2.5 se utilizaban para devolver la altura del marco y la anchura del marco, que devolvía el formato multimedia. Ahora devuelve la altura de salida y la anchura de salida respectivamente devueltas por el decodificador.
* El Flash Player de #19359 de Zendesk se bloquea debido a la posición #EXT-X-FAXS-CM atributo en el manifiesto de nivel de conjunto.

   La etiqueta #EXT-X-FAXS-CM siempre debe aparecer en la lista de reproducción superior antes de que la velocidad de bits o los segmentos individuales aparezcan en la lista de reproducción.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artefactos en subtítulos cerrados con fondo no opaco.

   La propiedad setTreatSpaceAsAlphaNum de TextFormat está expuesta. De forma predeterminada, el valor de la propiedad es False. Establezca la propiedad como True en un cliente para resolver el problema del espacio en blanco.

* La pantalla de Zendesk#25097 CC tiene artefactos visuales con la configuración de CC.

   La propiedad setTreatSpaceAsAlphaNum de TextFormat está expuesta. De forma predeterminada, el valor de la propiedad es False. Establezca la propiedad como True en un cliente para resolver el problema del espacio en blanco.

* La cadena del agente de usuario de Zendesk #31620 que sale del reproductor TVSDK está truncada.

   La cadena del agente de usuario ya no se truncará después de 128 caracteres.

   La cadena de versión de Adobe Primetime se agrega al agente de usuario del sistema.

* El evento SEEK_END que falta #30809 de Zendesk impide que la aplicación pase a un estado de reproducción.
* El color &#39;cian&#39; de Zendesk #30415 Closed Caption es ahora un tono más oscuro de azul (turquesa), en comparación con las versiones anteriores de TVSDK de Primetime.

   El color cambia de CianOscuro a Cian.

* Los anuncios de Zendesk #30727 VOD no se descargan o resuelven.

   En VMAP XML si hay una etiqueta VAST vacía sin una etiqueta de cierre explícita (‘&lt;/vast>&#39;) y sin un carácter de nueva línea después, el XML de VMAP no se analiza correctamente y es posible que no se reproduzcan anuncios.

**Android TVSDK 2.5.1**

* Se bloquea el dispositivo específico (Samsung Galaxy Tab 4); VOD DRM LBA con Auditude y hace clic en los anuncios.
* VHL: se envían llamadas de latido incorrectas al iniciar contenido desde un desplazamiento.
* Cuando se reproducen anuncios VPAID, Heartbeat de VHL llama a un evento:type:falta el anuncio de reproducción.
* Después de pasar al estado COMPLETO, el reproductor vuelve al estado REPRODUCIENDO con SKIP adBreakPolicy para los anuncios posteriores a la emisión.
* Las cookies no se adjuntan a las llamadas de retorno de anuncios salientes.
* Los puntos de referencia de anuncios no son visibles.
* HLS con pista SAP EAC3 separada no se carga.
* El Reproductor se bloquea cuando TVSDK recibe una calidad de pantalla activada después de restaurar el Reproductor multimedia.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

**Android TVSDK 3.11**

* No se han añadido nuevas limitaciones.

### Problemas y limitaciones conocidos en las versiones anteriores

**Android TVSDK 3.10**

* No se han añadido nuevas limitaciones.

**Android TVSDK 3.8**

* No se han añadido nuevas limitaciones.

**Android TVSDK 3.7**

* No se han añadido nuevas limitaciones.

**Android TVSDK 3.6**

* No se han añadido nuevas limitaciones.

**Android TVSDK 3.5**

* No se ha añadido ninguna nueva limitación.

**Android TVSDK 3.4**

* ID3, Subtítulos, Compatibilidad con audio de enlace tardío no se ha verificado para el flujo CMAF (CBC).
* En algunos dispositivos, existe un problema de baja reproducibilidad debido al cual la distorsión de vídeo puede aparecer en la parte superior durante el juego de trucos en flujos CMAF.

**Android TVSDK 3.3**

* Los subtítulos clcp:c608 no son compatibles con la reproducción de flujo CMAF.

**Android TVSDK 3.2**

* TVSDK 3.2 no admite la reproducción de secuencias AES y AES128 de muestra de CMAF.
* Los flujos HEVC CMAF no incluyen soporte para la reproducción de subtítulos.
* La coloración verde aparece para las secuencias cifradas con WV cuando la búsqueda se realiza alrededor del segmento no cifrado.
* Los flujos CMAF no admiten eventos ID3.
* Las secuencias HLS no admiten el formato de subtítulos HTML.

**Android TVSDK 3.0**

* La compatibilidad con HEVC tiene las siguientes limitaciones en esta versión

   * DRM no compatible
   * Compatibilidad con CC (CEA 608/708) no verificada
   * Aún no hay compatibilidad con 4K
   * Compatibilidad con etiquetas ID3 no verificada

* Para los eventos de progreso de publicidad, es posible que la barra de cronología no refleje el tiempo de reproducción de publicidad con una precisión del 100 %. Como solución alternativa, puede utilizar `adcompleteevent` para conocer la IU de finalización y actualización de la reproducción del anuncio para varios fines, como actualizar la barra de cronología, eliminar la IU relacionada con el anuncio, etc.
* Las llamadas publicitarias masivas devueltas desde VMAP no respetan la posición de anticipación Just-In-Time.

**Android TVSDK 2.5.6**

* No se admiten varias pausas publicitarias de VMAP al mismo tiempo.

**Android TVSDK 2.5.3**

Esta versión tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja o condiciones de red deficientes.
* Para los flujos FER, virtualTime y localTime pueden diferir. FER con desplazamiento tampoco funciona.
* La reproducción puede quedarse atascada cuando se busca el contenido de Enlace tardío de audio.
* De forma intermitente, los subtítulos webVTT pueden no estar sincronizados para el contenido en directo.
* De forma intermitente, se puede ver una reproducción rápida de algunos fotogramas tras salir de una pausa publicitaria.
* A veces, se genera un error 303 para Tripple Wrapper Ad Breaks, aunque se reproduzcan anuncios.

**Android TVSDK 2.5.2**

Esta versión tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja.
* La reproducción puede detenerse en ocasiones cuando se busca el final del contenido de VOD.
* Para los flujos FER, virtualTime y localTime pueden diferir. Además, FER con desplazamiento no funciona.

**Android TVSDK 2.5.1**

Esta versión de TVSDK tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja.
* Para los flujos FER, virtualTime y localTime pueden diferir. Además, FER con desplazamiento no funciona.
* En VMAP XML, si hay una etiqueta VAST vacía sin una etiqueta de cierre explícita (&lt;/vast>), y sin una nueva línea después de él, entonces el XML VMAP no se analiza correctamente y es posible que los anuncios no se reproduzcan.
* No se admiten las actualizaciones posteriores a la emisión de VPAID.

## Recursos útiles {#helpful-resources}

* [Requisitos del sistema](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [Guía del programador de TVSDK 3.10 para Android](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [TVSDK Android Javadoc para referencia de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [Documento de API de TVSDK para Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - Cada clase Java tiene una clase C++ correspondiente y la documentación de C++ contiene más material explicativo que Javadocs; por lo tanto, consulte la documentación de C++ para obtener más información sobre la API de Java.
* [Guía de migración de TVSDK 1.4 a 2.5 para Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Para conocer los casos de activación/desactivación de la pantalla, consulte la `Application_Changes_for_Screen_On_Off.pdf` archivo incluido en la compilación.
* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
