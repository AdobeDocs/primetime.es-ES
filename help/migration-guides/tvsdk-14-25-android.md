---
title: TVSDK 1.4 a 2.5 para Android (Java)
seo-title: TVSDK 1.4 a 2.5 para Android (Java)
description: TVSDK 2.5 oferta varias ventajas con respecto a la versión 1.4 en términos de rendimiento, seguridad, mejores integraciones y más.
seo-description: TVSDK 2.5 oferta varias ventajas con respecto a la versión 1.4 en términos de rendimiento, seguridad, mejores integraciones y más.
uuid: aaab7aec-cb5b-4840-82e8-7112a8d98a8a
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: 8d9136bf-b3ae-450c-bd8a-0bb246527886
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# TVSDK 1.4 a 2.5 para Android (Java) {#tvsdk-to-for-android-java}

TVSDK 2.5 oferta varias ventajas con respecto a la versión 1.4 en términos de rendimiento, seguridad, mejores integraciones y más.

TVSDK resuelve los mayores desafíos, en el dispositivo que más importa. Android continúa su dominio global, con más del 86% de la cuota de mercado. La migración a TVSDK en Android optimizará el rendimiento de la reproducción para mejorar la participación del usuario y acelerar el tiempo de comercialización con compatibilidad con nuevos formatos de contenido.

## Ventajas de migrar a TVSDK v2.5 {#benefits-of-migrating-to-tvsdk-v}

TVSDK 2.5 oferta varias ventajas con respecto a la versión 1.4 en términos de rendimiento, seguridad, mejores integraciones y más. Siga leyendo para conocer rápidamente las ventajas de migrar a esta nueva versión.

Según un estudio de evaluación comparativa de terceros, v2.5 proporciona una reducción de 5 veces en el tiempo de inicio y de 3,8 veces en el promedio de la industria.

| Características de rendimiento | Descripción |
|--- |--- |
| Activado para VOD y Activo | Precargue los segmentos iniciales de ts para la reproducción inmediata para VOD y transmisiones en directo lineales cuando se cambia de canal, para una experiencia similar a la de TV. |
| Carga de anuncios diferida | Reproducción de inicios tan pronto como el anuncio previo o el contenido esté disponible mientras se resuelven los anuncios en versión intermedia en un subproceso paralelo. |
| Conexiones de red persistentes | Aumente la eficiencia y disminuya la latencia del código de red para un rendimiento de reproducción más rápido. |
| Lógica de ABR mejorada | La nueva lógica ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que el ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúe y también optimiza el número de veces que el conmutador de velocidad de bits realmente se produce monitoreando la velocidad a la que cambia la longitud del búfer. |
| Descarga parcial de segmentos | Reproducción de inicios tan pronto como haya suficientes fotogramas de un segmento disponibles para procesar vídeo de forma fiable en el lado del cliente. |
| Descargas paralelas | TVSDK descarga los segmentos de audio y vídeo en paralelo para el contenido desmutado a fin de optimizar el rendimiento de reproducción. |

Las funciones de reproducción mejoran el compromiso del consumidor al ofrecer la experiencia de la retransmisión lineal en formato digital. Además, le ayuda a aprovechar DRM nativo como Widevine para la reproducción en HD.

| Funciones de reproducción | Descripción |
|--- |--- |
| Reproducción de MP4 | No es necesario volver a transcodificar los clips MP4 cortos para reproducirlos en TVSDK. |
| Reproducción de contenido de DASH VOD | Se admiten casos básicos de uso de reproducción de DASH VOD. |
| Ligero juego de trucos con ABR | Compatibilidad con avance rápido y rebobinado en HLS mediante fotogramas clave a velocidades bajas y I-Frames a velocidades más rápidas. Compatibilidad con ABR para todos los marcos admitidos. |

Las funciones son importantes para cumplir con las restricciones del estudio, como la reproducción HD sobre DRM nativo.

| Funciones | Descripción |
|--- |--- |
| Protección de salida basada en resolución | la reproducción se puede restringir únicamente a determinadas resoluciones permitidas por los requisitos de DRM. Disponible solo mediante DRM de Primetime. |
| Amplia compatibilidad | Compatible con flujos de VOD DASH para habilitar casos de uso de DRM nativos. |

La mejora de la facturación directa elimina la necesidad de crear informes manuales para la facturación cada mes. VHL 2.0 permite un tiempo de comercialización más rápido con integración previa a la compilación y una mayor precisión en el seguimiento.

| Funciones | Descripción |
|--- |--- |
| Integración de Moat | Compatibilidad con la medición de la visibilidad de anuncios de Moat. |
| VHL 2.0 | La última integración optimizada de Video Heartbeat Library para la recopilación automática de datos de uso para Adobe Analytics. |
| Compatibilidad con conmutación por error | Se han implementado estrategias adicionales para continuar la reproducción ininterrumpida, a pesar de los fallos de los servidores host, los archivos de listas de reproducción y los segmentos. |
| Integración de facturación directa | Envía métricas de facturación al servidor de Adobe Analytics, certificado por Adobe Primetime para flujos utilizados por clientes. |

>[!NOTE]
>
>Todas las funciones de TVSDK v1.4 son compatibles con v2.5, excepto la compatibilidad con Multi-CDN.

