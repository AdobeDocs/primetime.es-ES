---
description: Los controladores de eventos permiten que TVSDK responda a los eventos.
seo-description: Los controladores de eventos permiten que TVSDK responda a los eventos.
seo-title: Implementar escuchas de eventos y rellamadas
title: Implementar escuchas de eventos y rellamadas
uuid: 6b7859a4-55f9-48b1-b1f1-7b79bc92610a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementar escuchas de eventos y rellamadas{#implement-event-listeners-and-callbacks}

Los controladores de eventos permiten que TVSDK responda a los eventos.

Cuando se produce un evento, el mecanismo de eventos de TVSDK llama al controlador de eventos registrado y pasa la información del evento al controlador.

TVSDK define los oyentes como interfaces internas públicas en la `MediaPlayer` interfaz.

La aplicación debe implementar detectores de eventos para los eventos TVSDK que afecten a la aplicación.

Para obtener una lista completa de los eventos de análisis de vídeo, consulte Seguimiento de la reproducción de vídeo principal.

1. Determinar los eventos que debe escuchar la aplicación.

   * **Eventos** requeridos: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `onStateChanged` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar al siguiente paso del reproductor

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, implemente las rellamadas AdPlaybackEventListener.

1. Implementar detectores de eventos para cada evento.

   TVSDK devuelve valores de parámetro a las llamadas de retorno de event-listener. Estos valores proporcionan información relevante sobre el evento que puede utilizar en los oyentes para realizar las acciones adecuadas.

   `MediaPlayer.EventListener` enumera todas las interfaces de llamada de retorno. Cada interfaz muestra el nombre y los parámetros de llamada de retorno que se devuelven para cada evento.

   Por ejemplo:

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. Registre los oyentes de llamada de retorno con el `MediaPlayer` objeto mediante `MediaPlayer.addEventListener`.

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## Orden de los eventos de reproducción {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

Los siguientes ejemplos muestran el orden de algunos eventos que incluyen eventos de reproducción.

* Cuando se carga correctamente un recurso de medios a través de `MediaPlayer.replaceCurrentResource`, el orden de los eventos es:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con estado `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con estado `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>Cargue el recurso de medios en el subproceso principal. Si carga un recurso de medios en un subproceso en segundo plano, esta operación o las siguientes operaciones de TVSDK, o ambas, podrían generar un error (por ejemplo, `IllegalStateException`) y salir.

* Al prepararse para la reproducción a través de `MediaPlayer.prepareToPlay`, el orden de los eventos es:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con estado `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` si se insertaron publicidades.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` con estado `MediaPlayerStatus.PREPARED`

* Para flujos en directo/lineal, durante la reproducción a medida que avanza la ventana de reproducción y se resuelven oportunidades adicionales, el orden de los eventos es:

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` si se insertaron publicidades
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` si se insertaron publicidades

El siguiente ejemplo muestra una progresión típica de los eventos:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## Orden de los eventos publicitarios {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Cuando la reproducción incluye publicidad, TVSDK distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

Al reproducir publicidades, el orden de los eventos es:

* `AdPlaybackEventListener.onAdBreakStart`
* Se envían los siguientes datos para cada publicidad en la pausa publicitaria:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (varias veces durante la reproducción de un anuncio)
   * `AdPlaybackEventListener.onAdClick` (para cada clic)
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

El siguiente ejemplo muestra una progresión típica de los eventos de reproducción de publicidad:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

Al reproducir publicidades, el orden de los eventos es:

* `AdPlaybackEventListener.onAdBreakStart`
* Se envían los siguientes datos para cada publicidad en la pausa publicitaria:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (varias veces durante la reproducción de un anuncio)
   * `AdPlaybackEventListener.onAdClick` (para cada clic)
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

El siguiente ejemplo muestra una progresión típica de los eventos de reproducción de publicidad:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## Eventos de QoS {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK distribuye eventos de calidad de servicio (QoS) para notificar a la aplicación los eventos que pueden influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y la búsqueda de eventos.

El siguiente ejemplo muestra una progresión típica de estos eventos:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## Eventos DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM. El reproductor puede implementar acciones en respuesta a estos eventos.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, escuche `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. TVSDK distribuye eventos DRM adicionales a través de la `DRMManager` clase.

El siguiente ejemplo muestra una progresión típica:

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## Eventos de cargador {#section_5638F8EDACCE422A9425187484D39DCC}

El reproductor puede implementar acciones en función de los siguientes eventos:

| Evento | Significado |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | La carga de recursos multimedia se completó correctamente. |
| `onError` | Se produjo un problema con la carga de recursos multimedia. |

