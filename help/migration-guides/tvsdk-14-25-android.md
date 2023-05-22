---
title: TVSDK 1.4 a 2.5 para Android (Java)
description: TVSDK 2.5 ofrece múltiples ventajas con respecto a la versión 1.4 en términos de rendimiento, seguridad, mejores integraciones y mucho más.
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
exl-id: 3b7f8355-ebea-4322-aef4-5393308391b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# TVSDK 1.4 a 2.5 para Android (Java) {#tvsdk-to-for-android-java}

TVSDK 2.5 ofrece múltiples ventajas con respecto a la versión 1.4 en términos de rendimiento, seguridad, mejores integraciones y mucho más.

TVSDK resuelve los mayores desafíos, en el dispositivo que más importan. Android continúa su dominio global, con más del 86% de cuota de mercado. La migración a TVSDK en Android optimizará el rendimiento de reproducción para mejorar la participación del usuario y acelerar el tiempo de comercialización con compatibilidad con nuevos formatos de contenido.

## Ventajas de migrar a TVSDK v2.5 {#benefits-of-migrating-to-tvsdk-v}

TVSDK 2.5 ofrece múltiples ventajas con respecto a la versión 1.4 en términos de rendimiento, seguridad, mejores integraciones y mucho más. Siga leyendo para conocer rápidamente las ventajas de migrar a esta nueva versión.

Según un estudio de evaluación comparativa de terceros, v2.5 proporciona una reducción de 5 veces en el tiempo de inicio y de 3,8 veces en los fotogramas perdidos sobre el promedio de la industria.

| Funciones de rendimiento | Descripción |
|--- |--- |
| Instant-on para VOD y Live | Precargar sus segmentos iniciales para reproducción inmediata para emisiones lineales de VOD y en directo al cambiar de canal, para una experiencia similar a la de un televisor. |
| Carga diferida de publicidad | Inicia la reproducción en cuanto el contenido o el anuncio previo a la emisión están disponibles mientras se resuelven los anuncios durante la emisión en un hilo paralelo. |
| Conexiones de red persistentes | Aumente la eficacia y disminuya la latencia del código de red para obtener un rendimiento de reproducción más rápido. |
| Lógica ABR mejorada | La nueva lógica ABR se basa en la longitud del búfer, la velocidad de cambio de la longitud del búfer y el ancho de banda medido. Esto garantiza que ABR elija la velocidad de bits correcta cuando el ancho de banda fluctúa y también optimiza el número de veces que el conmutador de velocidad de bits realmente se produce al monitorizar la velocidad a la que cambia la longitud del búfer. |
| Descarga parcial de segmentos | Inicia la reproducción en cuanto hay suficientes fotogramas de un segmento disponibles para procesar el vídeo de forma fiable en el lado del cliente. |
| Descargas paralelas | TVSDK descarga segmentos de audio y vídeo en paralelo para contenido demuxado a fin de optimizar el rendimiento de reproducción. |

Las funciones de reproducción mejoran la participación del consumidor al ofrecer la experiencia de difusión lineal en digital. Además, le ayuda a aprovechar la DRM nativa, como Widevine, para la reproducción en HD.

| Funciones de reproducción | Descripción |
|--- |--- |
| Reproducción de MP4 | Los clips cortos MP4 no tienen que volver a transcodificarse para su reproducción en TVSDK. |
| Reproducción de contenido de DASH VOD | Se admiten casos prácticos de reproducción básica de DASH VOD. |
| Smooth Trickplay con ABR | Compatibilidad para avanzar y rebobinar rápidamente en HLS mediante fotogramas clave a velocidades bajas e I-Frames a velocidades más rápidas. Compatibilidad con ABR para todos los fotogramas admitidos. |

Las funciones son importantes para cumplir con las restricciones del estudio, como la reproducción en HD con respecto a la DRM nativa.

| Funciones | Descripción |
|--- |--- |
| Protección de salida basada en resolución | La reproducción solo puede restringirse a determinadas resoluciones permitidas por los requisitos de DRM. Disponible solo a través de DRM de Primetime. |
| Soporte de Widevine | Compatible con flujos de VOD DASH para habilitar casos de uso nativos de DRM. |

