---
description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que TVSDK emite para fines de registro y depuración.
seo-description: Estas clases describen mensajes sobre errores, advertencias y algunas actividades que TVSDK emite para fines de registro y depuración.
seo-title: Clases de notificación
title: Clases de notificación
uuid: e231a2d0-6190-4251-87db-ca46d2aee60d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---


# Clases de notificación{#notification-classes}

Estas clases describen mensajes sobre errores, advertencias y algunas actividades que TVSDK emite para fines de registro y depuración.

Paquete: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) Paquete: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| Nombre de clase | Descripción |
|---|---|
| MediaPlayerNotification. [Error](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | Clase que describe la notificación de un error que hace que el reproductor detenga la reproducción. Es un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) de tipo de notificación ERROR. |
| MediaPlayerNotification. [Información](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | Clase que describe una notificación informativa. Es un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) de tipo de notificación INFO. |
| MediaPlayerNotification. [Advertencia](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | Clase que describe una notificación de advertencia. Es un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) de tipo de notificación ADVERTENCIA. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objetos de un solo evento de notificación dentro de [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | Devuelve la descripción asociada al código de notificación proporcionado. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | Clase que almacena un registro de objetos de notificación. Una lista circular de [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) objetos que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada elemento contiene una instancia separada de la clase [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html). (En el paquete [session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)). |
| NotificationHistory. [Elemento](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | Clase que define una entrada en la lista circular en [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) y que contiene la notificación y su marca de hora. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | Clase que contiene los tipos de notificaciones admitidos. |