## Visión general del proceso de migración {#overview-of-the-migration-process}

La migración sin problemas de TVSDK 1.4 a 2.5 implica cambiar a bibliotecas de la versión 2.5, volver a compilar y, a continuación, utilizar este documento para ayudar a depurar cualquier problema que se produzca.

Las bibliotecas TVSDK v1.4 no funcionan con bibliotecas v2.5 ni las coexisten con ellas. Debe utilizar bibliotecas v2.5 con TVSDK 2.5 y migrar sus aplicaciones e integraciones para actualizar a TVSDK 2.5. Este documento describe cómo y qué cambiar en el código de la aplicación y cómo solucionar los errores durante la recompilación.

El archivo psdk.jar utiliza bibliotecas de terceros para admitir distintas funciones. Para evitar la eliminación de las bibliotecas, incluya lo siguiente en el archivo `proguard.cfg`:

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

En el archivo `build.gradle`, debe incluir la directiva de compilación para incluir los archivos JAR basados en TVSDK. Si la aplicación incluye Adobe Video Analytics, deberá incluir la directiva de compilación para los tarros adicionales necesarios para la integración de Adobe Video Analytics en la aplicación

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

Este documento no cubre varios cambios menores. Para ver los cambios menores en la API, consulte [TVSDK 2.5 para la API Java de Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html). La referencia correspondiente a la API de C++ tiene descripciones detalladas. Para obtener documentación análoga sobre la API de C++, consulte [TVSDK 2.5 para Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html).

En la implementación de referencia distribuida con el TVSDK se explican varios ejemplos del uso de la API.

## Cambios de API en TVSDK v2.5 {#api-changes-in-tvsdk-v}

Las API nuevas, obsoletas y modificadas se documentan a continuación.

| TVSDK v1.4 | TVSDK v2.5 | Descripción |
|--- |--- |--- |
| import com.adobe.ave.drm.DRMAcquireLicenseSettings | import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; | Todos los nombres de clase de la API de TVSDK 2.5 comienzan con el prefijo com.adobe.mediacore. Este es sólo un ejemplo. |
| MediaPlayerException, IllegalStateException o IllegalArgumentException | MediaPlayerException | En 2.5, las API solo generan MediaPlayerException. |
| MediaPlayer.PlayerState (MediaPlayer.Evento.PLAYBACK) | MediaPlayerStatus (MediaPlayerEvent.STATUS_CHANGED) | En v2.5, se cambió el nombre de MediaPlayer.PlayerState a una enumeración independiente MediaPlayerStatus. |
| DefaultMediaPlayer.create (getActivity().getApplicationContext()) | MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); | Los métodos estáticos utilizados para crear objetos se sustituyen por constructores públicos. |
| MediaPlayer.seekToLocalTime() | MediaPlayer.seekToLocal() | El método MediaPlayer.searchtoLocalTime() ahora se denomina MediaPlayer.searchToLocal(). |
| closedCaptionsTrack.isActive() |  | No disponible |
| MetadataNode | Metadatos | En v2.5, la clase Metadata reemplaza el uso de la clase MetadataNode de v1.4. |
| DefaultMetadataKeys | MetadataKeys | Las claves DefaultMetadataKeys de v1.4 se encuentran en la versión 2.5 enum MetadataKeys. |
| AdvertisingFactory | ContentFactory | AdvertisingFactory de v1.4 se cambia el nombre a ContentFactory en v2.5 |
| PlacementOpportunityDetector | Generador de oportunidades | Los detectores se sustituyen por generadores. |
| mediaPlayer.getView().notificationClick(); | mediaPlayer.notificationClick(); | El método notificationClick() de MediaPlayerView se movió a la clase MediaPlayer. |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, int nMaxBitRate) | public ABRControlParameters(int nInitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate, intMaxTrickPlayBandwidthUsage, doble dMaxPlayout Rate) |  |
| playbackInformation.getTimeToFirstFrame() |  | No disponible |
|  | playInformation.get PerceectedBandwidth() | TVSDK v2.5 QOSProvider tiene una nueva propiedad para determinar el ancho de banda percibido durante una sesión de flujo. |

### Clases eliminadas {#removed-classes}

Las siguientes clases se eliminan y no tienen equivalentes.

* `TimeRangeCollection`
* `PSDKConfig`
* `BaseLogger`
* `DefaultLogger`
* `Log`
* `Logger`
* `LogFactory`
* `NullLogger`

Las seis últimas clases están disponibles como clases de utilidad en la implementación de referencia.

## Cambios de Área de nombres {#namespace-changes}

La API de TVSDK 2.5 consolida Áreas de nombres.

Todos los nombres de clase de la API de TVSDK 2.5 comienzan con el prefijo com.adobe.mediacore. Algunos nombres de clase en el inicio de API de TVSDK 1.4 con com.adobe.ave. Las clases 2.5 correspondientes cambian com.adobe.ave a com.adobe.mediacore. Por ejemplo: observe los cambios en las siguientes líneas de código para 1.4 y 2.5:

```java
// TVSDK 1.4
import com.adobe.ave.drm.DRMAcquireLicenseSettings; import com.adobe.ave.drm.DRMLicense;
import com.adobe.ave.drm.DRMManager; import com.adobe.ave.drm.DRMMetadata
```