La mejora de la facturación directa elimina la necesidad de crear informes manuales para la facturación todos los meses. VHL 2.0 permite un tiempo de comercialización más rápido con la integración previa a la compilación y una mejor precisión en el seguimiento.

| Funciones | Descripción |
|--- |--- |
| Integración de foso | Compatibilidad con la medición de la visibilidad de anuncios de Moat. |
| VHL 2.0 | La integración de la biblioteca de latidos de vídeo más reciente y optimizada para la recopilación automática de datos de uso para Adobe Analytics. |
| Compatibilidad con failover | Estrategias adicionales implementadas para continuar la reproducción ininterrumpida, a pesar de los errores de los servidores host, los archivos de lista de reproducción y los segmentos. |
| Integración de facturación directa | Envía métricas de facturación al backend de Adobe Analytics, que cuenta con la certificación de Adobe Primetime para los flujos que utilizan los clientes. |

>[!NOTE]
>
>Todas las funciones de TVSDK v1.4 son compatibles con la versión 2.5, excepto la compatibilidad con Multi-CDN.

## Información general sobre el proceso de migración {#overview-of-the-migration-process}

La migración sin problemas de TVSDK 1.4 a 2.5 implica cambiar a las bibliotecas de la versión 2.5, volver a compilar y, a continuación, utilizar este documento para depurar cualquier problema que se produzca.

Las bibliotecas de TVSDK v1.4 no funcionan con las bibliotecas v2.5 y coexisten con ellas. Debe utilizar las bibliotecas v2.5 con TVSDK 2.5 y migrar sus aplicaciones e integraciones para actualizar a TVSDK 2.5. Este documento describe cómo y qué cambiar en el código de la aplicación y cómo corregir errores durante la recompilación.

El archivo psdk.jar utiliza bibliotecas de terceros para admitir diferentes funciones. Para evitar la eliminación de las bibliotecas, incluya lo siguiente en la `proguard.cfg` archivo:

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

En el `build.gradle` , debe incluir la directiva de compilación para incluir los archivos JAR basados en TVSDK. Si su aplicación incluye Adobe Video Analytics, debe incluir la directiva de compilación para los archivos .jar adicionales necesarios para la integración de Adobe Video Analytics en la aplicación

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

En este documento no se tratan varios cambios menores. Para ver los cambios menores en la API, consulte [TVSDK 2.5 para la API de Java de Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html). La referencia de la API de C++ correspondiente tiene descripciones detalladas. Para obtener documentación análoga de la API de C++, consulte [API de TVSDK 2.5 para Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html).

En la implementación de referencia distribuida con el TVSDK se describen varios ejemplos del uso de API.

## Cambios de la API en TVSDK v2.5 {#api-changes-in-tvsdk-v}

Las API nuevas, obsoletas y modificadas se documentan a continuación.

| TVSDK v1.4 | TVSDK v2.5 | Descripción |
|--- |--- |--- |
| import com.adobe.ave.drm .DRMAcquireLicenseSettings | import com.adobe.mediacore.drm .DRMAcquireLicenseSettings; | Todos los nombres de clase de la API de TVSDK 2.5 comienzan con el prefijo com.adobe.mediacore. Esto es solo un ejemplo. |
| MediaPlayerException, IllegalStateException o IllegalArgumentException | MediaPlayerException | En la versión 2.5, las API solo generan MediaPlayerException. |
| MediaPlayer.PlayerState (MediaPlayer.Event.PLAYBACK) | MediaPlayerStatus (MediaPlayerEvent.STATUS_CHANGED) | En la versión 2.5, se cambió el nombre de MediaPlayer.PlayerState a una enumeración independiente MediaPlayerStatus. |
| DefaultMediaPlayer.create (getActivity().getApplicationContext()) | MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext(); | Los métodos estáticos utilizados para crear objetos se sustituyen por constructores públicos. |
| MediaPlayer.seekToLocalTime() | MediaPlayer.seekToLocal() | El método MediaPlayer.seekToLocalTime() ahora se llama MediaPlayer.seekToLocal(). |
| closedCaptionsTrack.isActive() |  | No disponible |
| MetadataNode | Metadatos | En la versión 2.5, la clase Metadata reemplaza el uso de la clase MetadataNode de la versión 1.4. |
| DefaultMetadataKeys | MetadataKeys | Las MetadataKeys predeterminadas de la versión 1.4 están en MetadataKeys de enumeración de la versión 2.5. |
| AdvertisingFactory | ContentFactory | Se cambia el nombre de AdvertisingFactory de v1.4 a ContentFactory en v2.5 |
| PlacementOpportunityDetector | OpportunityGenerator | Los detectores se sustituyen por generadores. |
| mediaPlayer.getView().notifyClick(); | mediaPlayer.notifyClick(); | El método notifyClick() de MediaPlayerView se ha movido a la clase MediaPlayer. |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, int nMaxBitRate) | public ABRControlParameters(int nInitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate, int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate) |  |
| playbackInformation.getTimeToFirstFrame() |  | No disponible |
|  | playbackInformation.get PerceptedBandwidth() | TVSDK v2.5 QOSProvider tiene una nueva propiedad para determinar el ancho de banda percibido durante una sesión de streaming. |

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

