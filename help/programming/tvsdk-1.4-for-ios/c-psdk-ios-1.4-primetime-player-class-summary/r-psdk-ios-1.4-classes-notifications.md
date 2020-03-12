---
description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que el TVSDK emite para fines de registro y depuración.
seo-description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que el TVSDK emite para fines de registro y depuración.
seo-title: Clases de notificación
title: Clases de notificación
uuid: 08c29efe-245d-4a6d-80c6-cd561cbf3b5f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Clases de notificación{#notification-classes}

Estas clases describen mensajes sobre errores, advertencias y algunas actividades que el TVSDK emite para fines de registro y depuración.

| Nombre de clase | Descripción |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Clase que describe la notificación de un error que hace que el reproductor detenga la reproducción. Es una notificación [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) del tipo de notificación ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Enumera todas las notificaciones enviadas por el módulo de Primetime Player. |
| [Notificación PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objetos de un solo evento de notificación dentro de [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Clase que almacena un registro de objetos de notificación [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada elemento contiene una instancia separada de la notificación [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Clase que define una entrada en la lista circular de [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) y que contiene la notificación y su marca de tiempo. |

