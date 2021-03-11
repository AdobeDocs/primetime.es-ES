---
description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que los problemas para registrar y depurar.
title: Clases de notificación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Clases de notificación {#notification-classes}

Estas clases describen mensajes sobre errores, advertencias y algunas actividades que los problemas para registrar y depurar.

Paquete: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Nombre de la clase | Descripción |
|---|---|
| [Notificación](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objetos de un solo evento de notificación dentro de [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Devuelve la descripción asociada al código de notificación proporcionado y proporciona constantes numéricas para los objetos de notificación. |
| [Historial de notificaciones](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | Clase que almacena un registro de objetos de notificación. Lista circular de objetos [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada elemento contiene una instancia separada de la clase [Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html). |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | Clase que define una entrada en la lista circular de [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) y que contiene la notificación y su marca de tiempo. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | Clase que contiene los tipos de notificaciones admitidos. |

