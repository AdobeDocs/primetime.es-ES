---
description: Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
title: Notificaciones de estado del reproductor, actividad, errores y registro
exl-id: cce634aa-5394-46c0-a031-70d6fc1b754b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Información general {#notifications-for-player-status-activity-errors-and-logging-overview}

Los objetos MediaPlayerNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la información de notificación y estado. También puede crear un sistema de registro para diagnósticos y validación utilizando la información de notificación.

Los oyentes de eventos se implementan para capturar eventos y responder a ellos. Muchos eventos proporcionan `MediaPlayerNotification` notificaciones de estado.