Las últimas seis clases están disponibles como clases de utilidad en la implementación de referencia.

## Cambios de área de nombres {#namespace-changes}

La API de TVSDK 2.5 consolida los espacios de nombres.

Todos los nombres de clase de la API de TVSDK 2.5 comienzan con el prefijo com.adobe.mediacore. Algunos nombres de clase de la API de TVSDK 1.4 comienzan con com.adobe.ave. Las clases correspondientes de la versión 2.5 cambian com.adobe.ave a com.adobe.mediacore. Por ejemplo, observe los cambios en las siguientes líneas de código para 1.4 y 2.5:

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
Por ejemplo, así se registra un controlador de eventos para `MediaPlayerEvent.STATUS_CHANGED:`

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

### Eventos renombrados {#renamed-events}

| Nuevo nombre | Nombre antiguo |
|--- |--- |
| SEEK_BEGIN | SEEK_STARTED |
| SEEK_END | SEEK_COMPLETED |
| SEEK_POSITION_ADJUSTED | SEEK_ADJUST_COMPLETED |
| BUFFERING_BEGIN | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATUS_CHANGED | STATE_CHANGED |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_ADDED |
| SIZE_AVAILABLE | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## Cambios de MediaPlayer {#mediaplayer-changes}

Una nueva forma de construir `MediaPlayer` y cambia algunos de los métodos.

**Cambios en la clase MediaPlayer**

Estos son los cambios en `MediaPlayer` clase:

* El `MediaPlayerStatus` enum reemplaza a `MediaPlayer.PlayerState`. Por ejemplo:

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

* El `MediaPlayer.seekToLocalTime()` ahora se llama al método `MediaPlayer.seekToLocal`. Por ejemplo:

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* El `MediaPlayerView.notifyClick()` el método es ahora `MediaPlayer.notifyClick()`. Por ejemplo:

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* La primera `MediaPlayer.MediaPlayer.getNotificationHistory()` El método de ya no está disponible y no se ha reemplazado.
* La primera `MediaPlayer.replaceCurrentItem()` se divide en dos métodos: `replaceCurrentResource()`, que toma una instancia de `MediaResource`, y `replaceCurrentItem()`, que toma una instancia de `MediaPlayerItem`. Por ejemplo:

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

Puede utilizar esto para cambiar entre instancias preinicializadas de MediaPlayer, como en el caso de las interrupciones.

**Los constructores reemplazan los métodos estáticos create()**

Puede utilizar constructores en TVSDK v2.5, en lugar de utilizar `create()` métodos de TVSDK v1.4. Todas las clases con nombres que comienzan por Default, como `DefaultMediaPlayer`, `DefaultNetworkConfig`, `DefaultContentFactory`, no están disponibles en la versión 2.5.

En algunos casos, la API de TVSDK v1.4 utiliza el siguiente patrón para crear clases:

1. Defina una interfaz (por ejemplo, `MediaPlayer`).
1. Proporcione una clase predeterminada (por ejemplo, `DefaultMediaPlayer`).
1. Proporcione un `create()` en la clase predeterminada para proporcionar una clase que implementa la interfaz.

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