```java
// TVSDK 2.5
import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; import com.adobe.mediacore.drm.DRMLicense;
import com.adobe.mediacore.drm.DRMManager; import com.adobe.mediacore.drm.DRMMetadata;
```

## Cambios en la administración de eventos {#changes-in-event-handling}

Para registrar eventos en esta versión, pase el controlador a `addEventListener`. La lista de eventos se ha revisado sustancialmente de la versión 1.4 a la versión 2.5.\
Por ejemplo: a continuación se muestra cómo registrar un controlador de evento para `MediaPlayerEvent.STATUS_CHANGED:`

```java
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,
new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
});
```

Así es como se registró el evento en 1.4:

```java
mPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {
@Override
public void onStateChanged(MediaPlayer.PlayerState state,
MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});
```

La enumeración MediaPlayerEvent contiene todos los códigos de evento. Los siguientes códigos de evento de 1.4 ya no existen en 2.5:

* `ADBREAK_PLACEMENT_COMPLETED`
* `ADBREAK_PLACEMENT_FAILED`
* `ADBREAK_REMOVAL_COMPLETED`
* `AD_BREAK_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_FAILED`
* `AUDIO_TRACK_FAILED`
* `BACKGROUND_MANIFEST_FAILED`
* `BUFFERING_FULL, CUSTOM_AD_EVENT`
* `CONTENT_MARKER`
* `CONTENT_PLACEMENT_COMPLETE`
* `CONTENT_CHANGED`
* `ITEM_REPLACED`
* `ITEM_READY`
* `VIEW_CLICKED`
* `PREPARED`
* `UPDATED`
* `OPPORTUNITY_COMPLETED`
* `OPPORTUNITY_CREATED`
* `OPPORTUNITY_FAILED`
* `PAUSE_AT_PERIOD_END`
* `PLAYBACK_STARTED`
* `PLAYBACK_PAUSED`
* `PLAYBACK_COMPLETED`
* `PLAY_COMPLETE`
* `POST_ROLL_COMPLETE`
* `RESOURCE_LOADED`
* `TIMED_METADATA_SKIPPED`
* `VIDEO_ERROR`
* `VIDEO_STATE_CHANGED`

Los siguientes códigos de evento son nuevos en 2.5:

* `AD_RESOLUTION_COMPLETE`
* `BUFFER_PREPARED`
* `CAPTIONS_UPDATED`
* `MANIFEST_UPDATED`
* `PLAYBACK_RANGE_UPDATED`
* `RESERVATION_REACHED`
* `TIME_CHANGED`
* `TIMED_EVENT`
* `TIMED_METADATA_ADDED_IN_BACKGROUND`

### Se cambió el nombre de los Eventos {#renamed-events}

| Nuevo nombre | Nombre antiguo |
|--- |--- |
| SEEK_BEGIN | SEEK_STARTED |
| SEEK_END | SEEK_COMPLETED |
| SEEK_POSITION_ADJUSTED | SEEK_ADJUST_COMPLETED |
| BUFFERING_BEGIN | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATUS_CHANGED | STATE_CHANGED |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_AÑADIDO |
| SIZE_AVAILABLE | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## Cambios de MediaPlayer {#mediaplayer-changes}

Una nueva forma de construir `MediaPlayer` y cambiar algunos de los métodos.

**Cambios en la clase MediaPlayer**

Estos son los cambios realizados en la clase `MediaPlayer`:

* La enumeración `MediaPlayerStatus` reemplaza a `MediaPlayer.PlayerState`. Por ejemplo:

```java
//TVSDK v1.4
mPlayer. addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {

@Override
public void onStateChanged(MediaPlayer.PlayerState state,MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});

//TVSDK v2.5
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
//Additional handlers.
...
});
```

* El método `MediaPlayer.seekToLocalTime()` ahora se denomina `MediaPlayer.seekToLocal`. Por ejemplo:

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* El método `MediaPlayerView.notifyClick()` ahora es `MediaPlayer.notifyClick()`. Por ejemplo:

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* El método anterior `MediaPlayer.MediaPlayer.getNotificationHistory()` ha desaparecido y no se ha reemplazado.
* El `MediaPlayer.replaceCurrentItem()` anterior se divide en dos métodos: `replaceCurrentResource()`, que toma una instancia de `MediaResource` y `replaceCurrentItem()`, que toma una instancia de `MediaPlayerItem`. Por ejemplo:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());

mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5 - replacing a resource
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());
...
try {
mMediaPlayer.replaceCurrentResource(playerResource, _mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
// TVSDK 2.5 - replacing an Item
MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(context, new MediaPlayerItemLoader.LoaderListener() {

@Override
public void onError(PSDKErrorCode psdkErrorCode, String s) {
...
}
@Override
public void onLoadComplete(MediaPlayerItem mediaPlayerItem) {
...
}
@Override
public void onBufferingBegin() {
...
}
@Override
public void onBufferPrepared() {
...
}
});
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());

itemLoader.load(playerResource); itemLoader.prepareBuffer();
mediaPlayer.replaceCurrentItem(itemLoader.getItem());
```

Puede utilizarlo para cambiar entre instancias de MediaPlayer preinicializadas, como en el caso de apagones.

**Los constructores reemplazan los métodos estáticos create()**

Puede utilizar constructores en TVSDK v2.5, en lugar de utilizar métodos `create()` de TVSDK v1.4. Todas las clases con nombres que comienzan por Predeterminado, como `DefaultMediaPlayer`, `DefaultNetworkConfig`, `DefaultContentFactory`, no están disponibles en v2.5.

En algunos casos, la API de TVSDK v1.4 utiliza el siguiente patrón para crear clases:

1. Defina una interfaz (por ejemplo, `MediaPlayer`).
1. Proporcione una clase predeterminada (por ejemplo, `DefaultMediaPlayer`).
1. Proporcione un método `create()` en la clase predeterminada para proporcionar una clase que implemente la interfaz.

En TVSDK v2.5, estas interfaces son clases concretas y se crean instancias de estas clases mediante los constructores respectivos. Los siguientes fragmentos de código ilustran esta diferencia:

```java
//TVSDK v1.4
// Create a media player
// MediaPlayer is an interface
private MediaPlayer createMediaPlayer() { MediaPlayer mediaPlayer =
DefaultMediaPlayer.create(getActivity().getApplicationContext()); return mediaPlayer;

//TVSDK v2.5
// Create a media player
// MediaPlayer is a class that you instantiate private MediaPlayer createMediaPlayer() {
MediaPlayer mediaPlayer =
new MediaPlayer(getActivity().getApplicationContext()); return mediaPlayer;
}
```

Otras clases que no siguen este patrón pero utilizan métodos `create()` en 1.4 incluyen:

* MediaResource\
   Anteriormente se usaba `MediaResource.createFromUrl()`. Ahora utilice el constructor, que toma una URL, un tipo de recurso y metadatos. Por ejemplo:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());
mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, getAdvertisingMetadata());

try { mediaPlayer.replaceCurrentResource(playerResource,_mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
```

* Publicidad
* AdAsset
* AdBreak

Algunas clases (por ejemplo, `ContentFactory`) son clases abstractas sin una implementación predeterminada disponible públicamente (por ejemplo, `DefaultContentFactory`). En estos casos, puede proporcionar una implementación predeterminada mediante una función de conveniencia, por ejemplo: `mediaPlayerItemConfig.getDefaultContentFactory()`

**Cambios en los subtítulos opcionales**

Los siguientes cambios afectan a las clases relacionadas con los subtítulos opcionales:

* Al recuperar las pistas de subtítulos cerrados, `MediaPlayerItem.getClosedCaptionTracks()` solo devuelve las pistas activas.
* `ClosedCaptionTrack` ya no tiene un  `isActive()` método.

```java
//TVSDK v1.4
public List<String> getClosedCaptionTracks(String label) {
List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks(); Iterator<ClosedCaptionsTrack> iterator =
closedCaptionsTracks.iterator();
if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); String isActive = closedCaptionsTrack.isActive() ? " (" + label
+ ")" : "";
closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName()
+ " : " + closedCaptionsTrack.getLanguage() + isActive);
}
}
return closedCaptionsTracksAsStrings;
}

//TVSDK v2.5
public List<String> getClosedCaptionTracks(String label) {

MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks();
Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator();

List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); closedCaptionsTracksAsStrings.
add(closedCaptionsTrack.getName() + " : ");
}
}
return closedCaptionsTracksAsStrings;
}
// Add snippet and desc for CaptionsUpdatedEventListener mediaPlayer.addEventListener(MediaPlayerEvent.CAPTIONS_UPDATED,
captionsUpdatedEventListener);

private final CaptionsUpdatedEventListener captionsUpdatedEventListener = new CaptionsUpdatedEventListener() {

@Override
public void onCaptionsUpdated(MediaPlayerItemEvent mediaPlayerItemEvent) { getActivity().findViewById(R.id.sbPlayerControlCC).setVisibility(
View.VISIBLE/*Visible*/);
}
};
```

## Cambios en la publicidad {#advertising-changes}

Hay varios cambios relacionados con la publicidad en la versión 2.5.

**Cambios en el comportamiento de la publicidad**

El comportamiento predeterminado de la reproducción del anuncio cuando un usuario realiza una búsqueda más allá de un pod de publicidad cambia ligeramente en la versión 2.5. Si no se observa la pausa publicitaria, la publicidad se reproduce después de una búsqueda hacia delante. Cuando la aplicación utiliza la directiva de publicidad predeterminada, la pausa publicitaria se elimina una vez finalizada la reproducción. Con TVSDK v2.5, si un usuario busca detrás de un pod de publicidad en la línea de tiempo y no se observa la pausa publicitaria, no se reproduce ningún anuncio.

Sin embargo, en TVSDK v1.4, de forma predeterminada, se reproduce un anuncio en caso de una búsqueda hacia atrás. Por ejemplo, si busca hacia atrás entre la tercera y la cuarta pausa publicitaria, el comportamiento predeterminado de TVSDK v1.4 es reproducir la tercera pausa publicitaria.

**Cambio de las reglas de publicidad**

Las reglas de publicidad se especifican mediante un archivo JSON. El formato del archivo JSON sigue siendo el mismo en ambas versiones del TVSDK. Sin embargo, en TVSDK v2.5, el archivo JSON de reglas de publicidad debe alojarse en una ubicación accesible mediante una URL HTTP. La aplicación puede utilizar una instancia de AuditudeSettings.

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

En la versión 1.4 de TVSDK, este archivo se coloca debajo de la carpeta assets en la aplicación y TVSDK carga el archivo.

**Cambio de nombre de fábrica de publicidad**

`AdvertisingFactory` ahora se denomina  `ContentFactory`. Con `ContentFactory` puede crear flujos de trabajo publicitarios personalizados anulando algunos de sus métodos. Use return null para mantener los comportamientos predeterminados, como se muestra a continuación:

```java
//TVSDK v2.5
new ContentFactory() {
@Override
public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item) { return new CustomAdPolicySelector();
}
@Override
public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { return null;
}
@Override
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { return null;
}
@Override
public List<CustomAdHandler> retrieveCustomAdPlaybackHandlers(MediaPlayerItem item) { return null;
}
};
```

**Saltos de publicidad de longitud cero**

TVSDK 2.5 inserta saltos de publicidad de longitud cero como marcadores de posición cuando el servidor de publicidad no devuelve anuncios.

Los saltos de publicidad de longitud cero se pueden determinar detectando que el recuento de publicidades sea cero en la pausa publicitaria mediante el evento onAdBreakStarted y que la aplicación debe gestionar estos saltos de publicidad en consecuencia.

**Cambios en los metadatos**

La clase Metadata proporciona un reemplazo más capaz de la antigua clase MetadataNode.

* La clase Metadata puede almacenar cadenas, conjuntos de bytes y otros objetos de metadatos:

```java
TVSDK v1.4
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new MetadataNode();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingParameters(advertisingParams);

return adSettings;
}
//TVSDK v2.5
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new Metadata();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingInfo(advertisingParams);

return adSettings;
}
```

* La enumeración `MetadataKeys` reemplaza a `DefaultMetadataKeys`. No todas las claves de `DefaultMetadataKeys` están presentes en la nueva versión.

```java
//TVSDK v1.4
if (this.mediaPlayer != null && this.mediaPlayer.getCurrentItem() != null) { MetadataNode resourceMetadata =
(MetadataNode) this.mediaPlayer.getCurrentItem().getResource().getMetadata();
VideoAnalyticsMetadata vaMetadata = (VideoAnalyticsMetadata)
resourceMetadata.getNode(DefaultMetadataKeys.
VIDEO_ANALYTICS_METADATA_KEY.getValue());
}

//TVSDK v2.5
if (resourceMetadata.containsKey(VideoAnalyticsMetadata.
VIDEO_ANALYTICS_METADATA_KEY)) {
JSONObject vaMetadataObj =
new JSONObject(resourceMetadata.
getValue(VideoAnalyticsMetadata. VIDEO_ANALYTICS_METADATA_KEY));
vaMetadata = parseVideoAnalyticsMetadata(vaMetadataObj);
}

} catch (JSONException e) { e.printStackTrace();
}
```

* Los metadatos de publicidad ahora están representados por la clase `AdvertisingMetadata`, una subclase de metadatos, y ahora se almacenan en `MediaPlayerItemConfig` en lugar de `MediaResource`.

```java
//TVSDK v1.4
MetadataNode mediaMetadata = new MetadataNode();

if (stream.live) { mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(),
getAdSettingsForLive());
} else {
mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(), getAdSettingsForVod());
}
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

if (stream.live) {
AuditudeSettings adSettings = getAdSettingsForLive(); adSettings.setLivePreroll(true); mediaItemConfig.setAdvertisingMetadata(adSettings);
} else {
// Set the advertising parameters for VOD. mediaItemConfig.setAdvertisingMetadata(getAuditudeSettingsForVod());
}

// Create advertising metadata node Metadata mediaMetadata = new Metadata();

// Asset Url
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, mediaMetadata);
try {
mediaPlayer.replaceCurrentResource(playerResource, mItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
//handle exception.
}
```

Los metadatos de configuración de red, anteriormente miembros de la clase `MediaResource`, ahora están representados por la clase `NetworkConfiguration` y ahora se almacenan en `MediaPlayerItemConfig` en lugar de `MediaResource`.

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**Cambios en el análisis de TimedMetadata**

El análisis de `TimedMetadata` ha cambiado en 2.5 con respecto a los tipos de datos para analizar la etiqueta ID3.

```java
//TVSDK v1.4
public void onTimedMetadata(TimedMetadata timedMetadata) { TimedMetadata.Type type = timedMetadata.getType();
if (type.equals(TimedMetadata.Type.ID3)){ PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata(); Set<String> keys = metadata.keySet();
for (String key : keys) {
String value = metadata.getValue(key); PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"Key = " + key + " Value = " + value);
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { parseSCTE35Tag(timedMetadata);
}
}
}

//TVSDK v2.5
public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { PMPDemoApp.logger.i(LOG_TAG + " inside"," ontimedmetadata"); TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata();

TimedMetadata.Type type = timedMetadata.getType(); if (type.equals(TimedMetadata.Type.ID3)) {
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata();
if (metadata != null) { PMPDemoApp.logger.i(LOG_TAG +
"::expandID3Metadata", "isEmpty " + metadata.isEmpty());
Set<String> keys = metadata.keySet(); PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"No of keys=" + keys.size());
String s;
for (String key : keys) {
byte[] value = metadata.getByteArray(key); s = new String(value);
if (key.equalsIgnoreCase("APIC"))
s = "SUPPRESSING BINARY DATA FOR ATTACHED PICTURE.";
PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"Key=" + key + ", Length=" + value.length + ", Value=" + s.trim());
}
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { PMPDemoApp.logger.i(LOG_TAG +
" inside ontimedmetadata"," ext"); parseSCTE35Tag(timedMetadata);
}
}
}
```

**Otros cambios**

Los siguientes cambios adicionales están disponibles en la versión 2.5:

* El método `notifyClick()` se ha movido de `MediaPlayerView` a `MediaPlayer`.

* `AdPolicySelector` es una interfaz, no una clase. Implementar todos sus métodos.
* `AdPolicyInfo` ahora contiene una lista de  `AdBreakTimelineItem`, no de  `AdBreakPlacement`.

* Se cambia el nombre de la API de la clase abstracta `ContentResolver`.
* `PlacementOpportunityDetector` ya no está disponible. En su lugar, extienda la clase abstracta `OpportunityGenerator`. La implementación de referencia proporciona un ejemplo de esto.

* Los parámetros del constructor `AdBreakPlacement` son los mismos, pero en un orden diferente. Para obtener una implementación de muestra, consulte la implementación de Reference Player incluida con el producto.

## Cambios en DRM {#changes-in-drm}

La mayoría de los cambios de esta versión se encuentran en la capa DRM. La siguiente tabla muestra los cambios adicionales entre las versiones 1.4 y 2.5:

| DRMManager (método) | Llamada de retorno correcta en 1.4 | Llamada de retorno de error en 1.4 | Listener en 2.5 |
|--- |--- |--- |--- |
| acquisitionLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| acquisitionPreviewLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| autenticar | DRMAuthauthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | NA | DRMOperationErrorCallback | DRMErrorListener |
| initialize | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leftLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| resetDRM | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| returnLicense | DRMLicenseReturnCompleteCallback | DRMOperationErrorCallback | DRMReturnLicenseListener |
| setAuthenticationToken | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| storeLicenseBytes | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |

```java
//TVSDK 1.4
private final MediaPlayer.DRMEventListener _drmEventListener = new MediaPlayer.DRMEventListener() {

@Override
public void onDRMMetadata(final DRMMetadataInfo drmMetadataInfo) { PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata available
// event and the play event, so launch the metadata interface
// and give it the loaded metadata bytes, but only once
_drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo == null ||
!DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG + "#onDRMMetadata", "DRM auth is not needed."); return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold
// between the current player time and the DRM metadata start
// time. For the time being, we resolve it as soon as we receive
// the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG + "#onDRMMetadata", "DRMManager is null."); return;
}
SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity()); String authUser =
sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG + "#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(long majorCode,
long minorCode, Exception e) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + majorCode + " 0x" + Long.toHexString(minorCode));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};

//TVSDK 2.5
private final DRMMetadataInfoEventListener drmMetadataInfoEventListener = new DRMMetadataInfoEventListener() {
@Override
public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { final DRMMetadataInfo drmMetadataInfo =
drmMetadataInfoEvent.getDRMMetadataInfo();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata
// available event and the play event, so launch the
// metadata interface and give it the loaded metadata
// bytes, but only once
drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo ==
null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG +
"#onDRMMetadata",
"DRM auth is not needed.");
return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold between
// the current player time and the DRM metadata start time. For the
// time being, we resolve it as soon as we receive the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG +
"#onDRMMetadata", "DRMManager is null.");
return;
}

SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity());
String authUser = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(int major,
int minor,
String erroString, String serverErrorURL) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + major +
" 0x" +
Long.toHexString(minor));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};
```

La instancia estática `DRMManager` que estaba disponible en 1.4 después de crear el mediaplayer ahora está disponible después de activar el detector de evento `onDRMMetadataInfo`.

## Cambios relacionados con la velocidad de bits adaptable (ABR) {#adaptive-bitrate-abr-related-changes}

**Cambios en constantes**

Muchas constantes han cambiado el tipo de `String` a `int`. Por ejemplo: `MediaResourceType`, `ABRControlParameters` y `MediaPlayerStatusChangeEvent`.

```java
//TVSDK v1.4
ABRControlParameters
private void setAbrControlParams() { SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity());
if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED,
PMPDemoApp.DEFAULT_ABR_ENABLED)) {
int initialBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE, 0);
int minBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE, 0);
int maxBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE, PMPDemoApp.DEFAULT_MAX_BIT_RATE);
int mbrPolicyAsInt =
getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, 0); ABRControlParameters.ABRPolicy abrPolicy = policyFromInt(mbrPolicyAsInt); abrPolicy = abrPolicy != null ?
abrPolicy : ABRControlParameters.ABRPolicy.ABR_MODERATE;
_mediaPlayer.setABRControlParameters(new ABRControlParameters(initialBitRate,
minBitRate, maxBitRate, abrPolicy));
}
}

//TVSDK v2.5
ABRControlParameters
private void setAbrControlParams() { ABRControlParametersBuilder abrBuilder =
new ABRControlParametersBuilder();

if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED, PMPDemoApp.DEFAULT_ABR_ENABLED)) {

abrBuilder.setInitialBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE,
ABRControlParameters.DEFAULT_ABR_INITIAL_BITRATE)); abrBuilder.setMinBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxPlayoutRate(getDoublePreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_PLAYOUT_RATE,
ABRControlParameters.DEFAULT_MAX_PLAYOUT_RATE)); abrBuilder.setMinTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxTrickPlayBandwidthUsage(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BANDWIDTH,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE));

switch (getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, -1)) {
case 0: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_CONSERVATIVE); break;
case 1: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_MODERATE); break;
case 2: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_AGGRESSIVE); break;
default: abrBuilder.setPolicy(ABRControlParameters.DEFAULT_ABR_POLICY);
}
}
_mediaPlayer.setABRControlParameters(abrBuilder.toABRControlParameters());
}
```

**Cambios en el constructor ABRControlParameters**

Se han agregado algunos parámetros, se ha cambiado el nombre de algunos y se han movido algunos. A continuación se muestra la firma del constructor en la versión 1.4 y la nueva firma en la versión 2.5:

```java
//TVSDK v1.4
public ABRControlParameters(ABRPolicy abrPolicy,
int nInitialBitRate, int nMinBitRate,
int nMaxBitRate)

//TVSDK v2.5
public ABRControlParameters(int nInitialBitRate,
int nMinBitRate, int nMaxBitRate,
ABRPolicy abrPolicy,
int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate,
int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate)
```

## Eventos de error y administración {#error-events-and-handling}

**Cambios en la gestión de errores**

La clase `MediaError` se reemplazó por la clase `Notification`. La única diferencia entre las clases `MediaError` y `Notification` es que esta última no contiene un atributo description. Los códigos de error TVSDK 1.4 con los valores 101xxx, 102xxx,104xxx,106xxx,107xxx,109xxx no existen en TVSDK 2.5. Para ver los códigos de reproducción en TVSDK 2.5, consulte [Error nativo- valores de reproducción de vídeo](assets/psdk_android_2.5.pdf).

Los siguientes son ejemplos de gestión de errores en TVSDK 1.4 y 2.5:

```java
//TVSDK v1.4
@Override
public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");

switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR: PMPDemoApp.logger.e(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: " + notification + "."); getActivity().finish();
break;
default:
// do nothing
}
}

//TVSDK v2.5
private final StatusChangeEventListener statusChangeEventListener = new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent mediaPlayerStatusChangeEvent)
{
MediaPlayerStatus state = mediaPlayerStatusChangeEvent.getStatus(); PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");
switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR:
PMPDemoApp.logger.e(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: ");
printErrorMetadata(mediaPlayerStatusChangeEvent.getMetadata()); showToast("MediaPlayer status ERROR: Look at the logs for details"); getActivity().finish();
break;
default:
// do nothing
}
}
};
```

Todos los errores recuperables se tratan como advertencias y se gestionan mediante el `NotificationEventListener` en TVSDK 2.5. Las advertencias aparecen como notificaciones con el detector `onOperationFailed` en el controlador QOS de TVSDK 1.4, donde, como en TVSDK 2.5, la notificación es un evento independiente. La advertencia tratada en 1.4 y 2.5 es la siguiente:

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener()
{
@Override
public void onBufferStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
}
@Override
public void onBufferComplete() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
}
@Override
public void onSeekStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
}
@Override
public void onSeekComplete(long adjustedTime) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
}
@Override
public void onLoadInfo(LoadInfo loadInfo) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize() + " bytes, media duration: " + loadInfo.getMediaDuration() + "ms, download duration: " + loadInfo.getDownloadDuration() + "ms");
}
@Override
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - ").append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append

