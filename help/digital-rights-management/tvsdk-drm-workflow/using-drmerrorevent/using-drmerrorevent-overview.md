---
seo-title: Información general sobre el uso de la clase DRMErrorEvent
title: Información general sobre el uso de la clase DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Uso de la información general de la clase DRMErrorEvent {#using-the-drmerrorevent-class-overview}

Primetime distribuye un objeto `DRMErrorEvent` cuando un objeto Primetime, al intentar reproducir contenido protegido, encuentra un error [relacionado con DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Si las credenciales de usuario no son válidas, el objeto `DRMAuthenticateEvent` se distribuye repetidamente hasta que el usuario introduce credenciales válidas o la aplicación deniega más intentos. La aplicación es responsable de escuchar cualquier otro evento de error de DRM para detectar, identificar y manejar los [errores relacionados con DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Incluso con credenciales de usuario válidas, los términos de la licencia del contenido pueden impedir que un usuario vea el contenido cifrado. Por ejemplo, se puede denegar el acceso a un usuario para intentar vista de contenido en una aplicación no autorizada (por ejemplo, la lista de permitidos de la aplicación). Una aplicación no autorizada es aquella que no se ha firmado con un certificado de firma de solicitudes permitido que figure en la lista. En este caso, se distribuye un objeto `DRMErrorEvent`.

Los eventos de error también se pueden activar si el contenido está dañado o si la versión de la aplicación no coincide con lo especificado por la licencia. La aplicación debe proporcionar un mecanismo adecuado para controlar los errores.
