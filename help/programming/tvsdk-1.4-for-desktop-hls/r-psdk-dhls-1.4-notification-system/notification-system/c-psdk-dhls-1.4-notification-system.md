---
description: Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
title: Notificaciones del estado, la actividad, los errores y el registro del reproductor
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Información general {#notifications-for-player-status-activity-errors-and-logging-overview}

Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la información de notificación y estado. También puede crear un sistema de registro para diagnósticos y validación mediante la información de notificación.

Los oyentes de eventos se implementan para capturar y responder a eventos. Muchos eventos proporcionan notificaciones de estado `MediaPlayerNotification`.