//TVSDK v2.5
private final NotificationEventListener notificationEventListener = new NotificationEventListener() {
/**
* An example of dumping the information within a Notification. Here, we don't handle the event in
* any way except to print a log message.
* @param event The NotificationEvent
*/
@Override
public void onNotification(NotificationEvent event) { Notification notification = event.getNotification(); Notification.Type type = notification.getType(); StringBuilder sb = new StringBuilder(); sb.append("[").append(type).append("]");
sb.append(" Player operation failed (").append(notification.getCode()).append(")"); Metadata metadata = notification.getMetadata();
if (metadata != null)
{
for (String key : metadata.keySet())
{
sb.append(", ").append(key).append(" = ").append(metadata.getValue(key));
}
}
Notification inner = notification.getInnerNotification(); if (inner != null) {
sb.append(" :: Inner Notification [").append(inner.getType()).append("](").append(inner.getCode()).append(")");
Metadata innerMetadata = inner.getMetadata(); if (innerMetadata != null) {
for (String iKey : innerMetadata.keySet()) { sb.append(", ").append(iKey).append(" =
").append(innerMetadata.getValue(iKey));
}
}
}
switch(type)
{
case ERROR:
PMPDemoApp.logger.e(LOG_TAG, sb.toString()); break;
case WARNING:
PMPDemoApp.logger.w(LOG_TAG, sb.toString()); break;
default:
PMPDemoApp.logger.i(LOG_TAG, sb.toString()); break;
}
showToast(sb.toString()); PMPDemoApp.logger.d(LOG_TAG, sb.toString());
}
};
```

**Nuevas excepciones**

Mientras que TVSDK v1.4 utilizó una combinación de números, devuelve un error y una variedad de excepciones ( `MediaPlayerException`, `IllegalStateException` y `IllegalArgumentException`), TVSDK v2.5 `generatesMediaPlayerException` para todos los errores.

>[!NOTE]
>
>Para obtener detalles sobre una excepción MediaPlayerException, puede utilizar `getErrorCode()`.

A continuación se muestra un ejemplo del cambio:

```java
//TVSDK v1.4
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (IllegalArgumentException e) { PrimetimeReference.logger.w(LOG_TAG +
"#setBufferControlParams",
"Unable to apply buffering params: " + e.getMessage() + ".");
}
}

