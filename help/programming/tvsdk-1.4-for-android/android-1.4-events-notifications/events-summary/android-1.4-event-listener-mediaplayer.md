---
description: TVSDK envía eventos de reproducción de anuncios en respuesta a operaciones relacionadas con anuncios, como cuando se comienza a reproducir un anuncio.
title: Eventos de reproducción de anuncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Eventos de reproducción de anuncio{#ad-playback-events}

TVSDK envía eventos de reproducción de anuncios en respuesta a operaciones relacionadas con anuncios, como cuando se comienza a reproducir un anuncio.

Para recibir notificaciones sobre todos los eventos relacionados con la reproducción de publicidad, registre una implementación de `MediaPlayer.AdPlaybackEventListener` que incluya las siguientes llamadas de retorno.

>[!TIP]
>
>Cuando los anuncios se insertan o eliminan del contenido, TVSDK envía el evento de reproducción [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significado |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak) | Se ha reproducido completamente una pausa publicitaria. |
| onAdBreakSkipped | Se omitió una pausa publicitaria durante la reproducción. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak) | Se ha iniciado una pausa publicitaria. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick))  (AdBreak adBreak, anuncio, AdClick adClick) | El usuario ha hecho clic en la publicidad. Proporciona información a la aplicación sobre la publicidad en la que hizo clic el usuario, en respuesta a la llamada `notifyClick` de la `MediaPlayerView` aplicación. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak, anuncio) | Un anuncio se ha reproducido completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int))  (AdBreak adBreak, anuncio, porcentaje int) | La reproducción del anuncio ha progresado. Se envía varias veces mientras se reproduce un anuncio. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad))  (AdBreak adBreak, anuncio) | Se ha iniciado un anuncio. |