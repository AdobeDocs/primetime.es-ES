---
seo-title: Autenticación de usuarios
title: Autenticación de usuarios
uuid: 191964eb-cd68-47a6-8214-aec01f993df4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Autenticación de usuario{#user-authentication}

Una solicitud de acceso a Adobe puede contener un token de autenticación.

Si se utilizó la autenticación de nombre de usuario y contraseña, la solicitud puede contener un `AuthenticationToken` generado por el `AuthenticationHandler`. Para acceder y verificar el token, utilice `RequestMessageBase.getAuthenticationToken()`. Para iniciar una solicitud de nombre de usuario y contraseña en el cliente, utilice el ActionScript `DRMManager.authenticate()` o la API de iOS.

Si el cliente y el servidor utilizan un mecanismo de autenticación personalizado, el cliente obtiene un autentificador de autenticación mediante otro canal y establece el autentificador de autenticación personalizado mediante la API de `DRMManager.setAuthenticationToken` ActionScript 3.0. Use `RequestMessageBase.getRawAuthenticationToken()` para obtener el token de autenticación personalizado. La implementación del servidor es responsable de determinar si el autentificador personalizado es válido.
