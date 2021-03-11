---
title: Autenticación de usuarios
description: Autenticación de usuarios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Autenticación de usuario {#user-authentication}

Una solicitud de Adobe Primetime DRM puede contener un token de autenticación.

Si se utilizó la autenticación de nombre de usuario/contraseña, la solicitud puede incluir un `AuthenticationToken` generado por el `AuthenticationHandler`. Si desea acceder y verificar el token, debe utilizar `RequestMessageBase.getAuthenticationToken()`. Para iniciar una solicitud de nombre de usuario y contraseña en el cliente, utilice el ActionScript `DRMManager.authenticate()` o la API de iOS.

Si el cliente y el servidor utilizan un mecanismo de autenticación personalizado, el cliente obtiene un token de autenticación a través de otro canal y establece el token de autenticación personalizado mediante la API `DRMManager.setAuthenticationToken` ActionScript 3.0. Utilice `RequestMessageBase.getRawAuthenticationToken()` para obtener el token de autenticación personalizado. La implementación del servidor determina si el token de autenticación personalizado es válido.
