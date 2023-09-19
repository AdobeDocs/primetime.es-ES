---
description: TVSDK envía eventos de reproducción de publicidad en respuesta a operaciones relacionadas con la publicidad, como cuando comienza a reproducirse un anuncio.
title: Eventos de reproducción de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Eventos de reproducción de publicidad {#ad-playback-events}

TVSDK envía eventos de reproducción de publicidad en respuesta a operaciones relacionadas con la publicidad, como cuando comienza a reproducirse un anuncio.

Para recibir notificaciones acerca de todos los eventos relacionados con la reproducción de anuncios, registre los oyentes en `MediaPlayer` para los eventos siguientes.

>[!TIP]
>
>Cuando se insertan anuncios en los medios o se eliminan de ellos, TVSDK envía el evento de reproducción TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significado |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Se ha reproducido una pausa publicitaria por completo. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Se ha omitido una pausa publicitaria durante la reproducción. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | Ha comenzado una pausa publicitaria. |
| Evento de clic.[_CLIC EN PUBLICIDAD](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | El usuario ha hecho clic en el anuncio. Proporciona información a la aplicación sobre el anuncio en el que hizo clic el usuario en respuesta a la llamada de la aplicación `notifyClick` en el `MediaPlayerView`. |
| AdPlaybackEvent.[ANUNCIO _COMPLETADO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Se ha reproducido un anuncio por completo. |
| AdPlaybackEvent.[_PROGRESO DEL ANUNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | La reproducción del anuncio ha progresado. Se envía varias veces mientras se reproduce un anuncio. |
| AdPlaybackEvent.[AD_SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Se ha producido una búsqueda a través de los límites de un anuncio o dentro de un anuncio. |
| AdPlaybackEvent.[AD _INICIADA](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Se ha iniciado un anuncio. |
