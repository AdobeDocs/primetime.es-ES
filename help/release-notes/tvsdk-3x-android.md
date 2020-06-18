---
title: Notas de la versión de TVSDK 3.12 para Android
seo-title: Notas de la versión de TVSDK 3.12 para Android
description: Las notas de la versión de TVSDK 3.12 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 3.12
seo-description: Las notas de la versión de TVSDK 3.12 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 3.12
uuid: 685d46f5-5a02-4741-af5c-91e91babd6f7
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 3a27379f-3cef-4ea3-bcae-21382dc1e9fd
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '5417'
ht-degree: 0%

---


# Notas de la versión de TVSDK 3.12 para Android {#tvsdk-for-android-release-notes}

Las notas de la versión de TVSDK 3.12 para Android describen las novedades o los cambios, los problemas resueltos y conocidos y los problemas de dispositivo en TVSDK Android 3.12.

El reproductor de referencia de Android se incluye con Android TVSDK en el directorio samples/ de su distribución. El archivo README.md que lo acompaña explica cómo crear el reproductor de referencia.

>[!NOTE]
>
>Para crear correctamente el reproductor de referencia, tal como se describe en README.md distribuido con la versión, asegúrese de hacer lo siguiente:
>
>1. Descargue VideoHeartbeat.jar de [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (VideoHeartbeat Library para Android v2.0.0)
>1. Extraiga VideoHeartbeat.jar en la carpeta libs/.
>



TVSDK para Android proporciona muchas mejoras de rendimiento con respecto a las versiones anteriores. Proporciona una experiencia de visualización de alta calidad y incorpora todas las características de la versión 1.4, con la excepción de la compatibilidad con Multi-CDN.

El conjunto completo de funciones compatibles y no compatibles se presenta en la sección Matriz [de](#feature-matrix) funciones de las notas de la versión.

## Android TVSDK 3.12

La versión de gradle de la aplicación Primetime Reference ahora se actualiza a la versión 5.6.4.

Para configurar y ejecutar la aplicación de referencia mediante Android Studio, siga las instrucciones del archivo Léame disponible con el zip de TVSDK en `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

Los principales problemas de los clientes corregidos en la versión actual se mencionan en la sección de problemas [](#resolved-issues) resueltos.

### Nuevas funciones y mejoras en las versiones anteriores

**Android TVSDK 3.11**

* **Cabecera específica del sistema de protección (PSSH) Casilla permitida** : TVSDK permite recuperar el cuadro de encabezado específico del sistema de protección asociado al recurso de medios cargado actualmente. Se ha añadido una nueva API `getPSSH()` a `com.adobe.mediacore.drm.DRMManager`.

Para obtener más información, consulte [Widevine DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

La versión se centró en solucionar los principales problemas de los clientes, como se indica en la sección de problemas [](#resolved-issues) resueltos.

**Android TVSDK 3.9**

* **Envío seguro a través de HTTPS** : Android TVSDK 3.9 introdujo las funciones de envío seguro a través de HTTPS para ofrecer contenido de forma segura con una escala y un rendimiento incomparables.

   Para activar el envío seguro a través de HTTPS, se ha introducido una nueva API en la `NetworkConfiguration` clase.

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Compatibilidad previa con la función** Ad-Break parcial: Con esta mejora, TVSDK 3.8 admite anuncios previos con la función Parcial Ad-Break (PABI).

El anuncio previo, si está disponible, se reproduce y, a continuación, el contenido se reproduce desde el punto en directo emulando la experiencia de la televisión en directo.

**Android TVSDK 3.7**

* Para el contenido de la prueba Widevine, se muestra una nueva API `setMediaDrmCallback` en la clase DRMManager para anular la implementación predeterminada de la interfaz MediaDrmCallback.

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* Se corrigió el error de AppCrash para no administrar `MediaPlayerEvent.ITEM_UPDATED` en la capa C++ (Android de 64 bits).

**Android TVSDK 3.6**

* **Mejore sus aplicaciones para satisfacer los requisitos** de 64 bits: la biblioteca nativa `(libAVEAndroid.so)` se ha actualizado y está disponible en dos versiones. Se ha cambiado la ubicación de la biblioteca nativa armeabi (32 bits) `/framework/Player to /framework/Player/armeabi` y se ha introducido una biblioteca adicional arm64-v8a (64 bits) en `/framework/Player/arm64-v8a.`

**Versión 3.5**

* **Resolución** de publicidad justo en tiempo: TVSDK 3.5 elimina la compatibilidad de las publicidades reproducidas de la línea de tiempo.

* **Compatibilidad habilitada para la reproducción** sin conexión: con la reproducción sin conexión, los usuarios pueden descargar contenido de vídeo en sus dispositivos y verlo cuando no están conectados. Para obtener información detallada, consulte &quot;Reproducción[sin conexión con Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf)&quot;.

**Versión 3.4**

* TVSDK ahora admite la reproducción de flujos CMAF para flujos CBC cifrados y sin formato.

**Versión 3.3**

* **Cambios en la API**

   * Se agrega una nueva API para `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` gestionar errores de red y tiempos de espera.
      * donde (n) es el número de reintentos.

**Versión 3.2**

* **Compatibilidad con la descarga de manifiesto y la resolución de publicidad paralela**

   * TVSDK 3.2 admite la resolución simultánea, en lugar de la resolución secuencial para todas las solicitudes de publicidad y los saltos de publicidad excepto para VMAP.

   * Todos los manifiestos de publicidad en una pausa publicitaria se descargan simultáneamente.

* **Se ha habilitado la compatibilidad con la resolución de anuncios y el tiempo de espera de descarga de manifiestos.**

   * Los usuarios ahora pueden establecer el valor de tiempo de espera para la resolución general de publicidad y las descargas de manifiesto.  En el caso de VMAP, el valor de tiempo de espera se aplica a los saltos de publicidad individuales, ya que todos los saltos de publicidad se resuelven secuencialmente.

* **Se han introducido nuevas API en la clase AdvertisingMetadata:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **Se ha eliminado la siguiente API de la clase AdvertisingMetadata:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **Reproducción habilitada de flujos con códec de audio AC3/EAC3**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` en `MediaPlayer` clase

* **TVSDK admite la reproducción de flujos sin formato y CMAF para CTR Widevine cifrado.**

* **Ahora se admite la reproducción de flujos HEVC de 4.000 rpm.**

* **Solicitudes** de llamada de publicidad paralelas: TVSDK ahora obtiene previamente 20 solicitudes de llamada de publicidad en paralelo.

**Versión 3.0**

* **TVSDK 3.0 admite flujos de codificación de vídeo de alta eficiencia (HEVC).**

* **Justo en el tiempo: la resolución de publicidades más cercanas a los marcadoresLa resolución de publicidades flojas ahora resuelve cada pausa publicitaria de forma independiente.** Anteriormente, la resolución de anuncios era un enfoque de dos fases: se resolvieron los pre-rolls antes del inicio de reproducción y todas las ranuras de rollover media/post combinadas después de iniciar la reproducción. Con esta función mejorada, cada pausa publicitaria ahora se resuelve en un momento específico antes del punto de referencia del anuncio.

> [!NOTE]
>
> La resolución diferida de publicidad ahora ha cambiado para desactivarse de forma predeterminada y debe habilitarse explícitamente.

Se agrega una nueva API a `AdvertisingMetadata::setDelayAdLoadingTolerance` para obtener la tolerancia de carga de anuncios retrasados asociada con estos metadatos de publicidad.\
Ahora se permite la búsqueda inmediatamente después de la PREPARACIÓN, la búsqueda por sobrecostos de anuncios resultará en una resolución inmediata antes de que finalice la búsqueda.\
Se admiten los modos `SERVER_MAP` de señalización y `MANIFEST_CUES` .

Para obtener más información, consulte [TVSDK 3.0 for Android Programmer&#39;s Guide](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) on API and evento changes (Guía del programador de Android 3.0 sobre los cambios en la API y el ).

* **Actualizado`targetSdkVersion`a la versión más reciente**

Se ha actualizado `targetSdkVersion` de 19 a 27 para un buen funcionamiento.

* **Placement.Type getPlacementType() es ahora un método en la interfaz TimelineMarker**

   Este método devolverá un tipo de colocación de Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Si no se resuelve una pausa publicitaria, el método getDuration() de la interfaz TimelineMarker devolverá 0.

**Versión 2.5.6.**

* **TVSDK 2.5 es compatible con Android P.**

* **Activación del audio de fondo**

   Para activar la reproducción de audio cuando la aplicación pasa de primer plano a segundo plano, la aplicación debe llamar a la `enableAudioPlaybackInBackground` API de MediaPlayer con true como argumento cuando el reproductor está en estado PREPARADO.

* **alwaysUseAudioOutputLatency(valor booleano) en la clase MediaPlayer**

Cuando esté configurado, utilice la latencia de salida en el cálculo de la marca de tiempo de audio.
Parámetros booleanos val: True utilizará la latencia de salida de audio en el cálculo de la marca de tiempo de audio.

* **Optimizado para obtener la mejor experiencia de reproducción, incluso si la velocidad de ancho de banda cae repentinamente**

TVSDK ahora cancela la descarga del segmento en curso, si es necesario, y cambia dinámicamente a la representación adecuada. Esto se hace cambiando sin interrupciones entre las velocidades de bits.

**Versión 2.5.5**

* **Inserción parcial de Ad-Break**

   Experiencia similar a la televisión de unirse en medio de un anuncio sin activar el seguimiento del anuncio parcialmente visto.\
   Ejemplo: El usuario se une en el medio (a los 40 segundos) de una pausa publicitaria de 90 segundos que consta de tres anuncios de 30 segundos. Pasarán 10 segundos desde el segundo anuncio de la pausa.

   * El segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.

   * Los rastreadores de anuncios para el anuncio parcial reproducido (segundo anuncio) no se activan. Se activan los rastreadores solamente para el tercer anuncio.

* **Carga segura de publicidad a través de HTTPS**

   Adobe Primetime ofrece una opción para solicitar la primera llamada al servidor de publicidad primetime y CRS a través de https.

* **AdSystem e ID de creativo agregados a las solicitudes de CRS**

   Ahora se incluyen `AdSystem` y `CreativeId` como parámetros nuevos en las solicitudes 1401 y 1403.

* **Se ha eliminado** la API setEncodeUrlForTracking en la clase NetworkConfiguration, ya que se deben codificar los caracteres no seguros de una dirección URL.

**Versión 2.5.4**

Android TVSDK v2.5.4 oferta las siguientes actualizaciones y cambios de API:

* Cambios en el valor predeterminado de `WebViewDebbuging`

   `WebViewDebbuging` se establece en `Fals`e de forma predeterminada. Para habilitarlo, llame `setWebContentsDebuggingEnabled(true)` a la aplicación.

* **Actualización de la versión OpenSSL y Curl**

   Se ha actualizado libcurl a v7.57.0 y OpenSSL a v1.0.2k.

* Acceso a nivel de aplicación para el objeto de respuesta VAST

   Se ha introducido una nueva API `NetworkAdInfo::getVastXml()` que proporciona acceso al objeto de respuesta VAST a la aplicación.

**Versión 2.5.3**

Android TVSDK v2.5.3 oferta las siguientes actualizaciones y cambios de API.

* Se recomienda a todos los clientes de TVSDK que utilicen CRS que actualicen sus aplicaciones con TVSDK 2.5.3.85 o posterior en Android. Esto sustituirá a la implementación de la aplicación existente. Tras la actualización de TVSDK, compruebe si hay solicitudes de URL creativas de CRS en una herramienta proxy (por ejemplo: Charles) y confirme que el nombre de host y la versión de la ruta de acceso se reflejan como en la estructura de URL de ejemplo siguiente.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente de usuario de TVSDK personalizable: hemos añadido algunas API nuevas para personalizar los agentes de usuario.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Uso compartido de cookies entre la aplicación Android y TVSDK: Android TVSDK ahora admite el acceso a cookies entre la capa JAVA (almacenada en CookieStore de la aplicación Android) y la capa C++ TVSDK. Ahora, es posible configurar y/o modificar las cookies en la capa nativa de C++, ya que estarán expuestas al almacén de cookies de Java.

* Cambios en la API:

   * Se `CookiesUpdatedEvent` agrega un nuevo Evento. El reproductor de medios lo distribuye cuando se actualiza la cookie.

   * Se agrega una nueva API a `NetworkConfiguration::set/ getCustomUserAgent()` para usar un agente de usuario personalizado.

   * Se agrega una nueva API a `NetworkConfiguration::set/ getEncodedUrlForTracking` para forzar la codificación de caracteres no seguros.

   * Se agrega una nueva API a `NetworkConfiguration::getNetworkDownVerificationUrl()` para establecer una URL de verificación de red en caso de una conmutación por error.

   * Se agrega una nueva propiedad `TextFormat::treatSpaceAsAlphaNum` que define si se debe tratar el espacio como alfanumérico mientras se muestran los rótulos.

* Cambios en `SizeAvailableEvent`. Anteriormente, `getHeight()` y `getWidth()` métodos de `SizeAvailableEvent` en 2.5.2 se utilizaban para devolver la altura y la anchura del marco, que devolvía el formato de medios. Ahora devuelve la altura de salida y la anchura de salida respectivamente devueltas por el descodificador.

* Cambios en el comportamiento de almacenamiento en búfer: Se cambia el comportamiento de almacenamiento en búfer. Depende del desarrollador de la aplicación lo que desea hacer en caso de que el búfer esté vacío. 2.5.3 utiliza el tamaño del búfer de reproducción en una situación vacía del búfer.

**Versión 2.5.2**

Android TVSDK v2.5.2 oferta importantes correcciones de errores y algunos cambios en la API.

**Versión 2.5.1**

Las nuevas funciones importantes lanzadas en Android 2.5.1.

* **Mejoras de rendimiento:** la nueva arquitectura TVSDK 2.5.1 ofrece una serie de mejoras de rendimiento. Según las estadísticas de un estudio de evaluación comparativa de terceros, la nueva arquitectura ofrece una reducción de 5 veces en el tiempo de inicio y de 3,8 veces menos en comparación con el promedio del sector:

* **Activado instantáneamente para VOD y en directo:** cuando se activa la activación instantánea, TVSDK inicializa y almacena en búfer los medios antes de los inicios de reproducción. Dado que puede iniciar varias instancias de MediaPlayerItemLoader simultáneamente en segundo plano, puede almacenar en búfer varios flujos. Cuando un usuario cambia el canal y el flujo se almacena correctamente en el búfer, la reproducción en los nuevos inicios de canal se realiza inmediatamente. TVSDK 2.5.1 también admite la activación instantánea para flujos **en directo** . Los flujos activos se vuelven a almacenar en búfer cuando se mueve la ventana activa.

* **Lógica de ABR mejorada:** la nueva lógica de ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que el ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúe y también optimiza el número de veces que el conmutador de velocidad de bits realmente se produce monitoreando la velocidad a la que cambia la longitud del búfer.

* **Descarga parcial de segmentos / Subsegmentación:** TVSDK reduce aún más el tamaño de cada fragmento para poder inicio de la reproducción lo antes posible. El fragmento ts debe tener un fotograma clave cada dos segundos.

* **Resolución de anuncios diferida:** TVSDK no espera a la resolución de anuncios no previos antes de iniciar la reproducción, lo que reduce el tiempo de inicio. Las API, como la búsqueda y la reproducción mediante trucos, siguen sin permitirse hasta que se resuelvan todos los anuncios. Esto es aplicable a los flujos de VOD utilizados con CSAI. Las operaciones como la búsqueda y el avance rápido no se permiten hasta que se complete la resolución de la publicidad. Para transmisiones en directo, esta función no se puede habilitar para la resolución de anuncios durante un evento en directo.

* **Conexiones de red persistentes:** Esta función permite a TVSDK crear y almacenar una lista interna de conexiones de red persistentes. Estas conexiones se reutilizan para varias solicitudes, en lugar de abrir una nueva conexión para cada solicitud de red y luego destruirla posteriormente. Esto aumenta la eficiencia y disminuye la latencia del código de red, lo que da como resultado un rendimiento de reproducción más rápido.
Cuando TVSDK abre una conexión, solicita al servidor una conexión *permanente* . Es posible que algunos servidores no admitan este tipo de conexión, en cuyo caso TVSDK volverá a establecer una conexión para cada solicitud. Además, aunque las conexiones persistentes estarán activadas de forma predeterminada, TVSDK ahora tiene una opción de configuración para que las aplicaciones puedan desactivar las conexiones persistentes si lo desea.

* **Descarga paralela:** la descarga de vídeo y audio en paralelo en lugar de en serie reduce los retrasos de inicio. Esta función permite reproducir archivos HLS Live y VOD, optimiza el uso de ancho de banda disponible en un servidor, reduce la probabilidad de entrar en situaciones de búfer en ejecución y minimiza el retraso entre descarga y reproducción.

* **Descargas de anuncios paralelas:** TVSDK recopila previamente las publicidades en paralelo a la reproducción de contenido antes de visitar las pausas publicitarias, lo que permite una reproducción transparente de las publicidades y el contenido.

* **Reproducción**

* **Reproducción de contenido MP4: no es necesario volver a transcodificar los clips cortos MP4 para que se reproduzcan dentro del TVSDK.**

   > [!NOTE]
   >
   > El cambio de ABR, la reproducción mediante trucos, la inserción de anuncios, el enlace de audio tardío y la subsegmentación no son compatibles con la reproducción de MP4.

* **Reproducción de trucos con velocidad de bits adaptable (ABR):** esta función permite que TVSDK cambie entre flujos de iFrame mientras se encuentra en modo de reproducción de trucos. Puede utilizar perfiles que no sean de iFrame para realizar el juego con trucos a velocidades más bajas.

* **Reproducción de trucos más fluida:** Estas mejoras mejoran la experiencia del usuario:

   * Selección de velocidad de bits y velocidad de fotogramas adaptable durante la reproducción mediante trucos, según el ancho de banda y el perfil del búfer

   * Uso del flujo principal en lugar del flujo IDR para obtener una reproducción rápida de hasta 30 fps.

* **Protección del contenido**

   * **Protección de salida basada en resolución:** Esta función vincula las restricciones de reproducción con resoluciones específicas, proporcionando controles DRM más precisos.

* **Compatibilidad con flujos de trabajo**

   * **Integración de facturación directa:** envía métricas de facturación al servidor de Adobe Analytics, certificado por Adobe Primetime para flujos utilizados por el cliente.
   TVSDK recopila automáticamente métricas, de acuerdo con el contrato de venta del cliente, para generar informes de uso periódicos requeridos para fines de facturación. En todos los eventos de inicio de flujo, TVSDK utiliza la API de inserción de datos de Adobe Analytics para enviar métricas de facturación como, por ejemplo, el tipo de contenido, los indicadores habilitados para la inserción de anuncios y los indicadores habilitados para drm (según la duración del flujo facturable) al grupo de informes propiedad de Adobe Analytics Primetime. Esto no interfiere con los grupos de informes o las llamadas al servidor de Adobe Analytics del cliente ni se incluye en ellos. Si se solicita, este informe de uso de facturación se envía a los clientes de forma periódica. Esta es la primera fase de la función de facturación que admite únicamente la facturación de uso. Se puede configurar en función del contrato de venta mediante las API descritas en la documentación. Esta función está habilitada de forma predeterminada. Para desactivar esta función, consulte la muestra del reproductor de referencia.

   * **Compatibilidad con failover mejorada: se han implementado estrategias adicionales para continuar la reproducción ininterrumpida, a pesar de los fallos de los servidores host, los archivos de listas de reproducción y los segmentos.**


* **Publicidad**

   * **Integración de Moat:** compatibilidad con la medición de la visibilidad de anuncios de Moat.

   * **Pancartas complementarias:** las pancartas complementarias se muestran junto con un anuncio lineal y, a menudo, se siguen mostrando en la vista después de que finalice el anuncio. Estas pancartas pueden ser de tipo html (fragmento HTML) o iframe (dirección URL de una página de iframe).

* **Analytics**

   * **VHL 2.0:** Esta es la última integración optimizada de Video Heartbeat Library (VHL) para la recopilación automática de datos de uso para Adobe Analytics. La complejidad de las API se ha reducido para facilitar la implementación. Descargue la biblioteca VHL [v2.0.0 para Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) y extraiga el archivo JAR en la carpeta libs.

* **SizeAvaliableEventListener**

   * `getHeight()` y `getWidth()` los métodos de `SizeAvailableEvent` ahora devolverán la salida en altura y anchura respectivamente. La relación de aspecto de visualización se puede calcular de la siguiente manera:

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      La relación de aspecto de Almacenamiento en cuanto a la anchura de la barra vertical y la altura de la barra también se puede utilizar para calcular la anchura del marco y la altura del marco:

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookies**

   * Android TVSDK ahora admite el acceso a cookies JAVA almacenadas en CookieStore de la aplicación Android. Se proporciona una API de llamada de retorno (onCookiesUpdated) para registrar cada vez que una nueva cookie se incluye como parte del encabezado **Set-Cookie** Response. Estas cookies están disponibles como Lista de HttpCookie(s) utilizadas para un URI o dominio diferente al configurar estos valores de cookies en ese URI o dominio concreto mediante CookieStore. Del mismo modo, los valores de las cookies en TVSDK se actualizan mediante la API de adición de CookieStore.

## Matriz de funciones {#feature-matrix}

TVSDK para Android admite una serie de funciones que puede implementar para agregar funcionalidad a las aplicaciones de vídeo.

En las tablas de funciones siguientes, una &#39;Y&#39; indica que la función es compatible con la versión actual.

| Función | Tipo de contenido | HLS |
|---|---|---|
| Reproducción general (Reproducir, Pausa, Buscar) | VOD + Activo | Y |
| FER: reproducción general (Reproducir, Pausa, Buscar) | FER VOD | Y |
| Buscar cuando se está reproduciendo un anuncio | VOD + Activo | No admitido |
| Reproducción HEVC | VOD + Activo | Solo contenedor fMP4 |
| AC3 y EAC3 | VOD + Activo | No admitido |
| MP3 | VOD | No admitido |
| Reproducción de contenido MP4 | VOD | Y |
| Lógica de conmutación de velocidad de bits adaptable | VOD + Activo | Y |
| Reproducción solo de audio | VOD + Activo | Y |
| Compatibilidad con varios CDN | VOD + Activo | No admitido |
| Reproducción de anuncios con medios solo de audio | VOD + Activo | No admitido |
| Subtítulos opcionales - 608/708 | VOD + Activo | Y |
| Subtítulos opcionales - WebVTT | VOD + Activo | Y |
| Conmutación por error de manifiesto | VOD + Activo | Y |
| Failover avanzado | VOD + Activo | Y |
| Notificaciones de QoS y reproductor | VOD + Activo | Y |
| Compatibilidad con encabezados de cookie | VOD + Activo | Y |
| Compatibilidad con encabezados HTTP personalizados | VOD + Activo | Y (se requiere que permita el listado) |
| Establecer parámetros de control de búfer | VOD + Activo | Y |
| Establecer controles de velocidad de bits adaptables | VOD + Activo | Y |
| Etiquetas de manifiesto personalizadas | VOD + Activo | Y |
| Enlace de audio tardío | VOD + Activo | Y |
| 302 Redirección | VOD + Activo | Y |
| Reproducción con desplazamiento | VOD + Activo | Y |
| Reproducción de trucos | VOD + Activo | Y |
| Movimiento lento en reproducción de truco | VOD + Activo | No admitido |
| Reproducción suave de trucos (con ABR) | VOD + Activo | Y |
| Análisis de ID3 | VOD + Activo | Y |
| Apagón de anuncios | VOD + Activo | No admitido |
| Instantáneo activado | VOD + Activo | No admitido |
| Compatibilidad con los marcadores de discontinuidad | VOD + Activo | Y |
| 302 Fijación de redirección | VOD + Activo | Y |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Reproducción general, publicidades habilitadas | VOD + Activo | Y |
| Contenido FER con anuncios habilitados | VOD | Y |
| Comportamientos de publicidad predeterminados | VOD + Activo | Y |
| VAST 2.0/3.0 | VOD + Activo | Y |
| VMAP 1.0 | VOD + Activo | Y |
| Publicidades MP4 | VOD + Activo | Y (de CRS) |
| Reproducción de trucos con publicidades habilitadas | VOD + Activo | Y |
| Solo publicidad | VOD | Y |
| Parámetros de objetivo | VOD + Activo | Y |
| Parámetros personalizados | VOD + Activo | Y |
| Comportamientos de publicidad personalizados | VOD + Activo | Y |
| Etiquetas de publicidad personalizadas | Live Live | Y |
| Resoluciones de publicidad personalizadas | VOD + Activo | Y |
| Resolución de publicidad personalizada FreeWheel | VOD | Y |
| C3 | VOD + Activo | No admitido |
| Resolución de publicidad diferida | VOD | Y |
| Compatibilidad con los marcadores de discontinuidad - SSAI | VOD + Activo | Y |
| Publicidades complementarias, publicidades tipo titular y publicidades en las que se puede hacer clic | VOD + Activo | Y |
| VPAID 2.0 | VOD + Activo | Y (JS) |
| Salida de publicidad anticipada | Live Live | Y |
| Prioridad creativa basada en reglas | VOD + Activo | Y |
| Reglas de CRS | VOD + Activo | Y |
| JSON Ad Resolver | VOD + Activo | No admitido |
| Integración de Moat | VOD + Activo | Y |
| Inserción parcial de pausa publicitaria | Live Live | Y |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Cifrado AES | VOD + Activo | Y |
| Cifrado AES de muestra | VOD + Activo | Y |
| Flujos tokenizados | VOD + Activo | Y |
| DRM amplio | VOD + Activo | Solo contenedor fMP4 |
| DRM Primetime | VOD + Activo | Y |
| Reproducción externa (RBOP) | VOD + Activo | Solo DRM de Primetime |
| Rotación de licencia | VOD + Activo | Solo DRM de Primetime |
| Rotación de clave | VOD + Activo | Solo DRM de Primetime |

| Función | Tipo de contenido | HLS |
|---|---|---|
| Integración con Adobe Analytics VHL | VOD + Activo | Y |
| Facturación | VOD + Activo | Y |

## Problemas resueltos {#resolved-issues}

Cuando la resolución está asociada a un problema informado, se muestra una referencia de Zendesk, por ejemplo ZD#xxxxx.

**Android TVSDK 3.12**

En esta sección se ofrece un resumen del problema resuelto en la versión de Android de TVSDK 3.12.

* ZD#40584 - La aplicación de referencia de Primetime no se genera con la versión más reciente de gradle.

### Problemas resueltos en versiones anteriores

**Android TVSDK 3.11**

* ZD#41252 - Caracteres coreanos en WebVTT rotos después de Android 7.1.

**Android TVSDK 3.10**

* ZD#40340 - La aplicación se bloquea con el error &quot;App Not Responding&quot; al intentar reproducir después de poner en la lista negra todos los archivos TS (TypeScript).

**Android TVSDK 3.8**

* No se agregaron nuevos problemas.

**Android TVSDK 3.7**

* No se agregaron nuevos problemas.

**Android TVSDK 3.6**

* No se agregaron nuevos problemas.

**Versión 3.5**

* ZD#37503 - Las respuestas de JSON para las reglas de CRS se almacenan en caché para evitar las solicitudes de duplicado.

**Versión 3.4**

* ZD#37996 - Se ha corregido un problema de reproducción de disquetes en los flujos HEVC CMAF lineales y VOD.
* ZD#37706 - Se ha corregido un problema con los rótulos incorrectos.
* ZD#37622 - Se ha corregido un problema con URISyntaxErrors fatales en anuncios específicos.
* ZD#36938 - Se ha corregido un problema que hacía que la velocidad de bits pasara a la velocidad de bits media y, a continuación, llegara a la velocidad de bits más alta después de salir de las reproducciones de trucos.

**Versión 3.3**

* ZD#37394 - El recurso CMAF provoca artefactos rápidamente después de que cambie la velocidad.
   * Se ha corregido un problema que se producía con un cambio de perfil durante la reproducción con trucos.
* ZD#37396 - Faltan eventos de seguimiento de anuncios para algunos segmentos intermedios y posteriores.
   * Se corrigió un caso específico en torno a los eventos de seguimiento de publicidad.
* ZD#37491 - El código de estado HTTP con error meta no está presente.
   * Se trabajó en la propagación de errores de red más altos en la pila.
* ZD#37808 - Permitir la lista Nuevo encabezado personalizado.
   * Se agregó compatibilidad con SSAI_TAG como parte de esta corrección.
* ZD#37622 - Errores de sintaxis de pods de publicidad específicos.
   * Se ha corregido un problema por el que la reproducción de flujo se bloqueaba cuando la aplicación de Android del cliente ofrecía anuncios que contenían un % sin codificar
* ZD#37631 - Mecanismo de reintento de manifiesto maestro para Android TVSDK.
   * Se Añadió una nueva API en la configuración de red para gestionar esta mejora. Si no se utiliza esta API, no se volverá a intentar el manifiesto. Si se utiliza, se volverá a intentar el manifiesto para gestionar errores de red y tiempos de espera.

**Versión 3.2**

* ZD#37493- Las señalizaciones de seguimiento para la reproducción en directo no se activan de forma intermitente para el primer anuncio en secuencia.
* ZD#36985- Las señalizaciones de seguimiento no se envían para saltos de anuncios vacíos en la respuesta de VMAP.
* ZD#37134 - TVSDK emite el ID incorrecto para la respuesta VMAP de forma intermitente.

**Versión 3.0**

* ZD#33740 - TVSDK emite una advertencia innecesaria justo después de crear un objeto MediaPlayer y llamar a replaceCurrentResource()

   * Se ha mejorado la corrección anterior al llamar a restore solo cuando el reproductor está en estado suspendido

* ZD#36442 - Cada nueva reproducción desconecta la sesión de depuración remota, lo que hace imposible la depuración.

   * La depuración no es posible de forma predeterminada en la vista web, ya que la depuración no está habilitada de forma predeterminada. La aplicación debe habilitar la depuración si es necesario, llamando a setWebContentsDebuggingEnabled(true) en el objeto devuelto desde MediaPlayer.getCustomAdView().

* ZD#33688 - Compatibilidad con Just In Time y resolución

   * Los saltos de publicidad se resuelven a un intervalo especificado antes de la posición de la pausa publicitaria.

* ZD#36441 - La duración de la ventana activa sigue aumentando más de 5 minutos y provoca varios problemas.

   * Se corrigió un problema en el cual virtualStartTime se agregaba dos veces al calcular el punto de lanzamiento virtual, lo que daba como resultado este problema.

**Android TVSDK 2.5.6**

* ZD #34992 - El idioma está vacío en los subtítulos opcionales.

   * Se ha corregido un caso en el que TVSDK no analizaba #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS desde el manifiesto principal para obtener los detalles del seguimiento de rótulos.

* ZD #35078 - Validación de Android P.

   * TVSDK 2.5.6 se ha validado con las últimas compilaciones beta de Android P. No se encontraron problemas debido al nuevo sistema operativo Android.

* ZD #34149 - El reproductor continúa solicitando los manifiestos aunque se encuentre un error.

   * Se corrigió el caso en el que TVSDK realizaba llamadas repetitivas incluso cuando todos los perfiles estaban inactivos (error 404).

* ZD #31533 - Reproducción de audio en Android después de enviar la aplicación al fondo.

   * API `enableAudioPlaybackInBackground` Añadida de MediaPlayer a la que se debe llamar con &#39;True&#39; como argumento (cuando el reproductor está en estado PREPARADO) para activar la reproducción de audio cuando la aplicación está en segundo plano.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640 x 368 cuando el tamaño real del vídeo es 640 x 360.

   * Debido a que la variable m_nOutputHeight (dentro de AndroidMCVideoDecoder) se está actualizando con la altura del marco en lugar de la altura de salida real. Se han realizado cambios relevantes en la función getVideoFrame para calcular m_nOutputHeight correctamente.

* ZD #26614 - Urgente — servicio de publicidad de terceros/programático — fracaso en el servicio de impresiones.

   * Se ha mejorado la corrección anterior al gestionar el caso en el análisis de XML en el que el problema se podía reproducir cuando &quot;espacio&quot; estaba antes del signo &quot;igual&quot; como &lt;VAST version =&quot;2.0&quot;>

* ZD #29296 - Android: Añada AdSystem y el ID creativo a las solicitudes de CRS.

   * Ahora se incluyen &#39;AdSystem&#39; y &#39;CreativeId&#39; como parámetros nuevos en las solicitudes 1401 y 1403.

* ZD #33062 - El SDK de TVSDK se bloquea en la incidencia de caracteres de barra vertical en la respuesta VAST en el nodo CDATA

   * Se eliminó la API setEncodeUrlForTracking en la clase NetworkConfiguration como caracteres no seguros en una dirección URL que se va a codificar

* ZD #33063 - Error en la lógica de selección de archivos CRS: TVSDK no enviaba una solicitud CRS de formato web sino que la enviaba para archivos 3gpp.

   * Se corrigió la lógica ahora. Al utilizar archivos de medios con formato web y 3gpp, se envía una solicitud CRS para el webm. Además, al utilizar ambos archivos de medios con formato 3gpp, se envía la solicitud CRS para el archivo 3gpp de velocidad de bits más alta.

* ZD #33125 - La aplicación de Android se bloquea con una etiqueta específica de DoubleClick dentro del VMAP.

   * Se corrigió el escenario para evitar el bloqueo.

* ZD #32256 - Problema de rotación de licencias y rotaciones clave - Adobe Access

   * Se corrigió la inicialización de segmentos con los metadatos DRM para el contenido de SampleAES. Funciona bien con contenido AES128.

* ZD #33619 - Reenvío rápido de un creciente contenido de listas de reproducción atascado en el estado de almacenamiento en búfer cerca del punto activo.

   * Se ha gestionado el caso al cruzar el punto activo en el modo de reproducción mediante trucos

* ZD #34151 - Objetos TimedMetadata desordenados.

   * Dos eventos TimedMetadata aparecían en orden aleatorio si pertenecían al mismo tiempo en la línea de tiempo. Mantuvo su orden original en manifiesto.

* ZD #34189 - Problema al buscar el comienzo de una pausa publicitaria.

   * El problema era con los anuncios de SSAI que se vinculan usando discontinuidad. Y la causa fue un comportamiento cuando buscamos el comienzo de esos anuncios, buscamos un fotograma clave y no lo encontramos. La razón era que la marca de tiempo de audio mínima del anuncio era anterior a la marca de tiempo mínima del vídeo. Por lo tanto, terminamos buscando un marco clave en los datos fragmentDump incorrectos. Corregido ahora.

* ZD #34528 - La resolución de vídeo no se actualiza más allá de 640 x 360 en la llave de tercera generación de FireTV.

   * Se ha mejorado la corrección para incluir las últimas actualizaciones de firmware

* ZD #34793 - TVSDK 2.5.x se utilizaba para bloquear con la resolución de contenido personalizado en algunos casos cuando VideoEngine suponía que auditudeSettings estaba disponible y no lo estaba.

   * El bloqueo se producía debido a una llamada de función en un puntero compartido Null (auditudeSettings). Se ha Añadido una comprobación condicional dentro de VideoEngineTimeline::placeToSourceTimeline() para asegurarse de que auditudeSettings esté disponible antes de llamar a cualquier elemento de ese objeto.

* ZD #32584 - No se puede acceder a la información completa presente en el nodo &lt;Extensions> de una respuesta VAST.

   * Se corrigió el problema en el análisis de XML y ahora NetworkAdInfo proporciona la información completa presente en el nodo &lt;Extensions>

* ZD #35086 - No se obtienen datos de extensión completos del reproductor en caso de respuestas VMAP específicas.

   * El problema era específico de xml de extensión, ya que el análisis de XML no funcionaba si xml de extensión tenía comillas de doble dentro del valor de atributo. Se corrigió el problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Sesión de reproducción que habilita la depuración remota de la vista de web.

WebViewDebuging se establece en False de forma predeterminada. Para habilitar la depuración, configúrela como true mediante la aplicación, mediante setWebContentsDebuggingEnabled(true).

* ZenDesk#33011 - La cronología de la publicidad no se resuelve en caso de que se produzca un error en la solicitud de CRS.

   Cuando falla una solicitud de CRS a una publicidad, la línea de tiempo se resuelve y se reproducen las demás publicidades.

* ZenDesk#34528 - La resolución de vídeo no se actualiza más allá de los 640 x 360 en la llave de la tercera generación de FireTV.

   La resolución de vídeo se activa como conmutadores de velocidad de bits.

* ZenDesk#33192 - AudioTrack tiene un nombre nulo cuando la pista se recupera mediante AudioUpdatedEventListener::onAudioUpdated.

   En algunos casos en FireTV Stick, el evento onAudioUpdate se activaba cuando no había ninguna actualización de audio. Esto se ha solucionado ahora.

**Android TVSDK 2.5.3**

* Zendesk#32216 - La suscripción de etiquetas personalizada TimedMetadata no funciona.

   Estamos devolviendo datos de ID3 como una matriz de bytes (para admitir datos de APIC o genéricos) al cliente, mientras que en 1.4 devuelve una cadena. La matriz de bytes no gestiona el carácter terminado nulo en sí misma, por lo tanto mostraba un carácter especial al cliente. Este problema se ha solucionado ahora.
* Zendesk#32670 - El jugador no falla en la lista de reproducción redundante

   Esto funciona bien ahora y setNetworkDownVerifyUrl funciona correctamente.
* Zendesk#32369 - Los subtítulos opcionales muestran diferentes elementos o elementos de color.

   Se ha solucionado el problema con los problemas de CC en la última compilación
* Zendesk #25590 - Mejore: Almacén de cookies TVSDK ( C++ a JAVA )

   Android TVSDK ahora admite el acceso a cookies entre la capa JAVA (almacenada en CookieStore de la aplicación Android) y la capa C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 no parece tener la corrección para PTPLAY-20269

   Este problema se ha corregido e integrado en la rama 2.5.2.
* Zendesk#31806 - Palos de audiencia en la preparación

   El reproductor estaba atascado en el estado de preparación porque el xml de respuesta tenía una etiqueta vacía. Ahora se ha solucionado el problema.
* Zendesk#31727 - Los caracteres de subtítulos opcionales TVSDK 2.5 se eliminan o se escriben mal.

   Se ha solucionado el problema y no se está eliminando o escribiendo incorrectamente ningún carácter.
* Zendesk#31485 - DrmManager en 2.5

   Hubo algún problema en Creación de DrmManager mediante un nuevo DrmManager(contexto de contexto). Se implementó la clase DRMService que proporcionaría DRMManager.
* El flujo de resolución Zendesk#32794- 1080P no se reproduce en Android

   hemos cambiado los métodos SizeAvailableEvent y Anteriormente, getHeight() y getWidth() de SizeAvailableEvent en 2.5 para devolver la altura y la anchura del fotograma, que el formato de medios devuelve. Ahora devuelve la altura de salida y la anchura de salida, respectivamente, que devuelve el descodificador.
* Zendesk #19359 Flash Player se bloquea debido a la posición del atributo #EXT-X-FAXS-CM en el manifiesto de nivel de conjunto.

   La etiqueta #EXT-X-FAXS-CM siempre debe aparecer en la lista de reproducción superior para que la velocidad de bits individual o los segmentos aparezcan en la lista de reproducción.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artefactos en subtítulos cerrados con fondo no opaco.

   Se expone la propiedad setTreatSpaceAsAlphaNum en TextFormat. De forma predeterminada, la propiedad es False. Establezca la propiedad como True en un cliente para resolver el problema del espacio oscuro.

* La pantalla de Zendesk#25097 CC tiene artefactos visuales con ajustes CC.

   Se expone la propiedad setTreatSpaceAsAlphaNum en TextFormat. De forma predeterminada, la propiedad es False. Establezca la propiedad como True en un cliente para resolver el problema del espacio oscuro.

* Zendesk #31620 La cadena del agente de usuario que sale del reproductor TVSDK está truncada.

   La cadena del agente de usuario ya no se truncará después de 128 caracteres.

   La cadena de versión de Adobe Primetime se agrega al agente de usuario del sistema.

* El evento de Zendesk #30809 que falta SEEK_END impide que la aplicación pase a un estado de reproducción.
* El color &#39;cian&#39; de Zendesk #30415 de los subtítulos opcionales es ahora un tono azul (turquesa) más oscuro en comparación con las versiones anteriores de Primetime TVSDK.

   El color se cambia de DarkCyan a Cian.

* Los anuncios de Zendesk #30727 de VOD no se están descargando ni resolviendo.

   En VMAP XML, si hay una etiqueta VAST vacía sin una etiqueta de cierre explícita (&#39;&lt;/VAST>&#39;) y sin un carácter de nueva línea después de ella, el XML VMAP no se analiza correctamente y es posible que no se reproduzcan las publicidades.

**Android TVSDK 2.5.1**

* Bloqueo específico del dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA con Auditude y haga clic en los anuncios.
* VHL: se envían llamadas de Heartbeat incorrectas al iniciar contenido desde un desplazamiento.
* Cuando se reproducen anuncios VPAID, falta el anuncio evento:tipo:play en VHL Heartbeat.
* Después de entrar en estado COMPLETO, el reproductor vuelve al estado REPRODUCIENDO con SKIP adBreakPolicy para anuncios posteriores al lanzamiento.
* Las cookies no se adjuntan a las rellamadas de anuncios salientes.
* Los puntos de referencia de anuncios no están visibles.
* No se cargarán HLS con un seguimiento EAC3 SAP independiente.
* El reproductor se bloquea cuando TVSDK recibe una calidad de pantalla activada después de restaurar el reproductor multimedia.

## Problemas y limitaciones conocidos {#known-issues-and-limitations}

**Android TVSDK 3.11**

* No se agregaron nuevas limitaciones.

### Problemas conocidos y limitaciones de las versiones anteriores

**Android TVSDK 3.10**

* No se agregaron nuevas limitaciones.

**Android TVSDK 3.8**

* No se agregaron nuevas limitaciones.

**Android TVSDK 3.7**

* No se agregaron nuevas limitaciones.

**Android TVSDK 3.6**

* No se agregaron nuevas limitaciones.

**Android TVSDK 3.5**

* No se ha agregado ninguna nueva limitación.

**Android TVSDK 3.4**

* No se ha verificado la compatibilidad con ID3, subtítulos opcionales y audio de enlace tardío para el flujo CMAF (CBC).
* En algunos dispositivos, existe un problema de baja reproducibilidad debido al cual la distorsión de vídeo puede aparecer en la parte superior durante la reproducción mediante trucos en flujos CMAF.

**Android TVSDK 3.3**

* los subtítulos clcp:c608 no son compatibles con la reproducción de flujo CMAF.

**Android TVSDK 3.2**

* TVSDK 3.2 no admite la reproducción de flujos AES de muestra CMAF y AES128.
* Los flujos CMAF HEVC no incluyen compatibilidad con la reproducción de subtítulos cerrados.
* La coloración verde aparece en los flujos cifrados WV cuando la búsqueda se realiza alrededor del segmento no cifrado.
* Los flujos CMAF no admiten eventos ID3.
* Los flujos HLS no admiten el formato de rótulos TTML.

**Android TVSDK 3.0**

* La compatibilidad con HEVC tiene las siguientes limitaciones en esta versión

   * DRM no compatible
   * Compatibilidad con CC (CEA 608/708) no verificada
   * La compatibilidad con 4K aún no está presente
   * Compatibilidad con etiquetas ID3 no verificada

* Para los eventos de progreso del anuncio, es posible que la barra de tiempo no refleje un tiempo de reproducción del anuncio 100% preciso. Como solución alternativa, se puede usar `adcompleteevent` para conocer la finalización de la reproducción de publicidad y actualizar la interfaz de usuario para diversos fines, como actualizar la barra de tiempo, eliminar la interfaz de usuario relacionada con la publicidad, etc.
* Las grandes llamadas de anuncios que devuelve VMAP no respetan la posición de &quot;Just-In-Time lookforward&quot;.

**Android TVSDK 2.5.6**

* No se admiten varias pausas publicitarias VMAP al mismo tiempo.

**Android TVSDK 2.5.3**

Esta versión tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja o condiciones de red deficientes.
* Para flujos FER, virtualTime y localTime pueden diferir. También FER con desplazamiento no funciona.
* La reproducción puede quedar atascada cuando se busca el contenido de Audio de enlace tardío.
* De forma intermitente, es posible que los subtítulos webVTT no estén sincronizados con el contenido en directo.
* De forma intermitente, se puede ver una reproducción rápida de algunos fotogramas después de salir de una pausa publicitaria.
* A veces, se produce un error 303 en los saltos de publicidad de triple envoltura, aunque se reproduzcan los anuncios.

**Android TVSDK 2.5.2**

Esta versión tiene los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja.
* La reproducción puede bloquearse a veces al buscar hasta el final del medio VOD.
* Para flujos FER, virtualTime y localTime pueden diferir. Además, FER con desplazamiento no funciona.

**Android TVSDK 2.5.1**

Esta versión de TVSDK presenta los siguientes problemas:

* La reproducción de vídeo en directo puede tener problemas de sincronización de audio y vídeo en dispositivos de gama baja.
* Para flujos FER, virtualTime y localTime pueden diferir. Además, FER con desplazamiento no funciona.
* En VMAP XML, si hay una etiqueta VAST vacía sin una etiqueta de cierre explícita (&lt;/VAST>) y sin una nueva línea después de ella, el XML VMAP no se analiza correctamente y es posible que las publicidades no se reproduzcan.
* No se admite el postdesplazamiento VPAID.

## Recursos útiles {#helpful-resources}

* [Requisitos del sistema](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-requirements.html)
* [Guía del programador de TVSDK 3.10 para Android](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-overview-prod-audience-guide.html)
* [Referencia de API para Android Javadoc de TVSDK](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [Documento](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) de API de Android C++ de TVSDK: cada clase de Java tiene una clase C++ correspondiente y la documentación de C++ contiene material más explicativo que los JavaScript, por lo que consulte la documentación de C++ para conocer mejor la API de Java.
* [Guía de migración de TVSDK 1.4 a 2.5 para Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Para controlar los escenarios de activación y desactivación de la pantalla, consulte el archivo `Application_Changes_for_Screen_On_Off.pdf` incluido en la compilación.
* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
