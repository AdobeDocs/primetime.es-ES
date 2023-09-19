---
description: Estas clases describen mensajes acerca de errores, advertencias y algunas actividades que TVSDK emite con fines de registro y depuración.
title: Clases de notificación
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Clases de notificación{#notification-classes}

Estas clases describen mensajes acerca de errores, advertencias y algunas actividades que TVSDK emite con fines de registro y depuración.

| Nombre de clase | Descripción |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Clase que describe la notificación de un error que hace que el reproductor detenga la reproducción. Este es un [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) del tipo de notificación ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Enumera todas las notificaciones enviadas por el marco de trabajo del reproductor de Primetime. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objeto de un único evento de notificación dentro de [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Clase que almacena un registro de objetos de notificación [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada uno de los cuales contiene una instancia independiente de [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Clase que define una entrada en la lista circular de [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) y contiene la notificación y su marca de tiempo. |
