---
description: Puede escuchar las notificaciones y agregar sus propias notificaciones al historial de notificaciones.
title: Configuración del sistema de notificaciones
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Configuración del sistema de notificaciones{#set-up-your-notification-system}

Puede escuchar las notificaciones y agregar sus propias notificaciones al historial de notificaciones.

El núcleo del sistema de notificación del reproductor de Primetime es la clase Notification, que representa una notificación independiente.

La clase NotificationHistory proporciona un mecanismo para acumular notificaciones. Almacena un registro de notificaciones ( `NotificationHistoryItem`) que representa una colección de Notificaciones.

Para recibir notificaciones:

* Escuchar notificaciones
* Añadir notificaciones al historial de notificaciones

1. Escuche los cambios de estado.
1. Implementación de `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` detector de eventos.
1. TVSDK pasa un `MediaPlayer.StatusChangeEvent` al detector de eventos, que contiene dos parámetros:

   * El nuevo estado ( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` objeto
