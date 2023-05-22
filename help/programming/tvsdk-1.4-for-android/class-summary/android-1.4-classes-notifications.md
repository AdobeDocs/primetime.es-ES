---
description: Estas clases describen mensajes acerca de errores, advertencias y algunas actividades que TVSDK emite con fines de registro y depuración.
title: Clases de notificación
exl-id: b869c201-2731-42e5-a20e-282edd2caddc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Clases de notificación{#notification-classes}

Estas clases describen mensajes acerca de errores, advertencias y algunas actividades que TVSDK emite con fines de registro y depuración.

Paquete: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)  Paquete: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| Nombre de clase | Descripción |
|---|---|
| MediaPlayerNotification. [Error](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | Clase que describe la notificación de un error que hace que el reproductor detenga la reproducción. Este es un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) del tipo de notificación ERROR. |
| MediaPlayerNotification. [Información](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | Clase que describe una notificación informativa. Este es un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) de tipo de notificación INFO. |
| MediaPlayerNotification. [Advertencia](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | Clase que describe una notificación de advertencia. Este es un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) de tipo de notificación ADVERTENCIA. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | Clase que proporciona mensajes informativos, advertencias y errores. Encapsula la representación de objeto de un único evento de notificación dentro de [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | Devuelve la descripción asociada con el código de notificación proporcionado. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | Clase que almacena un registro de objetos de notificación. Una lista circular de [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) que proporciona acceso a una lista del historial de eventos de notificación. Es decir, mantiene una lista de elementos, cada uno de los cuales contiene una instancia independiente de [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) clase. (Entrada [sesión](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) paquete.) |
| Historial de notificaciones. [Elemento](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | Clase que define una entrada en la lista circular de [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) y contiene la notificación y su marca de tiempo. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | Clase que contiene los tipos de notificaciones compatibles. |
