---
description: La aplicación puede monitorizar la actividad del reproductor y su estado cambiando al escuchar los eventos que envía TVSDK.
title: Resumen de eventos del reproductor Primetime
exl-id: 42489abe-ccaf-4b40-bb4b-de8547b5585a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Resumen de eventos del reproductor Primetime {#primetime-player-events-summary-overview}

La aplicación puede monitorizar la actividad del reproductor y su estado cambiando al escuchar los eventos que envía TVSDK.

## Eventos {#events}

TVSDK le avisa cuando se producen eventos, a los que la aplicación debe responder. Cada evento corresponde a una clase de agente de escucha, con un método de devolución de llamada que debe implementar.

>[!TIP]
>
>Los códigos de evento son las constantes de `MediaPlayerEvent` enum.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** Significado ** La reproducción de la pausa publicitaria ha finalizado.

* ** Callback para implementar ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** código de evento ** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** Significado ** Se ha omitido una pausa publicitaria durante la reproducción.

* ** Callback para implementar ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** código de evento ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** Significado ** ha comenzado la reproducción de la pausa publicitaria.

* ** Callback para implementar ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** código de evento ** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** Significado ** se hizo clic en un anuncio durante la reproducción.

* ** Callback para implementar ** `onAdClicked(AdClickEvent event)`

* ** código de evento ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** Significado ** La reproducción del anuncio ha finalizado.

* ** Callback para implementar ** `onAdCompleted(AdPlaybackEvent event)`

* ** código de evento ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** Significado ** informar del progreso durante la reproducción.

* ** Callback para implementar ** `onAdProgress(AdPlaybackEvent event)`

* ** código de evento ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Significa ** se ha completado Primetime y la toma de decisiones y resolución. Este evento solo se aplica al contenido de VOD.

* ** Callback para implementar ** `onAdResolutionComplete()`

* ** código de evento ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** Significado ** ha comenzado la reproducción del anuncio.

* ** Callback para implementar ** `onAdStarted(AdPlaybackEvent event)`

* ** código de evento ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** Significado ** Se ha detectado una nueva pista de audio.

* ** Callback para implementar ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** código de evento ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** Significado ** El reproductor ha comenzado el almacenamiento en búfer.

* ** Callback para implementar ** `onBufferingBegin(BufferEvent event)`

* ** código de evento ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** Significado ** el reproductor ha dejado de almacenar en búfer.

* ** Callback para implementar ** `onBufferingEnd(BufferEvent event)`

* ** código de evento ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** Significado ** el búfer está preparado.

* ** Callback para implementar ** `onBufferPrepared()`

* ** código de evento ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** Significado ** Se ha detectado un nuevo seguimiento de subtítulos.

* ** Callback para implementar ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** código de evento ** `CAPTIONS_UPDATED`

## DTMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** Significado ** Se ha detectado un nuevo metadato DRM en el flujo de medios.

* ** Callback para implementar ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** código de evento ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** Significado ** Se ha creado un nuevo elemento del reproductor de contenidos.

* ** Callback para implementar ** `onItemCreated(MediaPlayerItemEvent event)`

* ** código de evento ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** Significado ** se ha creado nueva información de carga para el elemento actual.

* ** Callback para implementar ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** código de evento ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** Significado ** Se ha cargado un nuevo segmento.

* ** Callback para implementar ** `onLoadInformation(LoadInformationEvent event)`

* ** código de evento ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** Significado ** Se ha actualizado el manifiesto principal o la lista de reproducción.

* ** Callback para implementar ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** código de evento ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** Significado ** la operación ha fallado.

* ** Callback para implementar ** `onNotification(NotificationEvent event)`

* ** código de evento ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** Significado ** Se ha actualizado el intervalo de reproducción.

* ** Callback para implementar ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** código de evento ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** Significado ** Una nueva velocidad de reproducción es visible en la pantalla.

* ** Callback para implementar ** `onRatePlaying(PlaybackRateEvent event)`

* ** código de evento ** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** Significado ** se ha establecido el atributo rate de MediaPlayer.

* ** Callback para implementar ** `onRateSelected(PlaybackRateEvent event)`

* ** código de evento ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** Significado ** que la reproducción ha comenzado.

* ** Callback para implementar ** `onPlayStart()`

* ** código de evento ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** Significado ** El perfil actual de MediaPlayer ha cambiado.

* ** Callback para implementar ** `onProfileChanged(ProfileEvent event)`

* ** código de evento ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** Significado ** la reproducción alcanzó una reserva de cronología.

* ** Callback para implementar ** `onReservationReached(ReservationEvent event)`

* ** código de evento ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** Significa que ** operación Seek se ha iniciado.

* ** Callback para implementar ** `onSeekBegin(SeekEvent event)`

* ** código de evento ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** Significado ** La operación de búsqueda ha finalizado.

* ** Callback para implementar ** `onSeekEnd(SeekEvent event)`

* ** código de evento ** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** Significado ** La posición de búsqueda se ha ajustado debido a reglas de reproducción internas o reglas comerciales externas.

* ** Callback para implementar ** `onPositionAdjusted(SeekEvent event)`

* ** código de evento ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** Significado ** El tamaño del medio está disponible.

* ** Callback para implementar ** `onSizeAvailable(SizeAvailableEvent event)`

* ** código de evento ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** Significado ** El estado de MediaPlayer ha cambiado.

* ** Callback para implementar ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** código de evento ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** Significado ** El cabezal de reproducción ha cambiado.

* ** Callback para implementar ** `onTimeChanged(TimeChangeEvent event)`

* ** código de evento ** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** Significado ** La operación se completa con el tiempo necesario para la operación.

* ** Callback para implementar ** `onTimedEvent(TimedEventEvent event)`

* ** código de evento ** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** Significado ** Se han agregado nuevos metadatos cronometrados a un elemento en segundo plano.

* ** Callback para implementar ** `onTimedMetadata(TimedMetadataEvent event)`

* ** código de evento ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** Significado ** Se ha detectado un nuevo metadato cronometrado en el flujo de medios.

* ** Callback para implementar ** `onTimedMetadata(TimedMetadataEvent event)`

* ** código de evento ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** Significado ** Se ha modificado la cronología. Es posible que se hayan agregado o eliminado anuncios de la cronología.

* ** Callback para implementar ** `onTimelineUpdated(TimelineEvent event)`

* ** código de evento ** `TIMELINE_UPDATED`
