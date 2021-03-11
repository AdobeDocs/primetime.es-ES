---
description: Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.
title: Configurar el sistema de notificaciones
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Configurar el sistema de notificaciones{#set-up-your-notification-system}

Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.

El núcleo del sistema de notificación de Primetime Player es la clase `Notification`, que representa una notificación independiente.

La clase `NotificationHistory` proporciona un mecanismo para acumular notificaciones. Almacena un registro de objetos Notification (NotificationHistoryItem) que representa una colección de Notificaciones.

Para recibir notificaciones:

* Escuchar notificaciones
* Añadir notificaciones al historial de notificaciones

1. Escuche los cambios de estado.
1. Implemente la llamada de retorno `MediaPlayer.PlaybackEventListener.onStateChanged`.
1. TVSDK pasa dos parámetros a la rellamada:

   * El nuevo estado ( `MediaPlayer.PlayerState`)
   * Un objeto `MediaPlayerNotification`

