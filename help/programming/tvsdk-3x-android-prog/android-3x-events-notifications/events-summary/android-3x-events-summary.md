---
description: La aplicación puede monitorizar la actividad del reproductor y su estado cambiando al escuchar los eventos que envía TVSDK.
title: Resumen de eventos del reproductor Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Resumen de eventos del reproductor Primetime {#primetime-player-events-summary}

La aplicación puede monitorizar la actividad del reproductor y su estado cambiando al escuchar los eventos que envía TVSDK.

## Eventos {#events}

TVSDK le avisa cuando se producen eventos, a los que la aplicación debe responder. Cada evento corresponde a una clase de agente de escucha, con un método de devolución de llamada que debe implementar.

>[!TIP]
>
>Los códigos de evento son las constantes de `MediaPlayerEvent` enum.

`AdBreakCompletedEventListener`

* **Significado** Se ha completado la reproducción de la pausa publicitaria.

* **Llamada de retorno para implementar** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Significado** Se ha omitido una pausa publicitaria durante la reproducción.

* **Llamada de retorno para implementar** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Significado** Ha comenzado la reproducción de la pausa publicitaria.

* **Llamada de retorno para implementar** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Código de evento** `AD_BREAK_START`

`AdClickedEventListener`

* **Significado** Se hizo clic en un anuncio durante la reproducción.

* **Llamada de retorno para implementar** `onAdClicked(AdClickEvent event)`
* **Código de evento** `AD_CLICK`

`AdCompletedEventListener`

* **Significado** Se ha completado la reproducción del anuncio.

* **Llamada de retorno para implementar** `onAdCompleted(AdPlaybackEvent event)`

* **Código de evento** `AD_COMPLETE`

`AdProgressEventListener`

* **Significado** Informe del progreso durante la reproducción.

* **Llamada de retorno para implementar** `onAdProgress(AdPlaybackEvent event)`

* **Código de evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Significado** Se ha completado Primetime y decisioning and resolution. Este evento solo se aplica al contenido de VOD.

* **Llamada de retorno para implementar** `onAdResolutionComplete()`

* **Código de evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **Significado** Ha comenzado la reproducción del anuncio.

* **Llamada de retorno para implementar** `onAdStarted(AdPlaybackEvent event)`

* **Código de evento** `AD_START`

`AudioUpdatedEventListener`

* **Significado** Se ha detectado una nueva pista de audio.

* **Llamada de retorno para implementar** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **Significado** El reproductor ha iniciado el almacenamiento en búfer.

* **Llamada de retorno para implementar** `onBufferingBegin(BufferEvent event)`

* **Código de evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **Significado** El reproductor ha dejado de almacenar en búfer.

* **Llamada de retorno para implementar** `onBufferingEnd(BufferEvent event)`

* **Código de evento** `BUFFERING_END`

`BufferPreparedEventListener`

* **Significado** El búfer está preparado.

* **Llamada de retorno para implementar** `onBufferPrepared()`

* **Código de evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **Significado** Se ha detectado un nuevo seguimiento de subtítulos.

* **Llamada de retorno para implementar** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **Significado** Se ha detectado un nuevo metadato DRM en el flujo de medios.

* **Llamada de retorno para implementar** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Código de evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **Significado** Se ha creado un nuevo elemento de reproductor de contenidos.

* **Llamada de retorno para implementar** `onItemCreated(MediaPlayerItemEvent event)`

* **Código de evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **Significado** Se ha creado nueva información de carga para el elemento actual.

* **Llamada de retorno para implementar** `onLoadComplete(MediaPlayerItemEvent event)`

* **Código de evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **Significado** Se ha cargado un nuevo segmento.

* **Llamada de retorno para implementar** `onLoadInformation(LoadInformationEvent event)`

* **Código de evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Significado** Se ha actualizado el manifiesto principal o la lista de reproducción.

* **Llamada de retorno para implementar** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **Significado** Error en la operación.

* **Llamada de retorno para implementar** `onNotification(NotificationEvent event)`

* **Código de evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **Significado** Se ha actualizado el intervalo de reproducción.

* **Llamada de retorno para implementar** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Código de evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Significado** Se puede ver una nueva velocidad de reproducción en la pantalla.

* **Llamada de retorno para implementar** `onRatePlaying(PlaybackRateEvent event)`

* **Código de evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **Significado** Se ha establecido el atributo de tarifa de MediaPlayer.

* **Llamada de retorno para implementar** `onRateSelected(PlaybackRateEvent event)`

* **Código de evento** `RATE_SELECTED`

`PlayStartEventListener`

* **Significado** Se ha iniciado la reproducción.

* **Llamada de retorno para implementar** `onPlayStart()`

* **Código de evento** `PLAY_START`

`ProfileChangeEventListener`

* **Significado** El perfil actual de MediaPlayer ha cambiado.

* **Llamada de retorno para implementar** `onProfileChanged(ProfileEvent event)`

* **Código de evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **Significado** La reproducción ha alcanzado una reserva de cronología.

* **Llamada de retorno para implementar** `onReservationReached(ReservationEvent event)`

* **Código de evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Significado** Operación de búsqueda iniciada.

* **Llamada de retorno para implementar** `onSeekBegin(SeekEvent event)`

* **Código de evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **Significado** La operación de búsqueda ha finalizado.

* **Llamada de retorno para implementar** `onSeekEnd(SeekEvent event)`

* **Código de evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Significado** La posición de búsqueda se ha ajustado debido a reglas de reproducción internas o reglas de negocio externas.

* **Llamada de retorno para implementar** `onPositionAdjusted(SeekEvent event)`

* **Código de evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **Significado** El tamaño del medio está disponible.

* **Llamada de retorno para implementar** `onSizeAvailable(SizeAvailableEvent event)`

* **Código de evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **Significado** El estado de MediaPlayer ha cambiado.

* **Llamada de retorno para implementar** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Código de evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **Significado** El cabezal de reproducción ha cambiado.

* **Llamada de retorno para implementar** `onTimeChanged(TimeChangeEvent event)`

* **Código de evento** `TIME_CHANGED`

`TimedEventEventListener`

* **Significado** La operación se ha completado con el tiempo necesario para la operación.

* **Llamada de retorno para implementar** `onTimedEvent(TimedEventEvent event)`

* **Código de evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **Significado** Se ha agregado un nuevo metadato temporizado a un elemento en segundo plano.

* **Llamada de retorno para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código de evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **Significado** Se ha detectado un nuevo metadato cronometrado en el flujo de medios.

* **Llamada de retorno para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código de evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **Significado** Se ha modificado la cronología. Es posible que se hayan agregado o eliminado anuncios de la cronología.

* **Llamada de retorno para implementar** `onTimelineUpdated(TimelineEvent event)`

* **Código de evento** `TIMELINE_UPDATED`
