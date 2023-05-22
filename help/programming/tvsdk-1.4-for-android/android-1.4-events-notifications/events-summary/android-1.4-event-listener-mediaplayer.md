---
description: TVSDK envía eventos de reproducción de publicidad en respuesta a operaciones relacionadas con la publicidad, como cuando comienza a reproducirse un anuncio.
title: Eventos de reproducción de publicidad
exl-id: f35e3c6f-1d58-4498-9e3b-cbd53e573ef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Eventos de reproducción de publicidad{#ad-playback-events}

TVSDK envía eventos de reproducción de publicidad en respuesta a operaciones relacionadas con la publicidad, como cuando comienza a reproducirse un anuncio.

Para recibir notificaciones acerca de todos los eventos relacionados con la reproducción de anuncios, registre una implementación de `MediaPlayer.AdPlaybackEventListener` incluyendo las siguientes llamadas de retorno.

>[!TIP]
>
>Cuando se insertan o eliminan anuncios de los medios, TVSDK envía el evento de reproducción [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significado |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Se ha reproducido una pausa publicitaria por completo. |
| onAdBreakSkipped | Se ha omitido una pausa publicitaria durante la reproducción. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Ha comenzado una pausa publicitaria. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, Ad ad, AdClick adClick) | El usuario ha hecho clic en el anuncio. Proporciona información a la aplicación sobre el anuncio en el que hizo clic el usuario en respuesta a la llamada de la aplicación `notifyClick` en el `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, anuncio de publicidad) | Se ha reproducido un anuncio por completo. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, Ad ad ad, int porcentaje) | La reproducción del anuncio ha progresado. Se envía varias veces mientras se reproduce un anuncio. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, anuncio de publicidad) | Se ha iniciado un anuncio. |
