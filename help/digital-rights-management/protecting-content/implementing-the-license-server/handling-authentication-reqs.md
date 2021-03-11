---
title: Gestión de solicitudes de autenticación
description: Gestión de solicitudes de autenticación
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Gestionar solicitudes de autenticación {#handle-authentication-requests}

La clase `AuthenticationHandler` se utiliza para procesar solicitudes de autenticación. Solo se utiliza para la autenticación de nombre de usuario y contraseña.

Al generar el token de autenticación, se debe especificar la fecha de caducidad del token. Las propiedades personalizadas también se pueden incluir en el token. Si se establece, el servidor verá esas propiedades cuando el token de autenticación se envíe en solicitudes posteriores. Consulte [Gestión de solicitudes de licencia](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) para obtener información sobre la administración de tokens de autenticación personalizados.

El controlador lee una solicitud de autenticación y analiza el mensaje de solicitud cuando se llama a `parseRequest()`. La implementación del servidor examina las credenciales de usuario en la solicitud y, si las credenciales son válidas, genera un objeto `AuthenticationToken` llamando a `getRequest().generateAuthToken()`. Si no se llama a `AuthenticationRequestMessage.generateAuthToken()` antes de `close()`, se envía un código de error de autenticación.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de la solicitud es &quot;URL del servidor de licencias en los metadatos: + &quot; [!DNL /flashaccess/authn/v4]&quot;. Si la versión de protocolo 3 es la máxima admitida por el cliente o el servidor, los clientes de Adobe Primetime DRM envían las solicitudes de autenticación a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;

