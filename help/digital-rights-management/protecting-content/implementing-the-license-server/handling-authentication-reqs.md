---
seo-title: Administrar solicitudes de autenticación
title: Administrar solicitudes de autenticación
uuid: abcb9cf6-668e-405c-9659-9ed1bcc33024
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Administrar solicitudes de autenticación {#handle-authentication-requests}

La clase `AuthenticationHandler` se utiliza para procesar solicitudes de autenticación. Solo se utiliza para la autenticación de nombre de usuario y contraseña.

Al generar el token de autenticación, se debe especificar la fecha de caducidad del token. También se pueden incluir propiedades personalizadas en el token. Si se establece, el servidor verá dichas propiedades cuando se envíe el autentificador en solicitudes posteriores. Consulte [Administración de solicitudes de licencia](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) para obtener información sobre cómo administrar los tokens de autenticación personalizados.

El controlador lee una solicitud de autenticación y analiza el mensaje de solicitud cuando se llama a `parseRequest()`. La implementación del servidor examina las credenciales de usuario en la solicitud y, si las credenciales son válidas, genera un objeto `AuthenticationToken` llamando a `getRequest().generateAuthToken()`. Si no se llama a `AuthenticationRequestMessage.generateAuthToken()` antes de `close()`, se envía un código de error de autenticación.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos: + &quot; [!DNL /flashaccess/authn/v4]&quot;. Si la versión 3 del protocolo es la máxima admitida por el cliente o el servidor, los clientes de Adobe Primetime DRM envían las solicitudes de autenticación a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. De lo contrario, las solicitudes de autenticación se envían a &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;

