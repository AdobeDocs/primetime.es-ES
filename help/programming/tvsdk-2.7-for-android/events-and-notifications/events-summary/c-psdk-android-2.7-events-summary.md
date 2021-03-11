---
description: La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor escuchando los eventos que envía TVSDK.
title: Resumen de eventos del reproductor de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Resumen de eventos del reproductor Primetime {#primetime-player-events-summary-overview}

La aplicación puede supervisar la actividad del reproductor y el estado cambiante del reproductor escuchando los eventos que envía TVSDK.

## Eventos {#events}

TVSDK le notifica cuándo se producen eventos a los que debe responder su aplicación. Cada evento corresponde a una clase listener, con un método callback que debe implementar.

>[!TIP]
>
>Los códigos de evento son las constantes de la enumeración `MediaPlayerEvent`.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** Significa ** La reproducción de la pausa publicitaria ha finalizado.

* ** Llamada de retorno para implementar ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** Código de evento ** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** Significa ** Se omitió una pausa publicitaria durante la reproducción.

* ** Llamada de retorno para implementar ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** Código de evento ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** Significa ** Se ha iniciado la reproducción de la pausa publicitaria.

* ** Llamada de retorno para implementar ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** Código de evento ** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** Significa ** Se hizo clic en un anuncio durante la reproducción.

* ** Llamada de retorno para implementar ** `onAdClicked(AdClickEvent event)`

* ** Código de evento ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** Significa ** La reproducción del anuncio ha finalizado.

* ** Llamada de retorno para implementar ** `onAdCompleted(AdPlaybackEvent event)`

* ** Código de evento ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** Significa ** Informe del progreso durante la reproducción.

* ** Llamada de retorno para implementar ** `onAdProgress(AdPlaybackEvent event)`

* ** Código de evento ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Significa ** Primetime ad decisioningy la resolución está completa. Este evento solo se aplica al contenido de VOD.

* ** Llamada de retorno para implementar ** `onAdResolutionComplete()`

* ** Código de evento ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** Significa ** Se ha iniciado la reproducción del anuncio.

* ** Llamada de retorno para implementar ** `onAdStarted(AdPlaybackEvent event)`

* ** Código de evento ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** Significa ** Se ha detectado una nueva pista de audio.

* ** Llamada de retorno para implementar ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** Código de evento ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** Significa ** El reproductor ha empezado a almacenar en búfer.

* ** Llamada de retorno para implementar ** `onBufferingBegin(BufferEvent event)`

* ** Código de evento ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** Significa ** El reproductor ha dejado de almacenar en búfer.

* ** Llamada de retorno para implementar ** `onBufferingEnd(BufferEvent event)`

* ** Código de evento ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** Significa ** Se prepara el búfer.

* ** Llamada de retorno para implementar ** `onBufferPrepared()`

* ** Código de evento ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** Significa ** Se ha detectado una nueva pista de subtítulos.

* ** Llamada de retorno para implementar ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** Código de evento ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** Significa ** Se han detectado nuevos metadatos DRM en el flujo de medios.

* ** Llamada de retorno para implementar ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** Código de evento ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** Significa ** Se ha creado un nuevo elemento de reproductor de contenidos.

* ** Llamada de retorno para implementar ** `onItemCreated(MediaPlayerItemEvent event)`

* ** Código de evento ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** Significa ** Se ha creado nueva información de carga para el elemento actual.

* ** Llamada de retorno para implementar ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** Código de evento ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** Significa ** Se ha cargado un nuevo segmento.

* ** Llamada de retorno para implementar ** `onLoadInformation(LoadInformationEvent event)`

* ** Código de evento ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** Significa ** Se ha actualizado el manifiesto principal o la lista de reproducción.

* ** Llamada de retorno para implementar ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** Código de evento ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** Significa ** La operación ha fallado.

* ** Llamada de retorno para implementar ** `onNotification(NotificationEvent event)`

* ** Código de evento ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** Significa ** Se ha actualizado el intervalo de reproducción.

* ** Llamada de retorno para implementar ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** Código de evento ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** Significa ** Una nueva tasa de reproducción es visible en la pantalla.

* ** Llamada de retorno para implementar ** `onRatePlaying(PlaybackRateEvent event)`

* ** Código de evento ** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** Significa ** Se ha establecido el atributo de tasa de MediaPlayer.

* ** Llamada de retorno para implementar ** `onRateSelected(PlaybackRateEvent event)`

* ** Código de evento ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** Significa ** Se ha iniciado la reproducción.

* ** Llamada de retorno para implementar ** `onPlayStart()`

* ** Código de evento ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** Significa ** El perfil actual de MediaPlayer ha cambiado.

* ** Llamada de retorno para implementar ** `onProfileChanged(ProfileEvent event)`

* ** Código de evento ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** Significa ** Reproducción alcanzada a una reserva en la cronología.

* ** Llamada de retorno para implementar ** `onReservationReached(ReservationEvent event)`

* ** Código de evento ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** Significa ** Se inició la operación de llamada a otro punto del contenido.

* ** Llamada de retorno para implementar ** `onSeekBegin(SeekEvent event)`

* ** Código de evento ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** Significa ** La operación de búsqueda ha finalizado.

* ** Llamada de retorno para implementar ** `onSeekEnd(SeekEvent event)`

* ** Código de evento ** `SEEK_END`

## SeekPositionAjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** Significa ** La posición de búsqueda se ha ajustado debido a reglas de reproducción internas o reglas comerciales externas.

* ** Llamada de retorno para implementar ** `onPositionAdjusted(SeekEvent event)`

* ** Código de evento ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** Significa ** El tamaño del contenido está disponible.

* ** Llamada de retorno para implementar ** `onSizeAvailable(SizeAvailableEvent event)`

* ** Código de evento ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** Significa ** El estado de MediaPlayer ha cambiado.

* ** Llamada de retorno para implementar ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** Código de evento ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** Significa ** El cabezal de reproducción ha cambiado.

* ** Llamada de retorno para implementar ** `onTimeChanged(TimeChangeEvent event)`

* ** Código de evento ** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** Significa ** La operación se completa con el tiempo necesario para la operación.

* ** Llamada de retorno para implementar ** `onTimedEvent(TimedEventEvent event)`

* ** Código de evento ** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** Significa ** Se han agregado nuevos metadatos temporizados a un elemento en segundo plano.

* ** Llamada de retorno para implementar ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Código de evento ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** Significado ** Se detectaron nuevos metadatos temporizados en el flujo de medios.

* ** Llamada de retorno para implementar ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Código de evento ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** Significa ** La línea de tiempo se ha modificado. Es posible que se hayan agregado o eliminado anuncios de la cronología.

* ** Llamada de retorno para implementar ** `onTimelineUpdated(TimelineEvent event)`

* ** Código de evento ** `TIMELINE_UPDATED`