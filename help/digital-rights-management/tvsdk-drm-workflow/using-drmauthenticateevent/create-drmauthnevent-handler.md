---
description: El objeto DRMAuthenticateEvent se envía cuando un objeto Primetime intenta reproducir contenido protegido que requiere credenciales de usuario para la autenticación antes de la reproducción (y aún no se ha realizado la autenticación). El controlador DRMAuthenticateEvent es responsable de recopilar las credenciales necesarias (nombre de usuario, contraseña y tipo) y pasar los valores al método .setDRMAuthauthenticationCredentials() para la validación.
title: Creación de un controlador DRMAuthenticateEvent
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Cree un controlador DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

El objeto DRMAuthenticateEvent se envía cuando un objeto Primetime intenta reproducir contenido protegido que requiere credenciales de usuario para la autenticación antes de la reproducción (y aún no se ha realizado la autenticación). El controlador DRMAuthenticateEvent es responsable de recopilar las credenciales necesarias (nombre de usuario, contraseña y tipo) y pasar los valores al método .setDRMAuthauthenticationCredentials() para la validación.

La aplicación debe proporcionar algún mecanismo para obtener las credenciales del usuario. Por ejemplo, la aplicación podría proporcionar a un usuario una interfaz de usuario sencilla para introducir valores de nombre de usuario y contraseña. Además, debería proporcionar un mecanismo para controlar y limitar los intentos repetidos de error de autenticación.

Cree un controlador de eventos que pase un conjunto de credenciales de autenticación codificadas al objeto Primetime que originó el evento:

```
var connection:NetConnection = new NetConnection();  
connection.connect(null);  
var videoStream:Primetime = new Primetime(connection);  
 
videoStream.addEventListener( 
  DRMAuthenticateEvent.DRM_AUTHENTICATE,  
  drmAuthenticateEventHandler)  
  private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
    videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
} 
```

(El código para reproducir el vídeo y asegurarse de que se ha realizado una conexión correcta al flujo de vídeo no se incluye aquí).
