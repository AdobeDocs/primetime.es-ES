---
description: TVSDK distribuye eventos de reproducción de anuncios en respuesta a operaciones relacionadas con los anuncios, como cuando se reproduce un inicio publicitario.
seo-description: TVSDK distribuye eventos de reproducción de anuncios en respuesta a operaciones relacionadas con los anuncios, como cuando se reproduce un inicio publicitario.
seo-title: Eventos de reproducción de publicidad
title: Eventos de reproducción de publicidad
uuid: dd6991ae-3e33-4d92-92e9-26b1086a555a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Eventos de reproducción de publicidad{#ad-playback-events}

TVSDK distribuye eventos de reproducción de anuncios en respuesta a operaciones relacionadas con los anuncios, como cuando se reproduce un inicio publicitario.

Para recibir notificaciones sobre todos los eventos relacionados con la reproducción de publicidad, registre una implementación de `MediaPlayer.AdPlaybackEventListener` incluyendo las siguientes rellamadas.

>[!TIP]
>
>Cuando se insertan o eliminan anuncios del medio, TVSDK distribuye el evento de reproducción [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significado |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Una pausa publicitaria se ha reproducido completamente. |
| onAdBreakSkipped | Se omitió una pausa publicitaria durante la reproducción. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Se ha iniciado una pausa publicitaria. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, anuncio, AdClick adClick) | El usuario ha hecho clic en la publicidad. Proporciona información a la aplicación sobre la publicidad en la que el usuario hizo clic, en respuesta a la llamada de la aplicación `notifyClick` en el `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, anuncio) | Un anuncio se ha reproducido completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, anuncio, porcentaje int) | La reproducción del anuncio ha progresado. Se distribuye varias veces mientras se reproduce un anuncio. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, anuncio) | Se ha iniciado una publicidad. |