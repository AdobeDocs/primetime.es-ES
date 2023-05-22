---
title: Información general sobre el uso de la clase DRMErrorEvent
description: Información general sobre el uso de la clase DRMErrorEvent
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Información general sobre el uso de la clase DRMErrorEvent {#using-the-drmerrorevent-class-overview}

Primetime envía un `DRMErrorEvent` cuando un objeto de Primetime, al intentar reproducir contenido protegido, encuentra un objeto [Error relacionado con DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Si las credenciales de usuario no son válidas, la variable `DRMAuthenticateEvent` se envía repetidamente hasta que el usuario introduce credenciales válidas o la aplicación rechaza nuevos intentos. La aplicación es responsable de escuchar cualquier otro evento de error DRM para detectar, identificar y gestionar el [Errores relacionados con DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Incluso con credenciales de usuario válidas, los términos de la licencia del contenido pueden impedir que un usuario vea el contenido cifrado. Por ejemplo, se puede denegar el acceso a un usuario por intentar ver contenido en una aplicación no autorizada (por ejemplo, la lista de aplicaciones permitidas). Una aplicación no autorizada es aquella que no se ha firmado con un certificado de firma de aplicación incluido en la lista de permitidos. En este caso, una `DRMErrorEvent` el objeto está distribuido.

Los eventos de error también se pueden activar si el contenido está dañado o si la versión de la aplicación no coincide con lo especificado en la licencia. La aplicación debe proporcionar un mecanismo adecuado para gestionar los errores.
