---
description: Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.
seo-description: Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.
seo-title: Configurar el sistema de notificaciones
title: Configurar el sistema de notificaciones
uuid: caa6a306-dea9-45ee-b0b3-569b5f2527a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Configurar el sistema de notificaciones{#set-up-your-notification-system}

Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.

El núcleo del sistema de notificaciones de Primetime Player es la `Notification` clase, que representa una notificación independiente.

La `NotificationHistory` clase proporciona un mecanismo para la acumulación de notificaciones. Almacena un registro de objetos de notificación (NotificationHistoryItem) que representa una colección de notificaciones.

Para recibir notificaciones:

* Escuchar notificaciones
* Agregar notificaciones al historial de notificaciones

1. Escuche los cambios de estado.
1. Implemente la `MediaPlayer.PlaybackEventListener.onStateChanged` llamada de retorno.
1. TVSDK pasa dos parámetros a la llamada de retorno:

   * El nuevo estado ( `MediaPlayer.PlayerState`)
   * Un `MediaPlayerNotification` objeto

