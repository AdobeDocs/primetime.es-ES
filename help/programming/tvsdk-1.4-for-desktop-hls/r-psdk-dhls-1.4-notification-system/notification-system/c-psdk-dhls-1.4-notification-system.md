---
description: Los objetos MediaPlayerNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-description: Los objetos MediaPlayerNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-title: Notificaciones de estado, actividad, errores y registro del reproductor
title: Notificaciones de estado, actividad, errores y registro del reproductor
uuid: 7ce5bed0-f312-437e-a82f-b1d4a8e1926c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Información general {#notifications-for-player-status-activity-errors-and-logging-overview}

Los objetos MediaPlayerNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la notificación y la información de estado. También puede crear un sistema de registro para diagnósticos y validación mediante la información de notificación.

Los oyentes de eventos se implementan para capturar y responder a los eventos. Muchos eventos proporcionan notificaciones `MediaPlayerNotification` de estado.