---
description: La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor escuchando los eventos que envía TVSDK.
seo-description: La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor escuchando los eventos que envía TVSDK.
seo-title: Resumen de eventos de Primetime Player
title: Resumen de eventos de Primetime Player
uuid: b2ff74f2-c373-42da-a717-2f0550cbcb7f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Resumen de eventos de Primetime player {#primetime-player-events-summary}

La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor escuchando los eventos que envía TVSDK.

## Eventos {#events}

TVSDK le notifica cuándo se producen eventos, a los que debe responder la aplicación. Cada evento corresponde a una clase de oyente, con un método de llamada de retorno que debe implementar.

>[!TIP]
>
>Los códigos de evento son las constantes de la enumeración `MediaPlayerEvent`.

`AdBreakCompletedEventListener`

* **** Significa que la reproducción de la pausa publicitaria se ha completado.

* **Llamada de retorno para implementar** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** Significa que se omitió una pausa publicitaria durante la reproducción.

* **Llamada de retorno para implementar** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **** SignificadoSe ha iniciado la reproducción de la pausa publicitaria.

* **Llamada de retorno para implementar** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_START`

`AdClickedEventListener`

* **** Significa que se hizo clic en un anuncio durante la reproducción.

* **Llamada de retorno para implementar** `onAdClicked(AdClickEvent event)`
* **Código de evento** `AD_CLICK`

`AdCompletedEventListener`

* **** Significa que la reproducción de la publicidad se ha completado.

* **Llamada de retorno para implementar** `onAdCompleted(AdPlaybackEvent event)`

* **Código de evento** `AD_COMPLETE`

`AdProgressEventListener`

* **** SignificadoProgreso de los informes durante la reproducción.

* **Llamada de retorno para implementar** `onAdProgress(AdPlaybackEvent event)`

* **Código de evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** SignificadoPrimetime y la toma de decisiones y la resolución se han completado. Este evento solo se aplica al contenido de VOD.

* **Llamada de retorno para implementar** `onAdResolutionComplete()`

* **Código de evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** Significa que se ha iniciado la reproducción de la publicidad.

* **Llamada de retorno para implementar** `onAdStarted(AdPlaybackEvent event)`

* **Código de evento** `AD_START`

`AudioUpdatedEventListener`

* **** Significa que se ha detectado una nueva pista de audio.

* **Llamada de retorno para implementar** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** Significa que el reproductor ha empezado a almacenar en búfer.

* **Llamada de retorno para implementar** `onBufferingBegin(BufferEvent event)`

* **Código de evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** Significa que el reproductor ha dejado de almacenar en búfer.

* **Llamada de retorno para implementar** `onBufferingEnd(BufferEvent event)`

* **Código de evento** `BUFFERING_END`

`BufferPreparedEventListener&#39;

* **** Significa que el búfer está preparado.

* **Llamada de retorno para implementar** `onBufferPrepared()`

* **Código de evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** Significa que se ha detectado una nueva pista de rótulo.

* **Llamada de retorno para implementar** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** Significa que se ha detectado un nuevo metadatos DRM en el flujo de medios.

* **Llamada de retorno para implementar** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Código de evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **** Significa que se ha creado un nuevo elemento de reproductor de medios.

* **Llamada de retorno para implementar** `onItemCreated(MediaPlayerItemEvent event)`

* **Código de evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** Significa que se ha creado nueva información de carga para el elemento actual.

* **Llamada de retorno para implementar** `onLoadComplete(MediaPlayerItemEvent event)`

* **Código de evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** Significa que se ha cargado un nuevo segmento.

* **Llamada de retorno para implementar** `onLoadInformation(LoadInformationEvent event)`

* **Código de evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** Significa que se ha actualizado el manifiesto o la lista de reproducción principal.

* **Llamada de retorno para implementar** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** Significa que la operación ha fallado.

* **Llamada de retorno para implementar** `onNotification(NotificationEvent event)`

* **Código de evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** Es decir, se ha actualizado el intervalo de reproducción.

* **Llamada de retorno para implementar** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** Es decir, se muestra una nueva velocidad de reproducción en la pantalla.

* **Llamada de retorno para implementar** `onRatePlaying(PlaybackRateEvent event)`

* **Código de evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** Significa que se ha establecido el atributo de tasa de MediaPlayer.

* **Llamada de retorno para implementar** `onRateSelected(PlaybackRateEvent event)`

* **Código de evento** `RATE_SELECTED`

`PlayStartEventListener`

* **** Significa que se ha iniciado la reproducción.

* **Llamada de retorno para implementar** `onPlayStart()`

* **Código de evento** `PLAY_START`

`ProfileChangeEventListener`

* **** Es decir, el perfil actual de MediaPlayer ha cambiado.

* **Llamada de retorno para implementar** `onProfileChanged(ProfileEvent event)`

* **Código de evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** Significa que Playback ha alcanzado una reserva de línea de tiempo.

* **Llamada de retorno para implementar** `onReservationReached(ReservationEvent event)`

* **Código de evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Se** inició la operación de SignificadoSeek.

* **Llamada de retorno para implementar** `onSeekBegin(SeekEvent event)`

* **Código de evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **** Significa que la operación de búsqueda ha finalizado.

* **Llamada de retorno para implementar** `onSeekEnd(SeekEvent event)`

* **Código de evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **** SignificadoLa posición de búsqueda se ha ajustado debido a reglas de reproducción internas o reglas comerciales externas.

* **Llamada de retorno para implementar** `onPositionAdjusted(SeekEvent event)`

* **Código de evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** Significa que el tamaño del medio está disponible.

* **Llamada de retorno para implementar** `onSizeAvailable(SizeAvailableEvent event)`

* **Código de evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** Significa que el estado de MediaPlayer ha cambiado.

* **Llamada de retorno para implementar** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Código de evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** Significa que el cursor de reproducción ha cambiado.

* **Llamada de retorno para implementar** `onTimeChanged(TimeChangeEvent event)`

* **Código de evento** `TIME_CHANGED`

`TimedEventEventListener`

* **** Significa que la operación se completa con el tiempo necesario para la operación.

* **Llamada de retorno para implementar** `onTimedEvent(TimedEventEvent event)`

* **Código de evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** SignificadoSe han agregado nuevos metadatos temporizados a un elemento en segundo plano.

* **Llamada de retorno para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código de evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** Significa que se ha detectado un nuevo metadatos temporizados en el flujo de medios.

* **Llamada de retorno para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código de evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** Significa que la línea de tiempo se ha modificado. Es posible que las publicidades se hayan agregado o eliminado de la línea de tiempo.

* **Llamada de retorno para implementar** `onTimelineUpdated(TimelineEvent event)`

* **Código de evento** `TIMELINE_UPDATED`