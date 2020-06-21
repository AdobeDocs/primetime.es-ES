---
seo-title: Información general sobre el uso de la clase DRMErrorEvent
title: Información general sobre el uso de la clase DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Uso de la clase DRMErrorEvent {#using-the-drmerrorevent-class}

Primetime distribuye un `DRMErrorEvent` objeto cuando un objeto Primetime, al intentar reproducir contenido protegido, encuentra un error [relacionado con](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM. Si las credenciales de usuario no son válidas, el `DRMAuthenticateEvent` objeto se distribuye repetidamente hasta que el usuario introduce credenciales válidas o la aplicación deniega más intentos. La aplicación es responsable de escuchar cualquier otro evento de error de DRM para detectar, identificar y controlar los errores [relacionados con](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM.

Incluso con credenciales de usuario válidas, los términos de la licencia del contenido pueden impedir que un usuario vea el contenido cifrado. Por ejemplo, se puede denegar el acceso a un usuario para intentar vista de contenido en una aplicación no autorizada (por ejemplo, la lista de permitidos de la aplicación). Una aplicación no autorizada es aquella que no se ha firmado con un certificado de firma de solicitudes permitido que figure en la lista. En este caso, se distribuye un `DRMErrorEvent` objeto.

Los eventos de error también se pueden activar si el contenido está dañado o si la versión de la aplicación no coincide con lo especificado por la licencia. La aplicación debe proporcionar un mecanismo adecuado para controlar los errores.

## Creación de un controlador DRMErrorEvent {#create-a-drmerrorevent-handler}

Cree un controlador de evento para procesar los eventos de error enviados desde Primetime cuando detecte un error al intentar reproducir contenido protegido.

Normalmente, cuando una aplicación encuentra un error, realiza cualquier número de tareas de limpieza. A continuación, informa al usuario del error y proporciona opciones para resolverlo.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
