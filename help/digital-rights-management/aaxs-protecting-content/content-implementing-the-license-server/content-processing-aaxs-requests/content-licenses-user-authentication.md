---
title: Autenticación de usuario
description: Autenticación de usuario
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Autenticación de usuario{#user-authentication}

Una solicitud de acceso de Adobe puede contener un token de autenticación.

Si se ha utilizado la autenticación de nombre de usuario y contraseña, la solicitud puede contener un `AuthenticationToken` generado por el `AuthenticationHandler`. Para acceder y verificar el token, utilice `RequestMessageBase.getAuthenticationToken()`. Para iniciar una solicitud de nombre de usuario y contraseña en el cliente, utilice el `DRMManager.authenticate()` ActionScript o API de iOS.

Si el cliente y el servidor utilizan un mecanismo de autenticación personalizado, el cliente obtiene un token de autenticación a través de algún otro canal y establece el token de autenticación personalizado utilizando `DRMManager.setAuthenticationToken` API de ActionScript 3.0. Uso `RequestMessageBase.getRawAuthenticationToken()` para obtener el token de autenticación personalizado. La implementación del servidor es responsable de determinar si el token de autenticación personalizado es válido.
