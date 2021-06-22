---
description: La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor escuchando los eventos que envía TVSDK.
title: Resumen de eventos del reproductor de Primetime
exl-id: 3912f140-1600-41fb-9dc4-306646b7cd85
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Resumen de eventos del reproductor Primetime {#primetime-player-events-summary}

La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor escuchando los eventos que envía TVSDK.

## Eventos {#events}

TVSDK le notifica cuándo se producen eventos a los que debe responder su aplicación. Cada evento corresponde a una clase listener, con un método callback que debe implementar.

>[!TIP]
>
>Los códigos de evento son las constantes de la enumeración `MediaPlayerEvent`.

`AdBreakCompletedEventListener`

* **** Lo que significa que la reproducción de la pausa publicitaria ha finalizado.

* **Llamada de retorno para implementar** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** Lo que significa que se omitió una pausa publicitaria durante la reproducción.

* **Llamada de retorno para implementar** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **** Lo que significa que se ha iniciado la reproducción de la pausa publicitaria.

* **Llamada de retorno para implementar** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_START`

`AdClickedEventListener`

* **** Lo que significa que se hizo clic en un anuncio durante la reproducción.

* **Llamada de retorno para implementar** `onAdClicked(AdClickEvent event)`
* **Código de evento** `AD_CLICK`

`AdCompletedEventListener`

* **** Lo que significa que la reproducción del anuncio ha finalizado.

* **Llamada de retorno para implementar** `onAdCompleted(AdPlaybackEvent event)`

* **Código de evento** `AD_COMPLETE`

`AdProgressEventListener`

* **** Significa que se informa del progreso durante la reproducción.

* **Llamada de retorno para implementar** `onAdProgress(AdPlaybackEvent event)`

* **Código de evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** Lo que significa que la toma de decisiones y la resolución de anuncios de Primetime han finalizado. Este evento solo se aplica al contenido de VOD.

* **Llamada de retorno para implementar** `onAdResolutionComplete()`

* **Código de evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** Lo que significa que se ha iniciado la reproducción del anuncio.

* **Llamada de retorno para implementar** `onAdStarted(AdPlaybackEvent event)`

* **Código de evento** `AD_START`

`AudioUpdatedEventListener`

* **** Lo que significa que se ha detectado una nueva pista de audio.

* **Llamada de retorno para implementar** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** Es decir, el reproductor ha empezado a almacenar en búfer.

* **Llamada de retorno para implementar** `onBufferingBegin(BufferEvent event)`

* **Código de evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** Es decir, el reproductor ha dejado de almacenar en búfer.

* **Llamada de retorno para implementar** `onBufferingEnd(BufferEvent event)`

* **Código de evento** `BUFFERING_END`

`BufferPreparedEventListener`

* **** Significa que el búfer está preparado.

* **Llamada de retorno para implementar** `onBufferPrepared()`

* **Código de evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** Lo que significa que se ha detectado una nueva pista de rótulo.

* **Llamada de retorno para implementar** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** Lo que significa que se ha detectado un nuevo metadatos DRM en el flujo de medios.

* **Llamada de retorno para implementar** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Código de evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **** Lo que significa que se ha creado un nuevo elemento del reproductor de contenidos.

* **Llamada de retorno para implementar** `onItemCreated(MediaPlayerItemEvent event)`

* **Código de evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** Significa que se ha creado nueva información de carga para el elemento actual.

* **Llamada de retorno para implementar** `onLoadComplete(MediaPlayerItemEvent event)`

* **Código de evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** Lo que significa que se ha cargado un segmento nuevo.

* **Llamada de retorno para implementar** `onLoadInformation(LoadInformationEvent event)`

* **Código de evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** Lo que significa que se ha actualizado el manifiesto principal o la lista de reproducción.

* **Llamada de retorno para implementar** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** Lo que significa que la operación ha fallado.

* **Llamada de retorno para implementar** `onNotification(NotificationEvent event)`

* **Código de evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** Lo que significa que se ha actualizado el intervalo de reproducción.

* **Llamada de retorno para implementar** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** Esto significa que se puede ver una nueva tasa de reproducción en la pantalla.

* **Llamada de retorno para implementar** `onRatePlaying(PlaybackRateEvent event)`

* **Código de evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** Es decir, se ha establecido el atributo de tasa de MediaPlayer.

* **Llamada de retorno para implementar** `onRateSelected(PlaybackRateEvent event)`

* **Código de evento** `RATE_SELECTED`

`PlayStartEventListener`

* **** Es decir, se ha iniciado la reproducción.

* **Llamada de retorno para implementar** `onPlayStart()`

* **Código de evento** `PLAY_START`

`ProfileChangeEventListener`

* **** Es decir, el perfil actual de MediaPlayer ha cambiado.

* **Llamada de retorno para implementar** `onProfileChanged(ProfileEvent event)`

* **Código de evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** Significa que Playback ha alcanzado una reserva en la cronología.

* **Llamada de retorno para implementar** `onReservationReached(ReservationEvent event)`

* **Código de evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **** Se inició la operación de SIGNIFICACIÓN.

* **Llamada de retorno para implementar** `onSeekBegin(SeekEvent event)`

* **Código de evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **** Lo que significa que la operación de búsqueda ha finalizado.

* **Llamada de retorno para implementar** `onSeekEnd(SeekEvent event)`

* **Código de evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **** Lo que significa que la posición de búsqueda se ha ajustado debido a reglas de reproducción internas o reglas comerciales externas.

* **Llamada de retorno para implementar** `onPositionAdjusted(SeekEvent event)`

* **Código de evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** Es decir, el tamaño del contenido está disponible.

* **Llamada de retorno para implementar** `onSizeAvailable(SizeAvailableEvent event)`

* **Código de evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** Es decir, el estado de MediaPlayer ha cambiado.

* **Llamada de retorno para implementar** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Código de evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** Es decir, el cabezal de reproducción ha cambiado.

* **Llamada de retorno para implementar** `onTimeChanged(TimeChangeEvent event)`

* **Código de evento** `TIME_CHANGED`

`TimedEventEventListener`

* **** Es decir, la operación se completa con el tiempo necesario para la operación.

* **Llamada de retorno para implementar** `onTimedEvent(TimedEventEvent event)`

* **Código de evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** Es decir, se ha añadido un nuevo metadato temporizado a un elemento en segundo plano.

* **Llamada de retorno para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código de evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** Es decir, se ha detectado un nuevo metadato temporizado en el flujo de medios.

* **Llamada de retorno para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código de evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** Lo que significa que la línea de tiempo se ha modificado. Es posible que se hayan agregado o eliminado anuncios de la cronología.

* **Llamada de retorno para implementar** `onTimelineUpdated(TimelineEvent event)`

* **Código de evento** `TIMELINE_UPDATED`
