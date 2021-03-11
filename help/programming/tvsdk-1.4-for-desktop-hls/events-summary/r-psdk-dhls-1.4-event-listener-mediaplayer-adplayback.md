---
description: TVSDK envía eventos de reproducción de anuncios en respuesta a operaciones relacionadas con anuncios, como cuando se comienza a reproducir un anuncio.
title: Eventos de reproducción de anuncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Eventos de reproducción de anuncio {#ad-playback-events}

TVSDK envía eventos de reproducción de anuncios en respuesta a operaciones relacionadas con anuncios, como cuando se comienza a reproducir un anuncio.

Para recibir notificaciones sobre todos los eventos relacionados con la reproducción de publicidad, registre los oyentes con el objeto `MediaPlayer` para los eventos siguientes.

>[!TIP]
>
>Cuando los anuncios se insertan o eliminan del contenido, TVSDK distribuye el evento de reproducción TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significado |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Se ha reproducido completamente una pausa publicitaria. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Se omitió una pausa publicitaria durante la reproducción. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | Se ha iniciado una pausa publicitaria. |
| AdClickEvent.[AD_CLICK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | El usuario ha hecho clic en la publicidad. Proporciona información a la aplicación sobre la publicidad en la que hizo clic el usuario, en respuesta a la llamada `notifyClick` de la `MediaPlayerView` aplicación. |
| AdPlaybackEvent.[ANUNCIO _FINALIZADO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Un anuncio se ha reproducido completamente. |
| AdPlaybackEvent.[AD_PROGRESS](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | La reproducción del anuncio ha progresado. Se envía varias veces mientras se reproduce un anuncio. |
| AdPlaybackEvent.[AD_SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Se ha producido una búsqueda a través de límites de anuncios o dentro de un anuncio. |
| AdPlaybackEvent.[AD_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Se ha iniciado un anuncio. |