---
description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que el SDK emite para fines de registro y depuración.
title: Clases de notificación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Clases de notificación{#notification-classes}

Estas clases describen mensajes sobre errores, advertencias y algunas actividades que el SDK emite para fines de registro y depuración.

| Nombre de la clase | Descripción |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Clase que describe la notificación de un error que hace que el reproductor detenga la reproducción. Se trata de una [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) del tipo de notificación ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Enumera todas las notificaciones enviadas por el marco de Primetime Player. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objetos de un solo evento de notificación dentro de [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Clase que almacena un registro de objetos de notificación [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada elemento contiene una instancia separada de [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Clase que define una entrada en la lista circular de [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) y que contiene la notificación y su marca de tiempo. |

