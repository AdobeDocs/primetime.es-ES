---
description: Estas clases describen mensajes acerca de errores, advertencias y algunas actividades que causan problemas con fines de registro y depuración.
title: Clases de notificación
exl-id: d8af783f-1e80-4e50-89b8-97643ff6670b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Clases de notificación {#notification-classes}

Estas clases describen mensajes acerca de errores, advertencias y algunas actividades que causan problemas con fines de registro y depuración.

Paquete: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Nombre de clase | Descripción |
|---|---|
| [Notificación](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objeto de un único evento de notificación dentro de [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Devuelve la descripción asociada al código de notificación proporcionado y proporciona constantes numéricas para los objetos de notificación. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | Clase que almacena un registro de objetos de notificación. Una lista circular de [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada uno de los cuales contiene una instancia independiente de [Notificación](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) clase. |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | Clase que define una entrada en la lista circular de [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) y contiene la notificación y su marca de tiempo. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | Clase que contiene los tipos de notificaciones compatibles. |
