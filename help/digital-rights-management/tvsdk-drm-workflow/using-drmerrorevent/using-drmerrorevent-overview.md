---
seo-title: Información general sobre el uso de la clase DRMErrorEvent
title: Información general sobre el uso de la clase DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Información general sobre el uso de la clase DRMErrorEvent {#using-the-drmerrorevent-class-overview}

Primetime distribuye un `DRMErrorEvent` objeto cuando un objeto Primetime, al intentar reproducir contenido protegido, encuentra un error [relacionado con](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM. Si las credenciales de usuario no son válidas, el `DRMAuthenticateEvent` objeto se distribuye repetidamente hasta que el usuario introduce credenciales válidas o la aplicación deniega más intentos. La aplicación es responsable de escuchar cualquier otro evento de error de DRM para detectar, identificar y controlar los errores [relacionados con](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM.

Incluso con credenciales de usuario válidas, los términos de la licencia del contenido pueden impedir que un usuario vea el contenido cifrado. Por ejemplo, se puede denegar el acceso a un usuario para intentar ver contenido en una aplicación no autorizada (por ejemplo, la lista blanca de la aplicación). Una aplicación no autorizada es aquella que no se ha firmado con un certificado de firma de aplicación de la lista blanca. En este caso, se distribuye un `DRMErrorEvent` objeto.

Los eventos de error también se pueden activar si el contenido está dañado o si la versión de la aplicación no coincide con lo especificado por la licencia. La aplicación debe proporcionar un mecanismo adecuado para controlar los errores.
