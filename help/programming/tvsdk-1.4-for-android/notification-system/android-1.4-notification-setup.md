---
description: Puede escuchar las notificaciones y agregar sus propias notificaciones al historial de notificaciones.
title: Configuración del sistema de notificaciones
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Configuración del sistema de notificaciones{#set-up-your-notification-system}

Puede escuchar las notificaciones y agregar sus propias notificaciones al historial de notificaciones.

El núcleo del sistema de notificación del reproductor de Primetime es el `Notification` , que representa una notificación independiente.

El `NotificationHistory` proporciona un mecanismo para acumular notificaciones. Almacena un registro de objetos notification (NotificationHistoryItem) que representa una colección de Notificaciones.

Para recibir notificaciones:

* Escuchar notificaciones
* Añadir notificaciones al historial de notificaciones

1. Escuche los cambios de estado.
1. Implementación de `MediaPlayer.PlaybackEventListener.onStateChanged` devolución de llamada.
1. TVSDK pasa dos parámetros a la llamada de retorno:

   * El nuevo estado ( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` objeto

