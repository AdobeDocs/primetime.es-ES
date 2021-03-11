---
title: Información general sobre el uso de la clase DRMErrorEvent
description: Información general sobre el uso de la clase DRMErrorEvent
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Uso de la clase DRMErrorEvent {#using-the-drmerrorevent-class}

Primetime distribuye un objeto `DRMErrorEvent` cuando un objeto Primetime, al intentar reproducir contenido protegido, encuentra un [error relacionado con DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Si las credenciales de usuario no son válidas, el objeto `DRMAuthenticateEvent` se envía varias veces hasta que el usuario introduce credenciales válidas o la aplicación deniega más intentos. La aplicación es responsable de escuchar cualquier otro evento de error de DRM para detectar, identificar y gestionar los [errores relacionados con DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Incluso con credenciales de usuario válidas, los términos de la licencia del contenido aún pueden impedir que un usuario vea el contenido cifrado. Por ejemplo, se puede denegar el acceso a un usuario si intenta ver contenido en una aplicación no autorizada (por ejemplo, la lista de permitidos de la aplicación). Una aplicación no autorizada es aquella que no se ha firmado con un certificado de firma de aplicación incluido en la lista de permitidos. En este caso, se envía un objeto `DRMErrorEvent`.

Los eventos de error también se pueden activar si el contenido está dañado o si la versión de la aplicación no coincide con lo que especifica la licencia. La aplicación debe proporcionar un mecanismo adecuado para controlar los errores.

## Crear un controlador DRMErrorEvent {#create-a-drmerrorevent-handler}

Cree un controlador de eventos para procesar eventos de error distribuidos desde Primetime cuando detecte un error al intentar reproducir contenido protegido.

Normalmente, cuando una aplicación encuentra un error, realiza cualquier cantidad de tareas de limpieza. A continuación, informa al usuario del error y proporciona opciones para solucionarlo.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
