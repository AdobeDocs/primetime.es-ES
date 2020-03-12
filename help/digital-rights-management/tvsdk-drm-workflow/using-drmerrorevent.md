---
seo-title: Información general sobre el uso de la clase DRMErrorEvent
title: Información general sobre el uso de la clase DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Uso de la clase DRMErrorEvent {#using-the-drmerrorevent-class}

Primetime distribuye un `DRMErrorEvent` objeto cuando un objeto Primetime, al intentar reproducir contenido protegido, encuentra un error [relacionado con](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM. Si las credenciales de usuario no son válidas, el `DRMAuthenticateEvent` objeto se distribuye repetidamente hasta que el usuario introduce credenciales válidas o la aplicación deniega más intentos. La aplicación es responsable de escuchar cualquier otro evento de error de DRM para detectar, identificar y controlar los errores [relacionados con](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM.

Incluso con credenciales de usuario válidas, los términos de la licencia del contenido pueden impedir que un usuario vea el contenido cifrado. Por ejemplo, se puede denegar el acceso a un usuario para intentar ver contenido en una aplicación no autorizada (por ejemplo, la lista blanca de la aplicación). Una aplicación no autorizada es aquella que no se ha firmado con un certificado de firma de aplicación de la lista blanca. En este caso, se distribuye un `DRMErrorEvent` objeto.

Los eventos de error también se pueden activar si el contenido está dañado o si la versión de la aplicación no coincide con lo especificado por la licencia. La aplicación debe proporcionar un mecanismo adecuado para controlar los errores.

## Creación de un controlador DRMErrorEvent {#create-a-drmerrorevent-handler}

Cree un controlador de eventos para procesar los eventos de error enviados desde Primetime cuando detecte un error al intentar reproducir contenido protegido.

Normalmente, cuando una aplicación encuentra un error, realiza cualquier cantidad de tareas de limpieza. A continuación, informa al usuario del error y proporciona opciones para resolverlo.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
