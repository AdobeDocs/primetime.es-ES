---
description: TVSDK distribuye eventos de reproducción de anuncios en respuesta a operaciones relacionadas con los anuncios, como cuando se reproduce un inicio publicitario.
seo-description: TVSDK distribuye eventos de reproducción de anuncios en respuesta a operaciones relacionadas con los anuncios, como cuando se reproduce un inicio publicitario.
seo-title: Eventos de reproducción de publicidad
title: Eventos de reproducción de publicidad
uuid: 63138237-2315-45ff-914d-369da18fdff7
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Eventos de reproducción de publicidad {#ad-playback-events}

TVSDK distribuye eventos de reproducción de anuncios en respuesta a operaciones relacionadas con los anuncios, como cuando se reproduce un inicio publicitario.

Para recibir notificaciones sobre todos los eventos relacionados con la reproducción de publicidad, registre los oyentes con el objeto `MediaPlayer` para los siguientes eventos.

>[!TIP]
>
>Cuando se insertan o eliminan anuncios del medio, TVSDK distribuye el evento de reproducción TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significado |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Una pausa publicitaria se ha reproducido completamente. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Se omitió una pausa publicitaria durante la reproducción. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | Se ha iniciado una pausa publicitaria. |
| AdClickEvent.[PUBLICAR _CLIC](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | El usuario ha hecho clic en la publicidad. Proporciona información a la aplicación sobre la publicidad en la que el usuario hizo clic, en respuesta a la llamada de la aplicación `notifyClick` en el `MediaPlayerView`. |
| AdPlaybackEvent.[ANUNCIO _COMPLETADO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Un anuncio se ha reproducido completamente. |
| AdPlaybackEvent.[AD_PROGRESS](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | La reproducción del anuncio ha progresado. Se distribuye varias veces mientras se reproduce un anuncio. |
| AdPlaybackEvent.[AD_SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Se ha producido una búsqueda a través de los límites de la publicidad o dentro de una publicidad. |
| AdPlaybackEvent.[_INICIO DE PUBLICIDAD](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Se ha iniciado una publicidad. |