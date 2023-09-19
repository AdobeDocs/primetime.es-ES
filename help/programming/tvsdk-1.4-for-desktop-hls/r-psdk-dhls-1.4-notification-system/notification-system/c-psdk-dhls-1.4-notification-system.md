---
description: Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
title: Notificaciones de estado del reproductor, actividad, errores y registro
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Información general {#notifications-for-player-status-activity-errors-and-logging-overview}

Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la información de notificación y estado. También puede crear un sistema de registro para diagnósticos y validación utilizando la información de notificación.

Los oyentes de eventos se implementan para capturar eventos y responder a ellos. Muchos eventos proporcionan `MediaPlayerNotification` notificaciones de estado.
