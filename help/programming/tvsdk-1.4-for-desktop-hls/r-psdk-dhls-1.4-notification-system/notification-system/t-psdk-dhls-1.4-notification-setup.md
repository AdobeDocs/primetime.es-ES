---
description: Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.
seo-description: Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.
seo-title: Configurar el sistema de notificaciones
title: Configurar el sistema de notificaciones
uuid: 2d1876c7-4ce6-491c-880b-dd94697d4feb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Configure el sistema de notificaciones{#set-up-your-notification-system}

Puede escuchar notificaciones y agregar sus propias notificaciones al historial de notificaciones.

El núcleo del sistema de notificaciones de Primetime Player es la clase Notification, que representa una notificación independiente.

La clase NotificationHistory proporciona un mecanismo para la acumulación de notificaciones. Almacena un registro de objetos de notificación ( `NotificationHistoryItem`) que representa una colección de Notificaciones.

Para recibir notificaciones:

* Escuchar notificaciones
* Añadir notificaciones al historial de notificaciones

1. Escuche los cambios de estado.
1. Implementar el detector de evento `MediaPlayer.StatusChangeEvent.STATUS_CHANGED`.
1. TVSDK pasa una instancia `MediaPlayer.StatusChangeEvent` al detector de evento, que contiene dos parámetros:

   * El nuevo estado ( `MediaPlayer.Status`)
   * Un objeto `MediaPlayerNotification`

