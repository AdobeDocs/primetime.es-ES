---
description: Los controladores de eventos permiten que TVSDK responda a eventos.
title: Implementación de oyentes de eventos y llamadas de retorno
exl-id: eda5cd4e-4ee8-4b37-a179-242e8697f61f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Implementación de oyentes de eventos y llamadas de retorno{#implement-event-listeners-and-callbacks}

Los controladores de eventos permiten que TVSDK responda a eventos.

Cuando se produce un evento, el mecanismo de eventos de TVSDK llama al controlador de eventos registrado y pasa la información de evento al controlador.

TVSDK define los oyentes como interfaces internas públicas en `MediaPlayer` interfaz.

La aplicación debe implementar detectores de eventos para los eventos de TVSDK que afecten a la aplicación.

Para obtener una lista completa de los eventos de análisis de vídeo, consulte Seguimiento de reproducción de vídeo principal.

1. Determine para qué eventos debe escuchar la aplicación.

   * **Eventos obligatorios**: escucha todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >El evento de reproducción `onStateChanged` proporciona el estado del reproductor, incluidos los errores. Cualquiera de los estados puede afectar al siguiente paso del reproductor

   * **Otros eventos**: Opcional, según la aplicación.

      Por ejemplo, si incorpora publicidad en la reproducción, implemente las llamadas de retorno AdPlaybackEventListener.

1. Implemente detectores de eventos para cada evento.

   TVSDK devuelve valores de parámetro a las llamadas de retorno del oyente de eventos. Estos valores proporcionan información relevante sobre el evento que puede utilizar en los oyentes para realizar las acciones adecuadas.

   `MediaPlayer.EventListener` enumera todas las interfaces de devolución de llamada. Cada interfaz muestra el nombre de la llamada de retorno y los parámetros que se devuelven para cada evento.

   Por ejemplo:

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. Registre los oyentes de devolución de llamada con `MediaPlayer` mediante `MediaPlayer.addEventListener`.

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

TVSDK envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

Los siguientes ejemplos muestran el orden de algunos eventos que incluyen eventos de reproducción.

* Al cargar correctamente un recurso de medios mediante `MediaPlayer.replaceCurrentResource`, el orden de los eventos es:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con el estado `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con el estado `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>Cargue el recurso de medios en el subproceso principal. Si carga un recurso multimedia en un subproceso en segundo plano, esta operación u operaciones posteriores de TVSDK, o ambas, podrían generar un error (por ejemplo, `IllegalStateException`) y salga.

* Al preparar la reproducción mediante `MediaPlayer.prepareToPlay`, el orden de los eventos es:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con el estado `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` si se insertaron anuncios.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` con el estado `MediaPlayerStatus.PREPARED`

* En el caso de los flujos lineales/en directo, durante la reproducción a medida que avanza la ventana de reproducción y se resuelven oportunidades adicionales, el orden de los eventos es el siguiente:

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` si se insertaron anuncios
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` si se insertaron anuncios

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

Cuando la reproducción incluye publicidad, TVSDK envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

Al reproducir anuncios, el orden de los eventos es:

* `AdPlaybackEventListener.onAdBreakStart`
* Se envían los siguientes elementos por cada anuncio de la pausa publicitaria:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (varias veces durante la reproducción de un anuncio)
   * `AdPlaybackEventListener.onAdClick` (por cada clic)
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

Al reproducir anuncios, el orden de los eventos es:

* `AdPlaybackEventListener.onAdBreakStart`
* Se envían los siguientes elementos por cada anuncio de la pausa publicitaria:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (varias veces durante la reproducción de un anuncio)
   * `AdPlaybackEventListener.onAdClick` (por cada clic)
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

TVSDK envía eventos de calidad de servicio (QoS) para notificar a la aplicación eventos que podrían influir en el cálculo de las estadísticas de QoS, como el almacenamiento en búfer y los eventos de búsqueda.

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

## Eventos de DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles. El reproductor puede implementar acciones en respuesta a estos eventos.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, espere `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. TVSDK envía eventos DRM adicionales a través de la `DRMManager` clase.

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
| `onLoadComplete (mediaPlayerItem playerItem)` | La carga de medios se completó correctamente. |
| `onError` | Se ha producido un problema con la carga de medios. |