Otras clases que no siguen este patrón pero utilizan `create()` Los métodos de la versión 1.4 incluyen:

* MediaResource\
   Anteriormente utilizado `MediaResource.createFromUrl()`. Ahora utilice el constructor, que toma una dirección URL, un tipo de recurso y metadatos. Por ejemplo:

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

* Anuncio
* AdAsset
* AdBreak

Algunas clases (por ejemplo, `ContentFactory`) son clases abstractas sin implementación predeterminada disponible públicamente (por ejemplo, `DefaultContentFactory`). En estos casos, puede proporcionar una implementación predeterminada mediante una función de conveniencia, por ejemplo: `mediaPlayerItemConfig.getDefaultContentFactory()`

**Cambios en los subtítulos**

Los siguientes cambios afectan a las clases relacionadas con los subtítulos:

* Al recuperar las pistas de subtítulos cerrados, `MediaPlayerItem.getClosedCaptionTracks()` sólo devuelve pistas activas.
* `ClosedCaptionTrack` ya no tiene un `isActive()` método.

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

## Cambios publicitarios {#advertising-changes}

Hay varios cambios relacionados con el anuncio en la versión 2.5.

**Cambios en el comportamiento publicitario**

El comportamiento predeterminado de la reproducción del anuncio cuando un usuario realiza una búsqueda más allá de un pod de anuncios cambia ligeramente en la versión 2.5. Si no se ve la pausa publicitaria, se reproduce después de una búsqueda hacia delante. Cuando la aplicación utiliza la política de publicidad predeterminada, la pausa publicitaria se elimina una vez finalizada la reproducción. Con TVSDK v2.5, si un usuario busca detrás de un pod de anuncios en la cronología y no se ve la pausa publicitaria, no se reproduce ningún anuncio.

Sin embargo, en TVSDK v1.4, de forma predeterminada, se reproduce un anuncio en caso de una búsqueda hacia atrás. Por ejemplo, si busca hacia atrás entre la tercera y la cuarta pausa publicitaria, el comportamiento predeterminado para TVSDK v1.4 es reproducir la tercera pausa publicitaria.

**Cambio de reglas de publicidad**

Las reglas de publicidad se especifican mediante un archivo JSON. El formato del archivo JSON sigue siendo el mismo en ambas versiones de TVSDK. Sin embargo, en TVSDK v2.5, el archivo JSON de reglas de publicidad debe alojarse en una ubicación accesible a través de una URL HTTP. La aplicación puede utilizar una instancia de AuditudeSettings.

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

En la versión 1.4 de TVSDK, este archivo se coloca debajo de la carpeta de recursos en la aplicación y TVSDK carga el archivo.

**Cambio de nombre de fábrica de anuncios**

`AdvertisingFactory` ahora se denomina `ContentFactory`. Con `ContentFactory` puede crear flujos de trabajo de publicidad personalizados anulando algunos de sus métodos. Utilice devolver nulo para mantener los comportamientos predeterminados, como en los siguientes casos:

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

**Saltos de anuncios de longitud cero**

TVSDK 2.5 inserta pausas publicitarias de longitud cero como marcadores de posición cuando el servidor de publicidad no devuelve anuncios.

Las pausas publicitarias de longitud cero se pueden determinar detectando que el recuento de anuncios es cero en la pausa publicitaria mediante el evento onAdBreakStarted y la aplicación debe gestionar estas pausas publicitarias en consecuencia.

**Cambios de metadatos**

La clase de metadatos proporciona un reemplazo más eficaz para la clase MetadataNode anterior.

* La clase Metadata puede almacenar cadenas, matrices de bytes y otros objetos Metadata:

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

* El `MetadataKeys` enum reemplaza a `DefaultMetadataKeys`. No todas las llaves están dentro `DefaultMetadataKeys` están presentes en la nueva versión.

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

* Los metadatos de publicidad ahora se representan mediante la variable `AdvertisingMetadata` , una subclase de Metadatos y ahora se almacena en `MediaPlayerItemConfig` en lugar de `MediaResource`.

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

