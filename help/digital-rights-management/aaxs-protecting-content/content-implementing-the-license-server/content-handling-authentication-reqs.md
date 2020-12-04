---
seo-title: Gestión de solicitudes de autenticación
title: Gestión de solicitudes de autenticación
uuid: 036582d4-611c-4772-b247-81a3144fd5d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Gestión de solicitudes de autenticación{#handling-authentication-requests}

La clase `AuthenticationHandler` se utiliza para procesar solicitudes de autenticación. Solo se utiliza para la autenticación de nombre de usuario y contraseña.

Al generar el token de autenticación, se debe especificar la fecha de caducidad del token. También se pueden incluir propiedades personalizadas en el token. Si se establece, el servidor verá dichas propiedades cuando se envíe el autentificador en solicitudes posteriores. Consulte [Administración de solicitudes de licencia](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) para obtener información sobre cómo administrar los tokens de autenticación personalizados.

El controlador lee una solicitud de autenticación y analiza el mensaje de solicitud cuando se llama a `parseRequest()`. La implementación del servidor examina las credenciales de usuario en la solicitud y, si las credenciales son válidas, genera un objeto `AuthenticationToken` llamando a `getRequest().generateAuthToken()`. Si no se llama a `AuthenticationRequestMessage.generateAuthToken()` antes de `close()`, se envía un código de error de autenticación.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos: + &quot;/flashaccess/authn/v4&quot;. Si la versión 3 del protocolo es la máxima admitida por el cliente o el servidor, los clientes de Adobe Access enviarán solicitudes de autenticación a &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/authn/v3&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/authn/v1&quot;

