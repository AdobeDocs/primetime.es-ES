---
description: El objeto DRMAuthenticateEvent se distribuye cuando un objeto Primetime intenta reproducir contenido protegido que requiere una credencial de usuario para la autenticación antes de la reproducción (y la autenticación aún no se ha realizado). El controlador DRMAuthenticateEvent es responsable de recopilar las credenciales necesarias (nombre de usuario, contraseña y tipo) y pasar los valores al método .setDRMAuthenticationCredentials() para su validación.
title: Crear un controlador DRMAuthEvent
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Crear un controlador DRMAuthEvent{#create-a-drmauthenticateevent-handler}

El objeto DRMAuthenticateEvent se distribuye cuando un objeto Primetime intenta reproducir contenido protegido que requiere una credencial de usuario para la autenticación antes de la reproducción (y la autenticación aún no se ha realizado). El controlador DRMAuthenticateEvent es responsable de recopilar las credenciales necesarias (nombre de usuario, contraseña y tipo) y pasar los valores al método .setDRMAuthenticationCredentials() para su validación.

La aplicación debe proporcionar algún mecanismo para obtener las credenciales de usuario. Por ejemplo, la aplicación podría proporcionar a un usuario una interfaz de usuario sencilla para introducir los valores de nombre de usuario y contraseña. Además, debe proporcionar un mecanismo para gestionar y limitar los intentos de error de autenticación repetidos.

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

(El código para reproducir el vídeo y asegurarse de que se ha realizado correctamente una conexión con el flujo de vídeo no se incluye aquí).