//TVSDK v2.5
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (MediaPlayerException e) { PrimetimeReference.logger.w(LOG_TAG + "#setBufferControlParams", "Unable to apply buffering params: " + e.getMessage() + ".");
}
}
```

## Cambios en los parámetros de QOS {#changes-to-qos-parameters}

Hay cambios menores en las propiedades del objeto QOSProvider:

* El `TimeToFirstFrame` no está disponible en TVSDK 2.5.
* TVSDK 2.5 QOSProvider tiene una nueva propiedad para determinar el ancho de banda percibido durante una sesión de flujo.

```java
//TVSDK v1.4
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitrate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); setQosItem("Time to first frame", (int) playbackInformation.getTimeToFirstFrame()); setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); setQosItem("Last seek time", (int) playbackInformation.getLastSeekTime());
}

//TVSDK v2.5
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitRate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart());
setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare());
setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());
```

* El `QOSEventListener::onOperationFailed()` ya no existe en TVSDK 2.5. Las advertencias que solían aparecer en este detector de evento ahora aparecerán en el detector de evento `NotificationEventListener::onNotification()`.

* Los `QOSProvider event listeners onBufferStart()`, `onBufferComplete()`, `onSeekStart()`, `onSeekComplete()` y `onLoadInfo()` son detectores de evento individuales enlazados con una instancia de mediaPlayer.

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener() {

@Override
public void onBufferStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
@Override
public void onBufferComplete() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
hideBufferingSpinner();
}
@Override
public void onSeekStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
@Override
public void onSeekComplete(long adjustedTime) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " +
adjustedTime + ".");
_controlBar.setPosition(adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayer.PlayerState.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
@Override
public void onLoadInfo(LoadInfo loadInfo) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " +
loadInfo.getUrl() + ", size: " + loadInfo.getSize() +
" bytes, media duration: " +
loadInfo.getMediaDuration() + "ms, download duration: " +
loadInfo.getDownloadDuration() + "ms");
 
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - "). append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append(key).append(": ").
append(metadata.getValue(key));
}
}
innerNotification = innerNotification.getInnerNotification();
}
String errMsg = sb.toString(); PMPDemoApp.logger.w(LOG_TAG +
"::MediaPlayer.QOSEventListener#onOperationFailed()", errMsg);
showToast(errMsg);
}
};

//TVSDK v2.5
mediaPlayer.addEventListener(MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE,
loadInfoEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_BEGIN,
bufferingBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_END,
bufferingEndEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_BEGIN,
seekBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_END,
seekEndEventListener);
// Buffering events.
BufferingBeginEventListener bufferingBeginEventListener = new BufferingBeginEventListener() {
@Override
public void onBufferingBegin(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
};

BufferingEndEventListener bufferingEndEventListener = new BufferingEndEventListener() {
@Override
public void onBufferingEnd(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()",
"Buffering complete."); hideBufferingSpinner();
}
};

BufferPreparedEventListener bufferPreparedEventListener = new BufferPreparedEventListener() {
@Override
public void onBufferPrepared() {
}
};
// seek events.
SeekBeginEventListener seekBeginEventListener = new SeekBeginEventListener() {

@Override
public void onSeekBegin(SeekEvent seekEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
};
SeekEndEventListener seekEndEventListener = new SeekEndEventListener() {
@Override
public void onSeekEnd(SeekEvent seekEvent) {
double adjustedTime = seekEvent.getActualPosition();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
_controlBar.setPosition((long) adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayerStatus.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
};
/**
* LoadInformationEventListener that intercepts PSDK load info events
*/
private final LoadInformationEventListener loadInfoEventListener = new LoadInformationEventListener() {

@Override
public void onLoadInformation(LoadInformationEvent event) { LoadInformation loadInfo = event.getLoadInfomation(); PMPDemoApp.logger.i(
LOG_TAG + "::LoadInformationEventListener#onLoadInfomation()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize()
+ " bytes, download duration: "
+ loadInfo.getDownloadDuration() + "ms");
}
};
```

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Información y soporte de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).