---
description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que TVSDK emite para fines de registro y depuración.
seo-description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que TVSDK emite para fines de registro y depuración.
seo-title: Clases de notificación
title: Clases de notificación
uuid: 8a276056-775f-432d-a4b4-722f6e4e278f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# Clases de notificación {#notification-classes}

Estas clases describen mensajes sobre errores, advertencias y algunas actividades que TVSDK emite para fines de registro y depuración.

| **Nombre de clase** | **Descripción** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Clase que describe la notificación de un error que hace que el reproductor detenga la reproducción. Se trata de una [notificación de PTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) del tipo de notificación ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Lista todas las notificaciones enviadas por el módulo de Primetime Player. |
| [Notificación PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objetos de un solo evento de notificación dentro de [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Clase que almacena un registro de objetos de notificación [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada elemento contiene una instancia separada de [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Clase que define una entrada en la lista circular en [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) y que contiene la notificación y su marca de tiempo. |

