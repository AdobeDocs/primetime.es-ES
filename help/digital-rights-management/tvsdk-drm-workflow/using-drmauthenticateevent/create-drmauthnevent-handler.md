---
description: El objeto DRMAuthenticateEvent se distribuye cuando un objeto Primetime intenta reproducir contenido protegido que requiere una credencial de usuario para la autenticación antes de la reproducción (y aún no se ha realizado la autenticación). El controlador DRMAuthenticateEvent se encarga de reunir las credenciales necesarias (nombre de usuario, contraseña y tipo) y pasar los valores al método .setDRMAuthauthenticationCredentials() para la validación.
seo-description: El objeto DRMAuthenticateEvent se distribuye cuando un objeto Primetime intenta reproducir contenido protegido que requiere una credencial de usuario para la autenticación antes de la reproducción (y aún no se ha realizado la autenticación). El controlador DRMAuthenticateEvent se encarga de reunir las credenciales necesarias (nombre de usuario, contraseña y tipo) y pasar los valores al método .setDRMAuthauthenticationCredentials() para la validación.
seo-title: Creación de un controlador DRMAuthenticateEvent
title: Creación de un controlador DRMAuthenticateEvent
uuid: 58330691-d0b5-46bd-9b1d-8dc597580d31
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# Creación de un controlador DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

El objeto DRMAuthenticateEvent se distribuye cuando un objeto Primetime intenta reproducir contenido protegido que requiere una credencial de usuario para la autenticación antes de la reproducción (y aún no se ha realizado la autenticación). El controlador DRMAuthenticateEvent se encarga de reunir las credenciales necesarias (nombre de usuario, contraseña y tipo) y pasar los valores al método .setDRMAuthauthenticationCredentials() para la validación.

La aplicación debe proporcionar algún mecanismo para obtener las credenciales de usuario. Por ejemplo, la aplicación podría proporcionar a un usuario una interfaz de usuario sencilla para introducir los valores de nombre de usuario y contraseña. Además, debe proporcionar un mecanismo para controlar y limitar los intentos de error de autenticación repetida.

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

(Aquí no se incluye el código para reproducir el vídeo y asegurarse de que se ha realizado una conexión correcta al flujo de vídeo).