Metadatos de configuración de red, anteriormente miembro de `MediaResource` , ahora se representa mediante la clase `NetworkConfiguration` y ahora se almacena en `MediaPlayerItemConfig` en lugar de `MediaResource`.

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**Cambios en el análisis de metadatos cronometrados**

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

* El `notifyClick()` El método se ha movido de `MediaPlayerView` hasta `MediaPlayer`.

* `AdPolicySelector` es una interfaz, no una clase. Implemente todos sus métodos.
* `AdPolicyInfo` ahora contiene una lista de `AdBreakTimelineItem`, no `AdBreakPlacement`.

* Nombre de API de `ContentResolver` se cambia la clase abstracta.
* `PlacementOpportunityDetector` ya no está disponible. En su lugar, amplíe el `OpportunityGenerator` clase abstracta. La implementación de referencia proporciona un ejemplo de esto.

* Los parámetros del `AdBreakPlacement` Los constructores son los mismos, pero en un orden diferente. Para ver una implementación de ejemplo, consulte la Implementación del reproductor de referencia integrada en el producto.

## Cambios en DRM {#changes-in-drm}

La mayoría de los cambios de esta versión se realizan en la capa DRM. La siguiente tabla muestra cambios adicionales entre las versiones 1.4 y 2.5:

| Método DRManager | Llamada de retorno de éxito en 1.4 | Devolución de llamada de error en 1.4 | Listener en 2.5 |
|--- |--- |--- |--- |
| acquisitionLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| acquisitionPreviewLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| autentificar | DRMAuthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | NA | DRMOperationErrorCallback | DRMErrorListener |
| initialize | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leaveLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
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

La estática `DRMManager` la instancia de que estaba disponible en 1.4 después de crear mediaplayer ahora está disponible después de que `onDRMMetadataInfo` se activa el detector de eventos.

## Cambios relacionados con la velocidad de bits adaptable (ABR) {#adaptive-bitrate-abr-related-changes}

**Cambios en las constantes**

Muchas constantes han cambiado el tipo de `String` hasta `int`. Por ejemplo: `MediaResourceType`, `ABRControlParameters`, y `MediaPlayerStatusChangeEvent`.

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

Se han añadido algunos parámetros, se ha cambiado el nombre de algunos y se han movido algunos. A continuación se muestran la firma del constructor en v1.4 y la nueva firma en 2.5:

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

El `MediaError` La clase se ha reemplazado por `Notification` clase. La única diferencia entre las clases `MediaError` y `Notification` Esto último no contiene un atributo de descripción. Los códigos de error de TVSDK 1.4 con los valores 101xxx, 102xxx, 104xxx, 106xxx, 107xxx, 109xxx no existen en TVSDK 2.5. Para ver los códigos de reproducción de TVSDK 2.5, consulte [Error nativo: valores de reproducción de vídeo](assets/psdk_android_2.5.pdf).

A continuación se muestran ejemplos de control de errores en TVSDK 1.4 y 2.5:

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

Todos los errores recuperables se tratan como advertencias y se gestionan mediante el `NotificationEventListener` en TVSDK 2.5. Las advertencias aparecen como notificaciones con la variable `onOperationFailed` Listener en el controlador QOS en TVSDK 1.4 donde, como en TVSDK 2.5, la notificación es un evento independiente. La advertencia gestionada en 1.4 y 2.5 es la siguiente:

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

Mientras que TVSDK v1.4 utilizaba una combinación de valores nulos, los resultados de error y una variedad de excepciones ( `MediaPlayerException`, `IllegalStateException`, y `IllegalArgumentException`), TVSDK v2.5 `generatesMediaPlayerException` para todos los errores.

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
* TVSDK 2.5 QOSProvider tiene una nueva propiedad para determinar el ancho de banda percibido durante una sesión de streaming.

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

* El `QOSEventListener::onOperationFailed()` ya no existe en TVSDK 2.5. Las advertencias que solían aparecer en este detector de eventos ahora aparecerán en el `NotificationEventListener::onNotification()` detector de eventos.

* El `QOSProvider event listeners onBufferStart()`, `onBufferComplete()`, `onSeekStart()`, `onSeekComplete()`, y `onLoadInfo()` son detectores de eventos individuales enlazados con una instancia de mediaPlayer.

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

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
